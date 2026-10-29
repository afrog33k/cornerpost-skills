# First-run checks and practical tasks

## Context every receiving assistant needs

Twenty is the CRM used in this workflow. A company is an organization, a person is a contact, an opportunity is a deal, and tasks/notes can link to those records. Read [the operator guide](TWENTY-OPERATIONS.md) for discovery, structured values, relation IDs and practical tool arguments. Do not assume the receiving assistant has any earlier conversation context.

Use the recipient's Cornerpost company email shown on their invitation. Do not assume their browser's personal account is the invited identity. Find the invitation in an already-authorized source or ask for the missing identity privately; have the owner select that account and complete login/MFA/consent. Workspace URL, account details and private invitation links belong in the private conversation, not this package. Verify the intended workspace through trusted setup details and a recognized narrow read; a successful browser login alone does not prove the CRM connector's identity.

## Establish capability from actual evidence

Inventory the callable connector and computer/browser tools available in this conversation. Inspect discovery, schema, skill/help and execution wrappers. In this Twenty connector, record operations may be discovered by `get_tool_catalog`, learned by `learn_tools`, and invoked through `execute_tool`; a missing top-level create tool does not establish read-only access. Learn the relevant schemas and verify a harmless recognized read. Check write capability from actual schemas and permissions without creating a test record just to probe it.

When tools are missing, use the supported refresh/reconnection flow, fresh conversation, or app update/restart if available and appropriate. Preserve unsaved work and obtain required owner consent for login, new access or protected app changes. Reinspect the actual calls afterward. Another conversation's tools do not prove this one's capability. A recovered session does not prove caching or OAuth scope was the cause. Do not broaden permissions blindly. If a real authorized write fails, retain the sanitized tool/arguments/error/time and report the exact target and blocked field/action.

## Select the right computer, browser and view

A browser tab, window, browser profile, physical display and connected computer are different targets. Inventory the connected computer and browser surfaces before choosing. A personal browser profile may be signed into a different account; multiple windows may contain similar tabs. Resolve ambiguous targets with one focused choice instead of assuming the active tab or a monitor position.

Before a visual action, select the intended computer/window/tab using the current supported controls, obtain a current screenshot of that visible target and inspect it. Confirm the page and control are actually visible. Do not say you see a screen from a tab title, remote connection indicator, old screenshot or the user's description. If the screen changes materially or handoff returns, reacquire the relevant view before acting. Do not inspect or retain secret values during login/MFA.

If a companion or computer connection cannot provide a usable screenshot, report that missing capability and pause dependent visual actions. Continue safe connector work or guide the owner through the protected step. This package does not add screenshot capability to a companion app. Never click a guessed location to compensate for missing visual evidence.

## Gather context, then act within scope

For the requested company or deal, read relevant available authorized documents, Notion pages/meeting transcripts, CRM records and calendar entries. Use the company/person names, deal and useful time window as search context. Calendar reading can proceed when that connector is already authorized for the requested workflow; a missing connector needs a separate supported connection/owner-consent step. Do not treat “not connected” as “no meetings/documents exist.”

Cite the source, date and factual observation in the private result; distinguish inference and gaps. Avoid dumping full transcripts into CRM notes. Read enough to identify the agreed facts and next action. If a source is unavailable, state that precise gap, use verified context already available, and continue independent work. Do not fabricate commitments, contact details, dates or deal amounts.

Where desktop task agents are available, parallelize independent document/transcript search, calendar context and schema inspection. Keep one owner for writes and shared browser state. Consolidate their evidence before acting. Do not invent task-agent tools, create unrelated conversations or contact people as part of delegation.

For an agency baseline, organize the work around its company, relevant people, actual opportunity and next action. Make ordinary reversible choices about document structure, concise summaries and omitted unknown optional fields; label assumptions. Preserve the actual record owner and resolve an assignee from evidence rather than assigning the current speaker by default. Distinguish missing context, missing callable access and an unknown failure cause. Escalate only the specific essential fact or permission, then give a concise usable outcome.

A direct request such as “Add Example Agency as a company with this supplied website” already authorizes that scoped addition. Search duplicates, resolve the target, create/reuse as appropriate and read back; do not ask “Shall I go ahead?” again. Ask only when a material ambiguity, conflict, missing decision, expanded scope or platform control requires it. Access to read sources does not authorize sending messages, inviting attendees or making unspecified CRM changes.

## Useful first tasks

| Request | Action and success evidence |
| --- | --- |
| Add an agency/company | Learn company tools; search supplied domain and plausible name variants; reuse a clear match or create the authorized company. Read back ID/name/domain. Unknown optional facts stay omitted. |
| Add a contact to that agency | Resolve the company and possible person duplicates; preserve existing composite fields. Create/update within scope and read back the person and `companyId`. |
| Turn a conversation into next steps | Read the available transcript/notes and current CRM context; summarize sourced facts and identify an actual agreed action. Save only authorized notes/tasks and verify their target relationships. Resolve the due date in the owner's timezone. |
| Prepare a basic agency instructions package | Use the supplied business goal and available documents to draft concise reusable agency instructions, relevant entities, a repeatable task flow and exact success checks. Infer ordinary structure; label assumptions and omit unsupported facts. Save to the requested authorized private destination, read it back, then use the supported skill route if the owner asked to save a skill. Do not publish the agency's private context here. |
| Work a deal | Resolve the company, person and opportunity; apply the authorized stage/amount/note/next-action change using learned types, then read back saved values and relation IDs. Do not create an opportunity for every contact automatically. |
| Check today's relevant meetings | Read the already-authorized calendar for the requested day/timezone and join it with relevant CRM/context. Report conflicts or missing connections. Creating/changing/inviting remains a separately scoped action. |

## Durable enrollment and completion gate

When asked to save these workflows, inspect the actual supported skill route and target surface. Save/import only with the owner's authorization, then verify an installed handle/identity, the readable skill/reference resources, and the version/source/manifest hash that can actually be established. Test a harmless invocation or supported discovery/readback on the next applicable turn. A pasted prompt, file attachment or suggestion is not an installed skill. Record verification limits if the platform hides installed bytes.

For version checks, use the `skill-release-updates` package and its [update guide](https://github.com/afrog33k/cornerpost-skills/blob/main/skills/skill-release-updates/references/UPDATE-GUIDE.md). Keep the real installed receipt privately. Each owner enrolls cadence, timezone, destination and activation policy through their available native scheduler. Verify the saved scheduler reference/settings and a check result in that execution environment before claiming automatic checks work. Distinguish an enrolled schedule from a first run that has not completed. Preserve the old verified package and local customization. If scheduling or activation is unsupported, report the specific gap; this repository supplies no daemon or remote installer.

First-session success requires a recognized CRM read, one requested useful action with saved-value/relationship readback, and an honest skill/update state: verified installed/enrolled, chat-only, deferred or blocked. Show what is complete and the smallest remaining owner step. Do not mark a missing screenshot, unverified write or merely proposed schedule complete.
