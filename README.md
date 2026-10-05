# cursor-slack-scratch

Default landing repository for **Cursor Cloud Agents launched from Slack** (`@Cursor`).

## Why this exists

Slack `@Cursor` requires a repository (not a "REPL"). Pointing the workspace/channel default at a product or docs repo risks accidental PRs and noisy commits on load-bearing surfaces.

This repo is the safe pad:

- Prefer this as the **personal / channel default** for casual `@Cursor` mentions
- For real work, name the target in the prompt (`@Cursor in starshard-ai/architecture-v1 …`) or use `@Cursor settings` / routing rules per channel

## What belongs here

Throwaway experiments, Slack-triggered smoke tests, and scratch PRs. Promote lasting work into the appropriate public product/research repo.

## What does not belong here

Secrets, private hostnames, personal data, or anything that should not be public.

## Active briefs

Public-safe architecture (role names only). Owner go/no-go lives in the OPEN-QS file.

- Singapore execution-plane hub: `docs/SINGAPORE-HUB-BRIEF.md`
- Mesh authorize + Signal checklist: `docs/SINGAPORE-HUB-MESH-CHECKLIST.md`
- Heavy harness MVP: `docs/SINGAPORE-HEAVY-HARNESS.md`
- Owner go/no-go: `docs/SINGAPORE-HUB-OPEN-QS.md`
