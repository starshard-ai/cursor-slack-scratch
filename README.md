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

## Architecture briefs (public-safe)

- `docs/NO-TOKEN-FEDERATION-BRIEF.md` — no-token, no-chain collaboration network that still behaves like a durable DAO-style org, mapped onto the dual-plane Hub + work-packet stack. Read §0 (Chinese synthesis) first.
- `docs/NO-TOKEN-FEDERATION-OUTREACH-SLICES.md` — the only externally sayable conclusions from that brief, each with a claim type and a "sayable as" level.
- `docs/NO-TOKEN-FEDERATION-OPEN-QS.md` — seven owner go/no-go questions. Silent skip = no-go.
