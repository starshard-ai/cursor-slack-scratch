# Heavy harness MVP on Singapore (Cursor CLI / Codex / open)

**Status:** Recommendation (Cloud Fable, 2026-09-19). Install only after owner `go` on OPEN-QS Q4 + Q5.
**Owner:** 沈马成. Trigger: Claude Code is banned or blocked on some seats; Singapore should host the heavy coding tools.
**Surface note:** public. Official install URLs only. No API keys, no account emails, no spend figures.

Parent: `SINGAPORE-HUB-BRIEF.md`. Questions: `SINGAPORE-HUB-OPEN-QS.md`.

---

## 0. 综述

**推荐 MVP：先装 Cursor CLI（`agent`），同日把 Codex 登录补齐（给已有 poller 后端），开源 harness 留作厂商挡掉时的后备。** `design`

理由（短）：

1. 这个组织已经住在 Cursor 里（Cloud Agent、Slack `@Cursor`、本 brief）。Claude Code 被挡时，**同家族终端席**摩擦最小。
2. 新加坡 / seoul 的 fleet poller 后端已经标成 `codex`，但 **claims 关闭**；tokyo Codex 未登录。Codex 登录是「执行面工单」的缺口，不是「交互重型编码」的第一选择。
3. 开源 harness（推荐后备：**OpenCode**）在 Cursor **和** Codex 都不可用时才值得付第二套密钥与心智开销。OpenHands 更重（沙箱 / Docker），放到 P1。

不要在共享 Eden VM 上装这些。钥匙与 harness 认证都停在执行面。

---

## 1. When to use which surface

| Job | Surface | Why |
|---|---|---|
| Isolated PR on a cleared public repo (this pad, product docs) | **Cursor Cloud Agent** | No fleet keys; sandbox; reviewable diff. This brief is that path. |
| Interactive / long-running coding **on Singapore** (private worktrees, mesh hops, local daemons) | **Cursor CLI (`agent`)** on Singapore | Same product family; works when Claude Code is blocked; owner already has the seat. |
| Unattended fleet work-packet already shaped for pollers | **Codex** on Singapore / seoul | `executor_backend: codex` is already the label. Needs login + claims `go`. |
| Both Cursor **and** Codex blocked, or owner wants a provider-agnostic TUI | **OpenCode** on Singapore | Official install; bring-your-own provider. Extra spend + extra auth store. |
| Grok conversation, taste, drafts | **Eden seats** (Eva / zhizi-grok / Adam overview) | Still drafter, not Mac/fleet executor. Hub packets, not silent hops. |
| “Make Grok reach the fleet” | **Not a harness question** | Dual-plane ADR + this hub brief. Do not use Cloud workers or CLI as a backdoor onto the Eden VM. |

Cloud Agent **vs** Singapore CLI is not “which model is smarter.” It is **blast radius**:

- Cloud Agent: vendor sandbox, no Singapore hub private key, good default for public ship.
- Singapore CLI / Codex: lives next to the hub key and Signal. Treat every unattended `--force` / yolo flag as fleet-adjacent.

---

## 2. MVP stack (opinionated)

### P0 — install these, in this order, after OPEN-QS

| Order | Tool | Job on this host | Auth (on Singapore only) |
|---|---|---|---|
| 1 | **Cursor CLI** (`agent`) | Interactive + headless coding | `agent login` or seat-local `CURSOR_API_KEY` (never git) |
| 2 | **Codex CLI** | Poller-shaped packets; ChatGPT/Codex login if missing | Official `codex` login on this user — do not copy `~/.codex` from Air |
| 3 | *(defer)* **OpenCode** | Vendor-outage / provider-agnostic TUI | `/connect` or env on this user |

### P1 — only if P0 is tight

| Tool | When |
|---|---|
| **OpenHands** CLI / headless | Need Docker-isolated autonomy, not a daily TUI |
| **Goose** (AAIF) | Recipe / MCP automation beyond coding |
| Aider | Git-native pair loop; thinner than a full agent |

Do **not** install Claude Code on Singapore as the MVP if the reason we are here is that Claude Code is banned/blocked on some seats. Do not run three interactive agents on the same worktree at once.

---

## 3. Install shape (public commands)

