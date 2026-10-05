# ADR: One GitHub personal account for assistants and public brand

**Status:** Proposed standing (Cloud Fable, 2026-09-18)  
**Owner:** 沈马成 (Starshard / Eden)  
**Decides:** which of the two personal GitHub identities to **keep**, and the P0 path to stop dual-login confusion  
**Does not decide:** Cursor product settings beyond GitHub OAuth reconnect; org product strategy inside `starshard-ai`; custom-domain DNS  
**Surface note:** this file is public. Usernames already on public GitHub only. No tokens, private hostnames, Hub ids, or owner-only emails invented here. Copy emails from GitHub **Settings → Emails** on the owner’s own machine.

---

## 1. Decision (one path)

**Keep Account B — `MachengShen`. Retire Account A — `randomguy-2450` after transfers.**

| Identity | Public login (verified 2026-09-18) | Keep? |
|---|---|---|
| **B — named / MIT-alumni brand** | [`MachengShen`](https://github.com/MachengShen) (user id `47833670`, created 2019-02-20). **39** public repos, **11** followers. Owns [`MachengShen/MachengShen.github.io`](https://github.com/MachengShen/MachengShen.github.io). Live user-Pages host [`https://machengshen.github.io/`](https://machengshen.github.io/) (HTTP 200 this turn; contact Gmail already printed on that page). | **KEEP** |
| **A — Gmail / “random guy”** | [`randomguy-2450`](https://github.com/randomguy-2450) (user id `60761661`, created 2020-02-06, display name `anonymous_author`). **1** public repo: [`randomguy-2450/implicit_ensemble_training`](https://github.com/randomguy-2450/implicit_ensemble_training). **0** followers. This is the identity Cursor SCM currently lists alongside org repo `starshard-ai/cursor-slack-scratch`. | **RETIRE** (transfer, then delete) |

**How (GitHub has no merge button).** Official path: [transfer repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository) from A → B or `starshard-ai` → add A’s commit emails on B → [delete A](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-your-personal-account/deleting-your-personal-account). See [Merging multiple personal accounts](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-your-personal-account/merging-multiple-personal-accounts).

**Cursor / assistants:** one OAuth identity going forward = **`MachengShen`**. Pay a **single** owner-machine Dashboard reconnect. Do **not** invent a second GitHub login on the shared Grok VM. Do **not** keep dual-SSH aliases as the steady state.

**Org:** keep operating `starshard-ai` as today (Cursor GitHub App already installed, all-repos, per prior Mac receipt). Before deleting A, the owner must confirm **B is an org Owner**. Which personal account is the org owner / billing contact is **UNKNOWN** from the public API (members list is empty to this token).

---

## 2. Why B, not A (vs global context)

Same-day constraints this ADR must satisfy:

1. Cursor is already wired to **A + `starshard-ai`**.
2. Name-branded public Pages live on **B** (`machengshen.github.io/spine/`, `/pipeline/`, `/fable-ngs3077/`, and the user site).
3. Owner hates VM browser logins.
4. Same-day fleet reachability ADR: **one** assistant identity; **no** dual-login gymnastics on the shared Grok VM; Grok drafts only; no fleet keys on that box.

**A is cheaper for Cursor this afternoon. B is cheaper forever.** Switching Cursor is one Dashboard OAuth on the owner’s laptop/phone. Moving the public brand is not.

Load-bearing GitHub fact ([transfer docs](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository)):

> If the transferred repository contains a GitHub Pages site, then links to the Git repository on the Web and through Git activity are redirected. **However, we don't redirect GitHub Pages associated with the repository.**

User-site URLs are bound to the login. `https://machengshen.github.io/` exists only while the username `MachengShen` exists. Transferring `MachengShen.github.io` to A would change the published host to `randomguy-2450.github.io` (or an org host) **without** a github.io redirect. Renaming B away from `MachengShen` has the same Pages break. Citations, `llms.txt`, and already-shipped pedagogic URLs would rot.

Transfer **volume** also favors B:

- A → B (or org): **1** verified public repo, plus any **UNKNOWN** private repos on A.
- B → A: **39** public repos, including the Pages user site, plus the live URL break above.

`MachengShen` already has `ImplicitEnsembleTraining` and `Implicit_ensemble_training`. A same-name transfer of `implicit_ensemble_training` onto B will fail. Transfer it to **`starshard-ai/implicit_ensemble_training`** (name free on the org as of this turn) or rename during transfer.

Eva same-day interim (“unify assistants on the Cursor-connected account; move name repos or SSH-only on Air”) optimized for **zero Cursor reconnect**. That is the wrong cost function once Pages non-redirect and brand are in the weights. This ADR **supersedes** that interim the same way the fleet reachability ADR superseded Air-as-jump: keep the constraint (no Grok-VM GitHub login; one OAuth identity), replace the identity pick.

---

## 3. Rejected paths

| Reject | Why |
|---|---|
| **Keep A (`randomguy-2450`) as the surviving personal account** | Preserves today’s Cursor wiring and destroys (or dual-lives) the public name. Pages do not redirect. 39-repo move vs 1-repo move. Anonymous login is the wrong long-term assistant identity. |
| **Keep dual forever + SSH host aliases** (`github.com-work` / `github.com-brand`) | Solves *Mac git CLI only*. Does not give Cloud Agents / Slack `@Cursor` a single GitHub App identity. Reintroduces default-login confusion. Dual keys on a shared Grok VM are already banned by the fleet reachability ADR. Not clearly better than transfer. |
| **Username swap** (rename B, then rename A to `MachengShen`) | GitHub Pages follow the *current* username and do not keep the old github.io host. High-risk cooldown window. Still needs Cursor reconnect. Do not do this to “save” A. |
| **Leave Pages on B and point assistants at A** | Permanent dual. Every new App (Cursor, Claude, Actions) becomes another “which account?” prompt. This is the bug the owner asked to kill. |
| **Grok-VM or Cloud Agent browser login to the other account** | Owner-stated hate; fleet ADR forbids dual-login gymnastics on the shared conversation VM. All GitHub account clicks stay on the owner’s own machine. |
| **Invent emails / org ownership** | Not verified this turn. Owner copies from GitHub UI. Agents must not guess. |

---

## 4. Unknowns (do not fill by guess)

Mark each **owner-confirmed** before step 8 (delete A).

| # | Unknown | Where the owner looks |
|---|---|---|
| U1 | **Private repos, gists, packages, Codespaces / Actions secrets** on A or B | Each account → profile Repositories (including private) + Settings → Codespaces / Secrets / Packages |
| U2 | **Which personal account is `starshard-ai` Owner** and who pays billing | Logged-in Owner → `https://github.com/orgs/starshard-ai/people` (role = Owner) and org Settings → Billing. Public members API returned `[]` this turn. Prior Mac work used `gh` **as `MachengShen`** and had admin; that is **not** proof B is the sole owner. |
| U3 | **Verified emails on each GitHub account** | Each account → Settings → Emails. Do not assume the public Pages Gmail, the Cursor Cloud owning-user email, or any MIT alumni address is attached to a given login. |
| U4 | **Whether the Cursor GitHub App is installed on `MachengShen` personal repos** (org install is already green) | Cursor Dashboard → Integrations / GitHub. GitHub → Settings → Applications → Installed GitHub Apps, on **B**. |
| U5 | **SSH keys, deploy keys, PATs, authorized OAuth Apps** on A | A → Settings → SSH and GPG keys / Developer settings. Revoke after B is the only login assistants use. |
| U6 | **2FA recovery** for B | B must have working 2FA *before* A is deleted. Recovery codes stay in the owner vault, never chat/Hub. |

---

## 5. Risks

| Risk | What actually happens | Mitigation |
|---|---|---|
| **Pages URL** | Not moved in this plan. Risk is *accidentally* transferring or renaming `MachengShen.github.io` / `MachengShen`. | Never transfer the user-site repo. Never rename B. HTTP-check `/`, `/spine/`, `/pipeline/` after every owner session. |
| **Org lockout** | If A is the **sole** `starshard-ai` Owner and A is deleted, the org can become inaccessible. | Step 3: make B Owner and confirm B can open org Settings **before** any delete. Billing contact updated if it was A. |
| **Stars / followers / achievements on A** | User-level followers, achievements, and profile stars **do not** merge. A has 0 public followers; loss is small. Repo stars **do** travel with a transferred repo. | Accept. Do not keep A alive for cosmetics. |
| **Commit graph / noreply** | Commits stay in git. Contribution graph on B only counts commits whose author email is on B. `users.noreply.github.com` addresses are per-account and do not move. | Step 2: add every address listed on A, including GitHub noreply if A used it. Deterministic noreply *if* A used the current default: `60761661+randomguy-2450@users.noreply.github.com`. Confirm on A’s Emails page; do not invent other addresses. |
| **Cursor reconnect gap** | After disconnecting A, Cloud Agents / Slack `@Cursor` cannot push until B is connected and the org App is still installed. | One sitting, owner machine. Do not disconnect A until B’s App install + org install are confirmed. Scratch default stays `starshard-ai/cursor-slack-scratch`. |
| **Transfer invite expiry** | Personal→personal transfer must be **accepted within one day** or it expires. | Prefer transfer A → **org** (no email accept) when the owner is org Owner on the same login session. If transferring to B as a user, accept immediately on B. |
| **Name collision** | `MachengShen/implicit_ensemble_training` cannot be created; B already has near-duplicate research names. | Transfer to `starshard-ai/implicit_ensemble_training` or rename (e.g. `implicit_ensemble_training-2021`). |
| **Redirect footgun** | Creating a **new** repo at `randomguy-2450/implicit_ensemble_training` after transfer **permanently deletes** GitHub’s git redirect. | Do not recreate A’s old repo paths. Delete A instead. |
| **Account delete is not undoable** | Current GitHub docs: once the personal account is deleted, GitHub cannot restore the content. | Delete A only after the §7 gate. Until then A is the rollback valve. |

---

## 6. P0 checklist (execute in order — do not re-decide)

Legend: **Owner** = clicks on the owner’s own laptop/phone (never Grok VM). **Mac** = Codex / Cursor frontstage on Air. **Agent** = Cloud Fable / Slack `@Cursor` after reconnect.

### Inventory and keep-account prep

1. **Owner — inventory A.** Sign in as `randomguy-2450` once, on the owner machine. Export: private repo list, gists, packages, org role on `starshard-ai`, Settings → Emails (every address), SSH keys, PATs, installed Apps. Screenshot or vault note. Sign out.
2. **Owner — add A’s emails on B.** Sign in as `MachengShen` → Settings → Emails → add every address from step 1 (including A’s GitHub noreply if present) → verify. Do not remove B’s existing addresses.
3. **Owner — org Owner on B (hard gate).** As a current `starshard-ai` Owner: People → select `MachengShen` → Change role → **Owner** if not already. Confirm B can open `https://github.com/organizations/starshard-ai/settings`. If A is billing owner, update payment on B ([transfer organization ownership](https://docs.github.com/en/organizations/managing-organization-settings/transferring-organization-ownership)). **If this step is blocked, stop. Do not transfer or delete.**
4. **Owner — 2FA + recovery on B.** Confirm 2FA works. Recovery codes in the owner vault only.

### Move A’s code (transfer, do not dual-SSH)

5. **Owner — transfer A’s public repo.** Signed in as A: `randomguy-2450/implicit_ensemble_training` → Settings → Danger Zone → Transfer → new owner **`starshard-ai`** (preferred) or **`MachengShen` with a new name**. Type the repo name to confirm. If the destination is a personal account, accept on B the same day.
6. **Owner — transfer every private A repo from step 1.** Same Danger Zone path. Destination: `starshard-ai` for product/research; `MachengShen` for personal-only. No leftover repos on A except empty profile.
7. **Mac — remotes.** On Air, for each transferred clone: `git remote set-url origin NEW_URL`. `gh auth status` must show **`MachengShen` only**. Do not add `Host github.com-randomguy` SSH aliases. Do not copy any key onto the Grok VM.

### One Cursor OAuth identity (owner machine, one sitting)

8. **Owner — Cursor GitHub = B.** Cursor Dashboard → Integrations / GitHub:
   1. Confirm **Cursor GitHub App** is installed on **`starshard-ai`** (All repositories; already green as of 2026-09-16 Mac receipt — re-check).
   2. Install / configure the same App on **`MachengShen`** personal account (all repos, or at least Pages + any personal fallback).
   3. Disconnect the `randomguy-2450` connection if it is still the active SCM identity.
   4. Connect / reconnect as **`MachengShen`**.
   5. Slack `#` default / `@Cursor settings` → keep `starshard-ai/cursor-slack-scratch`.
9. **Owner — do not open github.com in a Grok-VM or Cloud Agent browser** to “finish” this. If a Cloud Agent cannot see a repo, fix Dashboard scopes (step 8), not a box login.
10. **Agent — smoke.** After step 8, one Slack or Cloud Agent turn: list visible remotes / open this repo. Success = `starshard-ai/cursor-slack-scratch` + `MachengShen` personal repos visible; `randomguy-2450/…` gone or redirect-only.

### Prove Pages and org, then delete A

11. **Owner or Agent — HTTP check (must all be 200):**
    - `https://machengshen.github.io/`
    - `https://machengshen.github.io/spine/`
    - `https://machengshen.github.io/pipeline/`
    - `https://github.com/starshard-ai`
    - transferred repo URL (`https://github.com/starshard-ai/implicit_ensemble_training` or the renamed B URL)
12. **Owner — revoke A’s leftover credentials.** Still signed in as A: delete PATs, SSH keys, OAuth Apps except GitHub itself. Sign out everywhere.
13. **Owner — delete A (Danger Zone, last).** Only after steps 3, 5–8, and 11 pass. `randomguy-2450` → Settings → Account → Delete your account. GitHub cannot restore a deleted personal account. Type the confirmations. Do **not** recreate the old `randomguy-2450/<repo>` paths.

---

## 7. Gate before delete (copy)

Stop if any box is unchecked.

- [ ] B (`MachengShen`) is a `starshard-ai` **Owner** and can open org Settings.
- [ ] Org billing is not stranded on A.
- [ ] Every A repo (public + private) is transferred and opens under B or `starshard-ai`.
- [ ] A’s commit emails (and noreply if used) are **verified** on B.
- [ ] Cursor Dashboard GitHub identity is **`MachengShen`**; Slack default still `starshard-ai/cursor-slack-scratch`.
- [ ] Agent smoke (step 10) succeeded without a VM GitHub login.
- [ ] Pages URLs in step 11 are HTTP 200.
- [ ] Mac `gh` is `MachengShen` only; no dual-SSH config added.
- [ ] Owner has 2FA recovery for B in the vault.

---

## 8. Rollback (only while A still exists)

| Failure | Rollback |
|---|---|
| Wrong transfer destination | Transfer **back** to A (A must still exist). Do not create a replacement repo at the old path. |
| Transfer invite expired | Re-issue from A. Prefer A → org to avoid the 1-day accept window. |
| Cursor reconnect fails / Slack picker empty | On the owner machine, reconnect Cursor to A **temporarily**. Do not delete A. Fix B App install (step 8) and retry. |
| Org Settings inaccessible on B | A still owns the org — stay on A for org admin; do not delete A; repeat step 3. |
| Pages 404 | This plan never moved Pages. If 404, B’s Pages settings or a bad rename/transfer of `MachengShen.github.io` is the cause — revert that change on B; A cannot fix github.io. |
| Mid-delete panic | If A is **already deleted**, GitHub cannot restore the user. Recover via transferred repos on B/org and commit emails. Untransferred A-only assets are gone. |

There is no rollback that “merges the accounts after all.” Dual-SSH is not the rollback; it is a rejected steady state.

---

## 9. Execute-next (who does what)

**Owner (one browser session on your machine, not a VM):**

1. Steps 1–6, 8, 12–13 in §6.
2. Do not approve any agent proposal to log into GitHub inside a Grok/Cursor VM.
3. Do not keep A “just in case” after the §7 gate — that is dual forever.

**Mac Codex / Cursor frontstage (Air):**

1. Step 7 remotes + `gh` as `MachengShen` only.
2. Claim leftover private-repo hunt if step 1 listed any (no secrets in Hub).

**Eva / Adam / zhizi-grok / Cloud Agents:**

1. After step 8: treat `MachengShen` + `starshard-ai` as the only GitHub identity.
2. Draft work-packets for Mac/owner clicks. Do not SSH. Do not open github.com login on the Grok VM.
3. Anti-signals: “just add another SSH alias”; “keep both so Pages stay”; inventing an email or org role; recreating `randomguy-2450/<repo>`.

---

## 10. Supersedes

Eva interim (same day): “unify assistants on the Cursor-connected account (`randomguy-2450`); transfer name repos or SSH-only on Air; avoid box-browser GitHub login.”

**Keep:** one assistant OAuth identity; no GitHub login on the shared Grok VM; transfer over dual-forever.  
**Replace:** “the identity we keep is whichever Cursor already sees.”  
**Use instead:** keep **`MachengShen`**; one owner-machine Cursor reconnect; transfer A’s small repo set into `starshard-ai` / B; delete A after the §7 gate.

Cross-read (same day): fleet reachability ADR on `starshard-ai/cursor-slack-scratch` branch `cursor/fleet-reachability-adr-e4c3` (`docs/FLEET-REACHABILITY-ADR.md`) — dual-plane, no fleet keys on the Grok VM. This file is the GitHub-identity half of that “one principal” rule.
