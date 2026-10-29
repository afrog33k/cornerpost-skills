# Cornerpost skills

Generic, versioned assistant workflows for guided onboarding, Twenty CRM work and release checking. No customer data, personal setup, credentials or connector configuration is included.

| Skill | Stable package ID | Purpose |
| --- | --- | --- |
| [Guided onboarding](skills/guided-dot-onboarding/SKILL.md) | `afrog33k/guided-dot-onboarding` | Handle supported setup, pause for owner login/consent, verify connections and complete approved deal work. |
| [Skill release updates](skills/skill-release-updates/SKILL.md) | `afrog33k/skill-release-updates` | Verify published versions, stage updates, preserve customization and guide supported activation/rollback. |

The [Twenty operator guide](skills/guided-dot-onboarding/references/TWENTY-OPERATIONS.md) covers common record operations and troubleshooting. Relearn schemas in the recipient's own connection.

## Start with your dot

Give your assistant this repository link and ask:

> Read the guided onboarding skill and help me set up one step at a time. Inspect available tools, open supported setup pages and do the permitted work. Pause for my private login, consent or business decision and verify each step. Then help me complete one useful CRM task. Inspect the supported skill installation route before claiming anything is installed. Offer to enroll version checks using the release-updates skill under my own settings.

The assistant should handle supported actions itself. You choose the account, complete protected sign-in/consent and approve business changes. If installation is unavailable, it can follow the instructions in the current chat and say so.

## Versions and updates

`manifest.json` declares the release version, stable IDs, exact source commit and payload hashes. Resolve the release's full commit and pin the manifest hash in a private installed receipt; `v0.1.0` is a convenient label, not an immutable reference by itself. Read the [update guide](skills/skill-release-updates/references/UPDATE-GUIDE.md), [changelog](CHANGELOG.md), and [blank receipt template](skills/skill-release-updates/assets/installed-receipt.template.json).

Each owner separately enrolls installation and any native scheduled check. Downloading instructions is not installation or runtime activation. This repository creates no schedule, installs nothing in other accounts and contains no custom daemon or executable installer. Actual update ability depends on the receiving platform and its permissions. Local changes are preserved, with the previous verified package retained for rollback.

[Skill authoring](https://learn.chatgpt.com/docs/build-skills), [skill controls](https://learn.chatgpt.com/docs/enterprise/skills), and [scheduled tasks](https://learn.chatgpt.com/docs/automations) describe the relevant product boundaries. Use current supported controls rather than guessing an import or update route.

## Public and private content

Only generic instruction packages, release metadata and empty templates belong here. Keep owner preferences, installation handles, scheduler references, customer information, private links and secrets in authorized private storage. A new skill version grants no access to email, calendar, CRM or computer use.

The original [public onboarding Gist](https://gist.github.com/afrog33k/5f312bedd13774c18220b746e510fc2b) is retained unchanged. `SOURCE-PROVENANCE.json` records its verified baseline.
