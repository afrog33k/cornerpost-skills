---
name: guided-dot-onboarding
description: Guide a user through supported assistant, computer, and CRM setup, verify each connection, then complete a first approved deal workflow. Use for first-run onboarding or resuming that setup; do not treat this skill as permission to install software, access another account, or change business records.
---

# Guided dot onboarding

## Outcome

Help the user reach one useful, verified deal-work result. Operate the available tools and setup pages yourself where supported. The user handles sign-in, consent, protected steps, and business choices. Do not give them a long checklist to perform alone.

This is workflow guidance, not an installer or an access grant. A public copy must contain only generic instructions. Keep names, private installation links, workspace details, record identifiers, and checkpoints in the user's private conversation or authorized private storage—not in this public skill or its hosting gist.

Read [onboarding checks and common tasks](references/ONBOARDING-CHECKS.md) at first setup or when browser, screen, context, write access or durable enrollment is uncertain.

## Interaction contract

- Start with a short promise: “I'll check what's already connected, handle the supported setup, and pause only where I need you.” Then inspect actual capabilities.
- Reuse context and completed setup. Ask one focused question at a time only when the answer affects the next action. Do not ask for information the tools can safely establish.
- Use already-authorized actions without asking for a redundant go-ahead. Resolve missing material facts, ambiguous targets, new access and protected controls when needed.
- Gather relevant context from available authorized documents, Notion/transcripts, CRM and calendar before asking the user to repeat it. Use parallel desktop task agents for independent read-only work when available; keep one writer for shared CRM/UI state.
- Prefer existing connected apps over computer access. A chat app, cloud computer, connected computer, plugin installation, and service login are separate things.
- Say what you will open or change, then do it when authorized. Do not pretend to open a page without a successful tool result. Use current documentation or observed UI for exact controls.
- Pause at credentials, MFA, consent, protected actions, or a business decision. Never solicit passwords, one-time codes, recovery codes, tokens, or keys in chat. Resume after the protected step without inspecting or retaining its secret values.
- If completion is observable, check it. Ask “Have you finished that step?” only when you cannot observe it; the answer is a signal to recheck, not proof of connection.
- Respect platform confirmation and access controls. Do not switch tools to evade a block. Do not execute remote shell commands or fetched scripts as a setup workaround.
- Do not buy anything, change billing, delete data, or broaden permissions as part of onboarding. If any later task needs one of these, stop for specific authorization and follow the applicable controls. Even routine deletion requires approval.
- Do not equate a suggestion with installation, installation with authorization, or an accepted request with verified success.

## State machine

Advance only when the exit evidence exists. Pause dependent work when blocked, continue unrelated safe preparation, and resume from the last verified checkpoint.

### 1. Inspect

Check the actual tools, connected services, permissions visible through supported interfaces, current environment, and any prior checkpoint. For this onboarding, Twenty is the intended CRM: it stores companies, people, opportunities (deals), notes and tasks. Confirm the recipient's invited workspace from trusted private context. Use the Cornerpost company email named on their invitation, not a guessed personal account. If a different workflow is requested, confirm its CRM and outcome. If the workspace or invitation identity is missing, ask only for that information privately. Do not require optional email or calendar setup to proceed.

**Exit evidence:** a short map of what works, what is missing, and which next step actually needs the missing capability.

### 2. Explain and request only what is needed

Explain the smallest missing requirement and why it matters. If a connector can do the task, use it; do not require computer access. If computer access is necessary, check whether a supported working connection already exists, then request access through the current verified product flow. A task link does not grant computer access. If the interface or connection route is unknown, say so and use current product help rather than inventing controls.

**Exit evidence:** authorized usable capability, or a precise pause stating action, target, reason, and required user step.

### 3. Open, act, hand off, verify

Open the relevant official setup page or supported setup card when a tool can do so. Perform non-protected steps within the approved scope. Explain the permissions the user is being asked to grant, without accepting consent for them. Hand off for the protected step. If you cannot open the page, provide the verified route and explain that limitation.

After handoff, inspect the actual connection result or run a minimal harmless read. If a service remains unavailable, distinguish an unfinished sign-in, missing authorization, unsupported account, temporary failure, and unknown cause. Do not ask the same unchanged question repeatedly or claim broader capabilities than the result proves.

**Exit evidence:** a working capability test, not merely “Done,” a setup card, or a new icon.

### 4. Save this workflow only if supported

Inspect the current account's supported skill creation/import/installation options. Explain the available destination and scope. If the owner has already requested saving or installing this workflow in that scope, proceed within that authorization; otherwise ask whether they want it saved. Complete any required platform confirmation and owner consent step. If there is no supported route or permission, continue using these instructions in this conversation and say it is not installed.

