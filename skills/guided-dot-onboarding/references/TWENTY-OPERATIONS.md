# Twenty CRM: quick operator guide

Schema checked against the connected Twenty MCP on 29 October 2026. Relearn the relevant schemas in the assistant's own connection before writing; workspaces and permissions can differ.

## Why creating a record can be awkward

This connector exposes a discovery layer, then object-specific tools. A contact is a `person`; a deal is an `opportunity`. Names, email addresses and money use structured fields, not plain strings. Relationships use record UUIDs, not names. Read calls require `select`. Some links are separate records. These are plausible failure points, **not a diagnosis of the assistant's unseen error**.

Earlier live checks in the tested connection passed company/person/deal/task creation and readback, person-company linking, and a task status change and restoration. This guide's examples are schema-verified templates, not commands executed during guide preparation. Notes and note/task target creation have not been live-tested here. Those successes do not establish the assistant's account or permissions.

## The operating loop

1. **Confirm context and scope.** Use trusted connection details to confirm the intended account/workspace. Corroborate with a narrowly scoped read of a known record if available. No `get_current_workspace` or `get_current_user` tool was found; do not invent one or treat the member list as proof of the acting account. If the workspace is uncertain, stop before writing.
2. **Use the built-in guidance.** `list_skills({})` currently includes `data-manipulation` and `crm-hygiene`. Load `data-manipulation` for record work; load `crm-hygiene` for duplicate audits. Skills are instructions, not grants of permission. For bulk imports, use the built-in import workflow rather than extending these one-record examples.
3. **Learn once, in a batch.** Call `learn_tools` with every needed tool name and `aspects: ["description", "schema"]`. Names follow forms such as `find_many_people`, `find_one_person`, `create_one_person`, `update_one_person`. Unknown names return `notFound`; resolve that before execution. Use `get_tool_catalog` only when you do not know which tool exists.
4. **Resolve duplicates and relationships first.** Query only relevant candidates. Reuse a clear match; do not silently create over an ambiguous match, overwrite a relationship, or merge/delete duplicates. Honor `hasNextPage` before concluding no match exists.
5. **Execute only the authorized mutation.** Pass the learned name to `execute_tool`. Fields go directly inside `arguments`: no invented `data`, `input`, or `filter` wrapper. A create returns its generated ID; keep that ID for dependent work.
6. **Read back and compare.** Use `find_one_*` with the returned ID and a nonempty `select`. Check important values and relationship IDs, not merely whether the call returned successfully. Report created/reused/updated/blocked outcomes separately.

Discovery example (add the relevant task/note tools when needed):

```json
{"toolNames":["find_many_companies","create_one_company","find_one_company","find_many_people","create_one_person","update_one_person","find_one_person","find_many_opportunities","create_one_opportunity","find_one_opportunity"],"aspects":["description","schema"]}
```

Pass that object to `learn_tools`, not `execute_tool`.

## Templates: resolve real values first; do not auto-run

The following JSON objects are **arguments to `execute_tool`**. Names, addresses and dates are illustrative, not instructions to create demo data. Replace every `<..._UUID>` with a UUID returned from a verified read/create in the intended workspace. Never send the placeholders. Omit optional fields whose values are unknown; do not fill them with guesses or `null` unless the learned schema permits it. Never execute the whole guide as a batch.

### 1. Find or create a company

Search by supplied domain and name before creating. The current company duplicate criteria include name and domain. Domain formatting can vary, so an exact URL miss is not conclusive: inspect plausible name/domain variants. Names alone can be ambiguous.

```json
{"toolName":"find_many_companies","arguments":{"or":[{"domainName":{"primaryLinkUrl":{"eq":"https://example.com"}}},{"name":{"ilike":"Example Company"}}],"limit":10,"select":["id","name","domainName"]}}
```

Only when no matching record exists and creation is authorized:

```json
{"toolName":"create_one_company","arguments":{"name":"Example Company","domainName":{"primaryLinkUrl":"https://example.com","primaryLinkLabel":"Website"}}}
```

Read back:

```json
{"toolName":"find_one_company","arguments":{"id":"<COMPANY_UUID>","select":["id","name","domainName"]}}
```

### 2. Find or create a contact; link to the company

```json
{"toolName":"find_many_people","arguments":{"emails":{"primaryEmail":{"eq":"alex@example.com"}},"limit":10,"select":["id","name","emails","companyId"]}}
```

