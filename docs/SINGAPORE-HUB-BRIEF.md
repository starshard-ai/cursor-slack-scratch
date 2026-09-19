# Brief: Singapore as execution-plane hub (Computers jump + fleet SSH)

**Status:** Architecture brief (Cloud Fable, 2026-09-19). Proposed standing; owner go/no-go in `SINGAPORE-HUB-OPEN-QS.md`.
**Owner:** 沈马成 / Macheng (Starshard / Eden / fleet Adam · zhizi-grok).
**Decides:** how the AWS Singapore host sits in the dual-plane map — Grok Bot Computers jump + fleet SSH hub + heavy-harness seat — and which keys may live where.
**Does not decide:** which pubkey line is appended on which host (checklist), which coding harness to install first (harness note + OPEN-QS), any spend number.
**Surface note:** this file is public. Role names only. No private hosts, mesh IPs, key material, Hub ids, or machine ids. Operational receipts live on Memory Hub.

**Parent standing:** Fleet reachability ADR (2026-09-18; sibling PR on this repo, Hub `standing`) — dual-plane; **no** fleet private keys or mesh client on the **shared Eden / Grok conversation VM**. This brief does **not** repeal that ADR. Singapore is the separate execution-plane host that ADR left as P1.

**Claim types**

| Tag | Meaning |
|---|---|
| `operational` | Verified this turn (owner brief, fleet receipts, or Hub standing). |
| `design` | Proposed here. Owner go/no-go before treating as standing. |
| `OPEN-Q` | Unknown. Listed in `SINGAPORE-HUB-OPEN-QS.md`. |

---

## 0. 综述（owner 先读）

**一句话：新加坡 AWS 是执行面常开席，不是对话面。Eden 共享 Grok 云机仍然不装舰队私钥、不作组网跳板。** `operational`（双平面 09-18）+ `design`（新加坡 = 那台被允许的执行面主机）

今天已经成立的事实（2026-09-19，owner + fleet 回执）：

1. Grok Bot Linux **0.56.1** 已在新加坡登录；该机已是 Eden **Computer**。Eden 对本机的 local-exec **不再依赖** Air 在线。`operational`
2. 意图中的保活路径：用户 systemd linger（grok-bot + 无头显示栈）。Air 休眠不应再挡住「Eden → 新加坡 Computer」。`operational`（回执：unit enabled + linger）
3. 组网层能看见：tokyo/rescue、seoul、bangkok-mini、Air；Pro 离线。`operational`
4. 从新加坡用本机枢纽公钥做 `BatchMode` SSH：**只有 tokyo/rescue 成功**。seoul / bangkok-mini / 新加坡自环 = 公钥未授权；Pro = 超时。`operational`
5. 共享 Eden/Grok VM 的红线不变：不持舰队私钥，不以 Tailscale 作主跳板。新加坡是另一台座位。`operational`

owner 要这台机器同时做三件事：

| 角色 | 给谁用 | 依赖 |
|---|---|---|
| **Computers 跳板** | Eden / Grok Bot → 本机 shell（需 grok-bot 活着） | Grok Bot 登录 + Computer 注册 + 保活 |
| **舰队 SSH 枢纽** | 已授权的执行面主体（owner / Mac / Adam / poller）→ 其他舰队机 | 枢纽**公钥**写入目标 `authorized_keys` + 组网 |
| **重型编码席** | Cursor CLI / Codex / 开源 harness（因部分座位禁/挡 Claude Code） | 见 `SINGAPORE-HEAVY-HARNESS.md` |

这三件事可以独立坏。Computers 死了，SSH 枢纽仍可从 Air/tokyo 修；组网死了，Eden 仍可能打到新加坡本机；钥匙铺错了，前两件事都变成舰队 root。

---

## 1. Dual-plane map (bright lines)