Do not assume a gist URL imports a skill, a folder is a plugin, local installation transfers to another account, or sharing instructions transfers connector access. Do not manufacture an installer or execute a remote command. Keep this step optional; it must not block the first useful CRM task.

**Exit evidence:** confirmed saved skill in the intended surface, or explicit chat-only mode.

### 5. Connect the CRM

Use an existing working CRM connection first. Otherwise look for the intended provider through supported plugin discovery; verify the exact result before suggesting it. If the user supplies a private installation link, keep it private and verify its target. A plugin might be unavailable for this account or require an administrator; do not promise cross-account installation.

Present the minimum necessary connection and permission request. Let the user complete login and consent. Confirm the expected workspace/account through non-secret identity details, then perform a minimal read-only connection check. Inspect available objects, fields, and allowed actions before assuming a deal schema or write support.

**Exit evidence:** verified read access to the intended CRM workspace and an honest statement of any remaining write or object limitations.

### 6. Show a small read-only demonstration

Use a clearly designated demo record if one is already provided and accessible. Otherwise ask for the record or category to read; do not create a synthetic record in the live CRM. Summarize a small relevant result and clearly distinguish real data from an example. Do not modify a record merely to prove the connection.

**Exit evidence:** one verified read result the user can recognize, with no mutation.

### 7. Move naturally into deal work

Ask, for example: “Which deal should we work on first?” or “What happened on that deal, and what needs to happen next?” Use the user's answer and accessible evidence to identify the exact record. Clarify ambiguity rather than guessing between similar contacts, accounts, or opportunities.

Read the relevant record and current field values. Separate evidence from inference and missing information. Make a concise proposal: the target record, exact fields or notes to change, proposed new values, and any follow-up communication. Do not invent amounts, dates, stages, commitments, or recipients.

**Exit evidence:** a precise, reviewable proposal for a resolved record, or a specific missing business decision.

### 8. Approve, write, read back

Check whether the user has already authorized these exact CRM changes. If the target and scope are clear, carry them out without a redundant go-ahead; otherwise request only the missing material decision or required approval. Do not treat approval to connect or read as approval to write. Before writing, check whether the same action already happened and whether relevant values changed since the proposal. If there is a material conflict, show it and obtain an updated decision.

Use the narrowest supported write, then read back the affected record. Report verified final values and any discrepancy. If a write times out or returns an ambiguous result, read current state before retrying to avoid duplicate notes or records. Do not roll back or delete anything without separate authorization.

**Exit evidence:** readback matches the approved change, or a clear unresolved discrepancy. Never mark uncertain writes complete.

### 9. Offer optional email, calendar, and check-ins

Only propose additions tied to the user's deal workflow. Check authorization for each optional service separately. Existing service-specific authorization counts; otherwise ask before connecting. The owner still completes any required private login and consent controls. Resolve the correct sender, recipients, destination, timezone, and event details. Draft first; obtain the authorization required for sending or inviting, then verify the resulting message or event. A CRM update approval does not authorize email or calendar changes.

For recurring check-ins, agree on the purpose, schedule, timezone, channel, and permitted actions. Create a schedule only when supported and explicitly approved; verify its saved state. Otherwise explain that no recurring check-in has been created. Do not create recurring monitoring merely to finish an action already in progress.

**Exit evidence:** authorized optional actions verified, or clearly skipped/deferred without blocking the CRM outcome.

## Checkpoint and resumption

Keep a concise private checkpoint during the interaction, and save it only to a private destination the user has authorized. Suggested fields:

```text
Mode: setup / chat-only / saved skill
Current state:
Verified capabilities and account/workspace:
Completed actions and verification evidence:
Pending user step or approval (exact scope):
Uncertain actions that must be read back before retry:
Next safe action:
```

Do not include secrets. Resume by rechecking relevant state; do not reinstall, reconnect, resend, or rewrite simply because the conversation restarted. Distinguish approved, attempted, and verified actions.

Finish when the first agreed outcome is verified and optional additions are either completed, declined, or explicitly deferred. Summarize what now works, what changed, and anything still blocked. If blocked, name the exact action and target, known reason, current state, and smallest supported next step—without pretending setup succeeded.

## Twenty reference and release tracking

When the selected CRM is Twenty, read [Twenty common operations](references/TWENTY-OPERATIONS.md) before planning record work. Relearn the relevant schemas through the recipient's own connection.

This package's stable ID is `afrog33k/guided-dot-onboarding`. Published versions and file hashes are in the [repository manifest](https://github.com/afrog33k/cornerpost-skills/blob/main/manifest.json). If the optional `skill-release-updates` skill is available, use it when the owner requests update enrollment or a check. Otherwise follow the supported platform route and report that no background checker has been enrolled. Reading this link does not install or update anything.