A primary-email miss does not exclude an address stored in `additionalEmails`. Check plausible name/company candidates and inspect their emails before creating. Current person duplicate criteria also include full name and LinkedIn. Use the metadata criteria as clues, not as query field names: queries use composites such as `name.firstName` represented as nested objects, never dotted keys.

```json
{"toolName":"find_many_people","arguments":{"name":{"firstName":{"ilike":"Alex"},"lastName":{"ilike":"Example"}},"limit":10,"select":["id","name","emails","companyId","linkedinLink"]}}
```

Only after resolving candidates:

```json
{"toolName":"create_one_person","arguments":{"name":{"firstName":"Alex","lastName":"Example"},"emails":{"primaryEmail":"alex@example.com"},"companyId":"<COMPANY_UUID>"}}
```

To link an **existing** person, update rather than recreate; first read their current company and resolve any conflict with the requested change:

```json
{"toolName":"update_one_person","arguments":{"id":"<PERSON_UUID>","companyId":"<COMPANY_UUID>"}}
```

```json
{"toolName":"find_one_person","arguments":{"id":"<PERSON_UUID>","select":["id","name","emails","companyId"]}}
```

Use scalar `companyId`, not `company: {"id": ...}` or a company name. Do not send empty `additionalEmails` during an update merely as boilerplate; that may clear existing data. Before editing a composite, read and preserve its existing values unless the user asked to replace them.

### 3. Create a deal with the correct amount and stage

Search `find_many_opportunities` by name and company before creation or any retry:

```json
{"toolName":"find_many_opportunities","arguments":{"name":{"eq":"Example opportunity"},"companyId":{"eq":"<COMPANY_UUID>"},"select":["id","name","companyId","pointOfContactId","amount","stage"]}}
```

```json
{"toolName":"create_one_opportunity","arguments":{"name":"Example opportunity","companyId":"<COMPANY_UUID>","pointOfContactId":"<PERSON_UUID>","amount":{"amountMicros":1250000000,"currencyCode":"USD"},"stage":"NEW"}}
```

USD 1,250 = **1,250,000,000 micros**, not cents. Use the user's actual currency. Relearn `stage`: this connection currently allows `NEW`, `SCREENING`, `MEETING`, `PROPOSAL`, `CUSTOMER`; do not invent a UI label or assume another workspace has the same enum. `ownerId` is a workspace-member UUID, while `pointOfContactId` is a person UUID. Optional `closeDate` must be an ISO date-time if included.

```json
{"toolName":"find_one_opportunity","arguments":{"id":"<OPPORTUNITY_UUID>","select":["id","name","amount","stage","companyId","pointOfContactId"]}}
```

### 4. Create a dated task, then attach it if requested

Resolve the intended assignee with `find_many_workspace_members`, selecting `id`, `name` and only necessary identifying fields. Distinguish duplicate names; a contact/person ID is not an assignee ID. Resolve relative dates in the user's timezone and provide an ISO date-time with an offset. Do not assume a sample date or UTC is the user's intent.

Before creation, search by the intended title/date/assignee; inspect candidates rather than treating a shared title as identity:

```json
{"toolName":"find_many_tasks","arguments":{"title":{"eq":"Prepare proposal"},"dueAt":{"eq":"2026-11-02T09:00:00Z"},"assigneeId":{"eq":"<MEMBER_UUID>"},"select":["id","title","dueAt","assigneeId","status"]}}
```

```json
{"toolName":"create_one_task","arguments":{"title":"Prepare proposal","dueAt":"2026-11-02T09:00:00Z","status":"TODO","assigneeId":"<MEMBER_UUID>","bodyV2":{"markdown":"Prepare the agreed proposal."}}}
```

Current task statuses are `TODO`, `IN_PROGRESS`, `DONE`; relearn before using them. Creating a task does **not** automatically link it to a company/person/deal. Resolve the returned task ID, query `find_many_task_targets` for that task/target pair, and create a missing link only:

```json
{"toolName":"create_one_task_target","arguments":{"taskId":"<TASK_UUID>","targetOpportunityId":"<OPPORTUNITY_UUID>"}}
```

```json
{"toolName":"find_one_task","arguments":{"id":"<TASK_UUID>","select":["id","title","dueAt","status","assigneeId","bodyV2"]}}
```

```json
{"toolName":"find_many_task_targets","arguments":{"taskId":{"eq":"<TASK_UUID>"},"targetOpportunityId":{"eq":"<OPPORTUNITY_UUID>"},"select":["id","taskId","targetOpportunityId"]}}
```