```
                    CONTEXT PLANE                         EXECUTION / FLEET PLANE
               (conversation, taste, draft)              (shell, mesh, keys, harness)
 ┌─────────────────────────────────────┐     ┌──────────────────────────────────────────┐
 │ Shared Eden / Grok VM               │     │ Singapore hub (always-on coding seat)    │
 │  - Memory Hub read / draft packets  │     │  - Grok Bot Computer (local-exec target) │
 │  - NO fleet private keys            │     │  - Fleet SSH hub identity (private key)  │
 │  - NO Tailscale as primary jump     │     │  - Heavy harnesses (CLI / Codex / open)  │
 │  - Computers: only if owner-gated   │────▶│  - Signal / poller home (existing)       │
 └─────────────────────────────────────┘     └───────────────┬──────────────────────────┘
         │ Hub work-packets                   pubkey-only    │
         ▼                                   authorization   ▼
   Mac frontstage / fleet pollers              tokyo/rescue · seoul · bangkok-mini · (Pro later)
   Air = owner laptop, intermittent;           Air is NOT the availability story
   NOT unattended jump
```

| Plane | Host (role) | May hold | Must not hold |
|---|---|---|---|
| **Context** | Shared Eden / Grok VM | Hub tokens already scoped to conversation; drafts | Fleet SSH **private** keys; mesh as primary jump; copy of Air `~/.ssh`; raw T1 / people-registry |
| **Execution** | Singapore hub | One dedicated hub SSH **private** key; Grok Bot login for *this* Computer; harness auth for *this* seat | Air’s full keyring; other seats’ vendor tokens “just in case”; conversation-VM copies |
| **Execution peers** | tokyo/rescue, seoul, bangkok-mini, Pro | Their own host keys + **Singapore hub public key** in `authorized_keys` (once owner says go) | Singapore’s **private** key; Eden VM keys |
| **Owner laptop** | Air | Owner keys; taste; intermittent Computer | Unattended jump duty for Grok seats |

`operational` for the context-plane forbids (ADR 09-18). `design` for naming Singapore as the execution-plane hub.

**What changed vs 09-18:** the ADR rejected “Air as unattended jump” and “keys on the conversation VM,” and left a **separate** bastion as P1. Singapore is that host. It is **not** a license to put the same keys on the Eden VM “now that we have a hub.”

**What did not change:** Grok seats on the shared box remain **front-end + drafter** (09-17 tier). Eden local-exec onto Singapore is owner-gated Computers, not a second dispatcher. Cursor Cloud Agents stay orthogonal (fine for public PRs; not the Grok reachability story).

---

## 2. Two jumps, two failure domains

### 2.1 Computers jump (Eden → Singapore)

- **Path:** Grok Bot app logged in on Singapore + Computers enabled → Eden can local-exec **on that machine only**. `operational`
- **Not implied:** every Tailscale node becomes a Computer. Only machines with Grok Bot logged in + Computers on. `operational`
- **Availability:** Air sleep must not block this path. Availability = `grok-bot` + display stack + linger, not Air. `operational` (intent) / `OPEN-Q` (reboot smoke still owner-side)

### 2.2 Fleet SSH hub (Singapore → peers)

- **Path:** Singapore holds a hub **private** key; each peer that should be reachable has **only the public half** in that user’s `authorized_keys`. Mesh provides the underlay. `design` (shape) + `operational` (tokyo already accepts; others do not)
- **Seeing ≠ entering:** a node visible on the mesh can still return `Permission denied (publickey)`. That is missing authorization, not a dead host. `operational` (seoul, bangkok-mini, Singapore-loop today)
- **Singapore-loop** (SSH to self) failing is **not** a hub blocker. Self-auth is optional and is not required for Computers or for hopping to peers. `design`

### 2.3 Who may use the hub key

Intended principals: owner, Mac frontstage, Adam (zhizi-grok fleet body), existing fleet pollers. `design`