Run **on Singapore**, as the hub user. These are vendor-documented entry points as of 2026-09-19. If a vendor page moved, follow the vendor page — do not invent a mirror.

### 3.1 Cursor CLI (first)

Host is Linux **arm64 / aarch64**. Confirm `uname -m` before assuming an x86_64 bundle.

```bash
curl https://cursor.com/install -fsS | bash
# ensure ~/.local/bin is on PATH
agent --version
agent login          # interactive; owner at the seat
# headless later, only after Q5 spend cap:
#   export CURSOR_API_KEY=...   # env or agent auth store — not a file in git
#   agent -p "..." --trust
```

Docs: [cursor.com/docs/cli/headless](https://cursor.com/docs/cli/headless.md), [cursor.com/cli](https://cursor.com/cli).

**Do not** set `--force` / `--yolo` as the unit default. Singapore holds the hub private key.

### 3.2 Codex CLI (same day, login)

Pollers on Singapore / seoul already expect Codex. Tokyo’s current block is `codex auth unavailable: Not logged in`. Do not assume Singapore is logged in just because the binary exists.

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
codex --version
codex login          # this user, this host
```

Fallback documented by upstream: `npm install -g @openai/codex`, or the arm64 musl tarball from GitHub Releases (`codex-aarch64-unknown-linux-musl`). Prefer the official install script.

**Do not** copy Air or Pro `~/.codex` onto Singapore. **Do not** enable fleet claims (`FLEET_CLAIMS_ENABLED`) from this doc — that is OPEN-QS Q7.

### 3.3 OpenCode (P0 only if Q4 picks it; else P1)

```bash
curl -fsSL https://opencode.ai/install | bash
# or: npm install -g opencode-ai
opencode            # then /connect on this host
```

Docs: [opencode.ai/docs](https://opencode.ai/docs). Provider keys stay on Singapore.

### 3.4 Shared host hygiene

- One worktree per harness session. Do not point Cursor CLI and Codex at the same dirty tree.
- Tokens: user environment or the tool’s auth store. Never `docs/`, never Hub memo content, never the Eden VM.
- Updates: `agent update` / vendor script. Do not pin a downloaded binary in this public repo.

---

## 4. Autostart vs harness

| Process | Autostart? | Why |
|---|---|---|
| Grok Bot + headless display | **Yes** (user systemd linger — already the intended path) | Computers jump dies without it |
| Signal user units | **Yes** (already on this host) | Collaborator path |
| Cursor CLI / Codex / OpenCode | **No daemon** for MVP | They are invoked sessions. A 24/7 agent loop on a box that holds the hub key is a new risk accept |
| Fleet poller claims | Off today | Owner Q7; not implied by “install Codex” |

If someone later wants a headless `agent -p` timer: that is a **new** OPEN-Q (unattended loop + spend + Always-allow equivalent). Not in P0.

---

## 5. PCSE / public-safe notes for harness work

| Artifact | Default |
|---|---|
| These four docs | SHIP (cleared org repo, no sovereign set) |
| Code / docs produced **by** a Singapore harness into `github.com/starshard-ai` | SHIP iff the **content** passes PCSE (a–e). The fact that it was typed on Singapore does not make it private, and does not make it public. |
| Mesh IPs, hub private keys, `authorized_keys`, Signal bodies, dollar caps | Named-defer. Do not ride along in a commit message or a “show your work” screenshot |
| New domain / brand / identity | Still owner |
| Cloud Agent PRs from Slack | Prefer this scratch pad for throwaways; name the real repo for product work |

Harness **credentials** are not a PCSE publish question. They are a placement question: execution plane only.

---

## 6. Acceptance (harness P0)

After Q4/Q5 `go`:

- [ ] `agent --version` works on Singapore; `agent login` completed for this user
- [ ] `codex --version` works; `codex` is logged in **or** a dated receipt says “login deferred”
- [ ] OpenCode **not** installed unless Q4 picked it
- [ ] No harness token in git
- [ ] One smoke: a **throwaway** edit in a cleared repo, or a local `agent -p` that does not use `--force` and does not hop the mesh
- [ ] Cloud Agent remains the default for public briefs like this one

Receipt: role + tool + `logged-in|deferred` + `claims=off|on`. No keys.