For a company/person attachment, use `targetCompanyId`/`targetPersonId` instead. Create one target record per intended attachment. If linking fails, retain and report the task ID; do not create another task.

### 5. Create a note, then its record link

This is **schema-verified, not live-tested**. Search `find_many_notes` by title/content and inspect relevant `find_many_note_targets` before creation; a title alone is not a unique key.

```json
{"toolName":"create_one_note","arguments":{"title":"Discovery summary","bodyV2":{"markdown":"Confirmed requirements and agreed next steps."}}}
```

Capture the returned note ID. Query for the exact note/target pair before creating a missing link:

```json
{"toolName":"create_one_note_target","arguments":{"noteId":"<NOTE_UUID>","targetCompanyId":"<COMPANY_UUID>"}}
```

```json
{"toolName":"find_one_note","arguments":{"id":"<NOTE_UUID>","select":["id","title","bodyV2"]}}
```

```json
{"toolName":"find_many_note_targets","arguments":{"noteId":{"eq":"<NOTE_UUID>"},"targetCompanyId":{"eq":"<COMPANY_UUID>"},"select":["id","noteId","targetCompanyId"]}}
```

Use `targetPersonId` or `targetOpportunityId` for other attachments. The note body and the note's CRM attachment are separate writes. Current note schemas expose no `isDemo` field; do not add one just because other objects have it.

## When a call fails

| Symptom | the assistant's next action |
| --- | --- |
| Unknown tool/field, wrong type, missing `select`, invalid enum or UUID | Relearn the affected schema; compare the exact arguments. Correct the invalid shape, not the user's data. Do not keep retrying the same payload. |
| Invalid relation / referenced record not found | Verify the related record exists in this workspace and the ID belongs to the correct object. Metadata field/object IDs are not record IDs. Do not substitute a name. |
| Unauthorized / forbidden / no permission to write field | Separate connection authentication from object/field permissions. Report the exact blocked action/field; request the appropriate account/admin remedy. Do not switch identities or bypass restrictions. Omit a blocked optional field only if the authorized task remains correct, and disclose the omission; never silently drop required business data. |
| Timeout / connection dropped / uncertain result | **Do not recreate blindly.** If an ID was returned, read it. Otherwise reconcile with a narrow search using the intended identifying fields and inspect matching records/links. Resume only missing steps. If the outcome is still ambiguous, stop the write and report it; no duplicate retry. |
| Duplicate / conflicting candidates | Inspect and resolve the existing match. Do not auto-merge, delete, or overwrite. A search-before-create flow reduces duplicates but is not an atomic uniqueness guarantee. |
| Read returns no match | Check workspace, filters, permitted visibility and pagination. An empty result is not proof a record does not exist. |

Keep the exact tool name, sanitized arguments, error text and timestamp for diagnosis. Keep tokens, private hosts, personal emails and customer UUIDs out of public troubleshooting. The exact assistant error is still needed to identify its cause.

**Deletion rule:** always obtain explicit approval before deleting any record, file, cache, message or other data, including cleanup of examples. Do not create test records unless authorized.

## Sources and maintenance

- Primary evidence: this connection's `learn_tools` schemas, company/person `get_object_metadata` duplicate criteria, and `list_skills` / `load_skills` (`data-manipulation`, `crm-hygiene`), inspected 29 October 2026.
- Twenty's official [permission overview](https://docs.twenty.com/user-guide/permissions-access/overview#key-features) documents separate object, field and settings permissions.
- Prefer live schemas over this snapshot. Use `search_help_center` before giving unverified Twenty UI instructions. This guide is an operator supplement, not a replacement for existing built-in skills or the user's authorization.

## When an assistant reports read-only tools

Inspect the tools actually callable in that conversation rather than relying on the assistant's summary. This connector has two layers: top-level discovery, schema, skills, help and execution wrappers; and record operations such as `create_one_opportunity`. Discover record operations with `get_tool_catalog`, learn their schemas with `learn_tools`, then invoke them through `execute_tool`. An operation may be callable through that wrapper even when it is not listed as a separate top-level tool.

Compare the exact connector and actual calls. Where supported, use the app's update, refresh or reconnection flow, or try a fresh conversation; verify the resulting tools instead of assuming the step fixed access. Another conversation's tool list does not prove the original session can call those tools. Do not present caching or OAuth scopes as a proven cause, and never broaden permissions merely to test.

Before resuming approved writes, verify the intended workspace and check for existing matching records, including the outcome of any uncertain prior attempt. Retain returned IDs and read back saved values and relationships. The presence of write tools does not prove that a write succeeded.