Not intended: unattended Grok seats on the **shared Eden VM** using Singapore as a silent jump the way Air was rejected. If local-exec on Singapore is set to **Always allow**, every confused-deputy turn on Eden inherits **always-on fleet root**. That is worse than the Air-jump reject (Air slept). `design`

---

## 3. What keys belong where

**One hub identity. Public half travels. Private half stays on Singapore.**

| Object | Where it lives | How it moves | Never |
|---|---|---|---|
| Singapore hub **private** key | Singapore `~/.ssh/` only (dedicated file preferred — OPEN-Q) | Does not move | Eden VM, git, Hub memo body, chat, screenshots |
| Singapore hub **public** key | Printed on Singapore; appended on peers by a principal that already has login | One line per target user | Pasted into this repo; dumped as a “key inventory” with private halves |
| Peer host keys / `authorized_keys` | On that peer | Local edit or existing admin path | Committed; published; used as a phone-home list |
| Air owner keys | Air | Stay on Air | Copied wholesale onto Singapore or Eden |
| Harness tokens (Cursor / Codex / open) | Singapore user env or that tool’s auth store | Official login on **this** seat | Shared by copying files onto the conversation VM |
| Mesh auth | Already on execution-plane hosts | Rotate via vendor console, not via public docs | New DIY tunnels originating on the Eden VM |

**Do not** “just copy Air `~/.ssh` so we’re not blocked.” That recreates the 09-18 reject with a larger blast radius (Singapore is always on). `operational` (ADR reject) 

**Do not** invent or publish credentials in this brief. If a command needs a key, it prints the **public** key on the hub and stops. See `SINGAPORE-HUB-MESH-CHECKLIST.md`.

---

## 4. Failure modes

### F1 — `grok-bot` / headless display dies

| | |
|---|---|
| **Symptom** | Eden Computers list shows Singapore offline or local-exec hangs. |
| **Still works** | Mesh + SSH hub (if keys are in place); Signal user units; someone who already has SSH can restart the unit. |
| **Does not work** | Eden → Singapore Computer without another jump. |
| **Mitigation** | User systemd linger + restart; reboot smoke (`OPEN-Q`); treat Computers liveness as *one* health signal, not the only one. |
| **Anti-signal** | “Air is back, use Air as jump until grok-bot is up” becoming the default again. |

### F2 — Mesh down (client, ACL, expiry, relay)

| | |
|---|---|
| **Symptom** | `BatchMode` SSH from Singapore to peers times out or cannot resolve. Tokyo-looking nodes disappear. |
| **Still works** | Eden → Singapore Computer (Grok Bot path ≠ mesh). Cloud-console / existing owner break-glass on the execution plane. |
| **Does not work** | Hub hops to seoul / tokyo / bangkok-mini / Pro. |
| **Mitigation** | Do not invent a reverse tunnel from the Eden VM. Do not put mesh client on the conversation VM to “save the day.” |
| **Anti-signal** | Publishing underlay IPs into this repo as a fallback list. |

### F3 — Key sprawl

| | |
|---|---|
| **Symptom** | Same private key on two planes; Air keyring cloned to Singapore; hub private key in chat/git; one god-key authorized everywhere with no inventory. |
| **Blast** | One injected turn or one laptop loss = fleet root. Singapore makes this **always-on**. |
| **Mitigation** | Dedicated hub identity; pubkey-only distribution; written list of *roles* that have the pubkey (not the key itself); rotate if the private half ever left Singapore. |
| **Anti-signal** | Any proposal that starts with “copy the keys so we’re not blocked.” |

### F4 — Confused deputy (Computers Always-allow)

| | |
|---|---|
| **Symptom** | A Grok seat on the shared box runs a hop through Singapore without a per-command owner gate. |
| **Blast** | Same as Air-jump, but the jump no longer sleeps. |
| **Mitigation** | Grok Bot → Execution on Local Computer → **Always require approval** or **Never**. Hub work-packets for unattended fleet work. |
| **Anti-signal** | “Singapore is ours, set Always allow so we can move.” |

