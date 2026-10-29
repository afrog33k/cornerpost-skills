# Enroll and update versioned skills

## What this distribution does

The repository publishes instruction packages and release metadata. It does not install a skill, grant a connector permission, enroll a schedule, or change another owner's dot. Real installed receipts and owner preferences stay in authorized private storage; the public template is blank.

Stable IDs are `afrog33k/guided-dot-onboarding` and `afrog33k/skill-release-updates`. Keep these IDs unchanged if display names change. Version `0.1.0` is the first release baseline; there is no earlier versioned release to roll back to. Preserve this baseline for later rollback.

## Verify a release

The current discovery location is `https://github.com/afrog33k/cornerpost-skills/blob/main/manifest.json`. A mutable branch is only a discovery pointer. Resolve its full Git commit, fetch that commit's manifest, and pin that revision and the manifest's SHA-256 in the private receipt. Verify the configured publisher account ID `712518` and record the actual repository ID during enrollment. Do not let a manifest redefine this trust configuration.

The manifest pins a prior source commit and the path, byte length and SHA-256 of every payload file. The release commit adds the manifest and checksum list afterward, avoiding a manifest that contains its own commit/hash. A release tag is a human label and can move; the full commit and hashes identify the bytes. Hashes check integrity, not permission or independent publisher authenticity. `SHA256SUMS` covers the payload and manifest without hashing itself. Release archive checksums are published separately.

For each enrolled ID, compare version and payload hashes with the receipt. The same version with changed content is a conflict. An older version is not an update unless rollback is explicitly requested. Reject absolute paths, parent traversal, files outside the listed package, unexpected publishers or repository changes. Fetch only listed files; do not execute fetched scripts. This release contains no executable updater.

## Install in a supported surface

[OpenAI's skill authoring documentation](https://learn.chatgpt.com/docs/build-skills) distinguishes standalone skills from plugin distribution. This repository supplies standalone packages, not an installed plugin. [Skill controls](https://learn.chatgpt.com/docs/enterprise/skills) distinguishes workspace, filesystem and plugin lifecycles; moving instructions transfers no service access.

In Codex environments with the bundled `skill-installer`, ask it to install the selected `skills/<skill-name>` path from this repository using the verified full source commit as `--ref`. Its documented helper supports GitHub paths and refs and aborts when the destination already exists. It is an installation route, not proof that arbitrary existing skills can be updated. It reports availability on the next turn. The helper is a platform-supplied tool; do not download an installer script from this repository.

For ChatGPT workspace Skills, use the current account's supported skill creation/import/update controls if present; verify the installed item and resource support. Do not invent a GitHub import button or assume a standalone filesystem skill is active on web/mobile or a dot. When no supported save/import route exists, the assistant can read the selected instructions in the current chat and label that mode chat-only. No installation has happened.

Before enrollment, resolve the actual installation identity and surface, current upstream version/hashes, any local modifications and the permitted activation policy. Populate [the blank installed-receipt template](../assets/installed-receipt.template.json) privately with the real values. A receipt with null installation or active-release fields is not proof of installation.

## Periodic checks and pulling candidates

Use the owner's available native scheduled-task mechanism. [Scheduled tasks](https://learn.chatgpt.com/docs/automations) documents desktop and web execution boundaries: local tasks need their computer/app available; web tasks cannot directly update a local folder. A scheduler's existence does not prove that its execution environment can fetch releases, preserve a private receipt or update the intended installation.

Agree on cadence (daily is a reasonable starting option), the owner's timezone, report destination and whether compatible changes may be activated or only staged. Verify capability and access before saving the schedule. Test the prompt in that environment, then verify the saved schedule and first run. Do not broaden network/filesystem/service permissions merely to test. A foreground check on next use is a fallback, not a background schedule.

Suggested task action, with cadence configured separately:

> Check the enrolled skill IDs in my private installed receipt against the configured afrog33k/cornerpost-skills release manifest. Resolve and pin the manifest commit; verify source, versions, file hashes and compatibility. Download an available candidate only into authorized staging. Preserve local edits and the previous verified package. Activate only through supported controls within my enrolled policy; otherwise report the proposed update or exact blocker. Read back activation before changing the active receipt. Report material updates or failures; do not claim an install from a download. Do not run downloaded scripts or access other accounts.

If the check needs an unavailable installer, private state or target surface, keep the existing release active and report that limit. Publication or a public prompt cannot enroll any other owner.

## Apply without overwriting local work

Record each installed upstream file's hash at installation. Before replacement, compare current bytes against those hashes. Differences are local modifications: keep the current copy and stage the candidate. Use a separate private overlay only if that platform supports it; otherwise reconcile explicitly. Keep personal preferences, CRM records, connection state and secrets outside the upstream package.

Review permission, connector, platform and executable changes against the owner's enrolled policy. A version bump grants no new scope. Already-authorized compatible updates need no duplicate conversational approval beyond platform controls. Hold expanded or uncertain scope for the required decision. Use a supported update route; do not remove an existing installation to force the initial installer to run.

## Receipts, failures and rollback

Record states separately: checked, downloaded/staged, activated and blocked/failed. Pin manifest commit/hash, source commit, version, file hashes, installation handle and verification method. If the platform hides installed file bytes, record the available verification and its limit. Never fabricate exact hashes or advance the active version after an ambiguous result.

Before activation retain the previous verified package bytes and receipt in authorized private storage; a URL alone is insufficient. Rollback restores that selected workflow through the supported platform route while preserving local customization. It does not undo CRM writes, messages or calendar events. Keep released source commits, checksum files and release assets available; do not retag or replace a version's bytes.