### F5 — Signal receive stale on Singapore

| | |
|---|---|
| **Symptom** | Hub delivery-only alarms: no receive envelope for N minutes. Recurs. |
| **Still works** | Memory Hub; Computers; SSH. Collaborator send may still be gated. |
| **Mitigation** | Checklist health (whoami + freshness), no message-body dumps, no tokens in docs. Do not page the owner with raw logs. |
| **Anti-signal** | Pasting Signal link payloads or device lists into a public PR. |

### F6 — Pro / Hangzhou offline

| | |
|---|---|
| **Symptom** | Hub → Pro times out. Mesh may still list the node as offline. |
| **Mitigation** | **Do not block hub v0 on Pro.** Defer (`OPEN-Q`). Bangkok-mini password / sudo deadlock is a separate owner item, not a Singapore-hub blocker. |

---

## 5. PCSE / public-safe

These four files are meant to **SHIP** on the cleared surface `github.com/starshard-ai` (this scratch pad):

- (a) role names only — no private persons / family / correlatable home detail
- (b) no financial figures
- (c) no new public identity
- (d) existing org repo
- (e) revertible

**Still named-defer if someone later adds:** mesh IPs, private keys, `authorized_keys` dumps, machine ids, Signal device lists, dollar caps, or a promise in the owner’s voice.

PCSE gates *publish content*, not *credential placement*. Credential placement is this brief + the 09-18 ADR. Do not treat a green PCSE checklist as permission to put keys on the Eden VM.

---

## 6. Phased rollout (design)

### P0 — enough to operate this week

1. Keep dual-plane: Eden VM stays clean. `operational`
2. Keep grok-bot logged in + linger. Owner-hand: local-exec **Always require approval** or **Never**. `design`
3. Authorize Singapore hub **pubkey** onto seoul + bangkok-mini (tokyo already done). Pro deferred unless OPEN-Q says include. See checklist. `OPEN-Q`
4. Verify Signal path freshness without dumping bodies. `OPEN-Q`
5. Install **one** interactive harness on Singapore (recommendation in harness note). `OPEN-Q`

### P1 — after P0 works

- Reboot smoke: grok-bot comes back without a human VNC.
- Optional dedicated hub key if P0 used a generic `id_ed25519`.
- Fleet claims on Singapore/Seoul only if owner wants poller execution (`OPEN-Q`).
- Open harness as vendor-outage fallback, not a second default.
- Pro pubkey when that host is actually reachable.

### Explicit rejects (inherited + new)

| Reject | Why |
|---|---|
| Fleet private keys / mesh as primary jump on the shared Eden VM | 09-18 ADR. Unchanged. |
| Copy Air `~/.ssh` onto Singapore | Always-on god-keyring. |
| Air as unattended jump now that Singapore exists | Singapore replaced that job; do not keep both as primary. |
| Register-all Computers as the mesh | Multiplies full-shell surface; Linux peers may not run Grok Bot. |
| Cursor Cloud self-hosted workers as the Grok reachability story | Different product. Fine for Cloud Agents; orthogonal here. |
| DIY tunnels from the Eden VM when mesh dies | Same key problem, unaudited. |
| Treating Singapore-loop SSH as a P0 gate | Not required. |

---

## 7. Related files

| File | Job |
|---|---|
| Fleet reachability ADR (sibling PR, 2026-09-18) | Parent dual-plane standing |
| `docs/SINGAPORE-HUB-MESH-CHECKLIST.md` | Pubkey authorize + Signal verify (no secrets) |
| `docs/SINGAPORE-HEAVY-HARNESS.md` | Cursor CLI vs Codex vs open harness |
| `docs/SINGAPORE-HUB-OPEN-QS.md` | Owner go / no-go |

**Execute-next (agents):** do not SSH from this Cloud Agent; do not invent credentials; wait for OPEN-QS before installing harnesses or appending keys. Mac / Adam on the execution plane run the checklist after owner `go`.
