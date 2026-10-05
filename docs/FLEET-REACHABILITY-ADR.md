# ADR: How Grok Bot assistants reach the owner fleet

**Status:** Proposed standing (Cloud Fable, 2026-09-18)  
**Owner:** 沈马成 (Starshard / Eden)  
**Decides:** reachability + taste ingest for Grok Bot seats (Eva / Adam / zhizi-grok)  
**Does not decide:** Mac Codex / Cursor frontstage privileges (unchanged)  
**Surface note:** this file is public. Role names only. No private hosts, mesh IPs, key paths, or Hub ids. Operational pointers live on Memory Hub.

---

## 1. Decision (one path)

**Dual-plane. Keys never land on the shared Grok Bot cloud VM.**

| Plane | Job | Path |
|---|---|---|
| **Context** | Global taste / prefs / standing | Memory Hub. Air *exports* a sanitized standing slice. Grok *reads Hub*. |
| **Work** | Act on machines that already SSH each other | Hub work-packet → Mac Codex / Cursor frontstage or existing fleet pollers. Grok *drafts*. Grok does *not* SSH. |

**Computers / local-exec on Air** is a gated *read/export* surface (owner-approved, per command), not a jump host and not the availability story.

This is stricter than the interim “Air jump **or** register-all Computers” recommendation. Air-as-jump gives every Grok seat on the shared box **fleet root by proxy** the moment Air is online. That is the same blast radius as copying keys onto the Grok VM, plus an intermittent single point of failure.

---

## 2. Why this, not the obvious alternatives

**Facts (already verified):** the Grok Bot cloud VM has no `ssh`, no mesh client, no `~/.ssh`. Air already has the fleet SSH mesh and Cloud Code / Claude taste. Only Air was registered on Computers, and it is intermittent. A 2026-09-17 commander ruling already set Grok seats to **front-end + drafter, not Mac executor**. The local-exec gateway on Air is still **shadow** (logs, does not block). An older credential-separation design already said the conversation host must not hold fleet SSH.

**So:**

- *Global context* is a Hub problem, not a tunnel problem.
- *Live shell on fleet* is a Mac/poller problem, not a Grok-VM problem.
- *Taste on Air* must be **ingested**, not **reached-through**.

If, after P0, owner still wants Grok-initiated live Linux shells, the only acceptable form is a **separate** fleet-control / bastion host — never the shared conversation VM — and only after an explicit written risk accept. See §5 rejects.

---

## 3. Taste ingest (Air → Hub, no key sprawl)

Goal: Eva / Adam / zhizi-grok share Cloud Code taste without copying private keys, raw home dirs, or T1 material onto the Grok VM.

**Allowlist (export these classes):**

- Standing owner prefs already meant for all surfaces
- Project `CLAUDE.md` / Cloud Code rule *excerpts* that are operational, not personal
- Named architectural standings (seat map, PCSE, “记下了” triad)

**Denylist (never copy, never summarize into Hub or Grok memory):**

- Any SSH private key, agent socket, mesh auth key, or `authorized_keys` dump
- Tokens, `*.env`, keychain, API keys
- People-registry / collaborator-memory / voiceprints / call recordings / T1 family notes
- Raw Cloud Code session transcripts (injection + PII)

**Who runs the export:** Mac frontstage on Air (Codex or Cursor), or owner paste. **Not** a Grok local-exec hop that then `ssh`s onward.

**How it lands:** Hub memo tagged `standing` + `audience:all-surfaces` + provenance (`source=air-taste-export`, date, allowlist version). Same turn: shared Grok user-memory profile fact if the item is a preference that should govern talk/act. Chat-local “记下了” alone is a miss (existing standing).

**Refresh:** when Air is online *and* taste drifted. Cadence script on Air is P1. Until then, one manual export is enough for P0.

---

## 4. Threat model (shared multi-agent box)

The Grok Bot cloud VM is a **shared multi-seat conversation host**. A prompt injection, confused-deputy turn, or compromised seat inherits every tool bound to that VM. Putting fleet private keys or a mesh client on that box makes one bad turn into full fleet takeover (Charter classes C/B). Using Computers on Air as an unattended SSH jump is the same takeover **without copying keys**: Air already holds the mesh.

Further risks if we collapse context into live Air reads: belief-supply-chain (unsanitized home-dir text becomes cross-agent “truth”), T1/people exfil, and kill-switch bypass (Charter freeze flags do not bind Computers local-exec today). Seat isolation on the shared box is unspecified — treat all Grok seats as one principal for blast-radius math.

---

## 5. Explicit rejects

| Reject | Why |
|---|---|
| Fleet private keys or mesh client on the shared Grok Bot cloud VM | Shared multi-agent blast radius = whole fleet. Owner must accept in writing *and* justify harder than this ADR; default is no. |
| Copy Air `~/.ssh` / automation keys onto the Grok VM | Same as above, plus secret-in-vendor-cloud. |
| **Air as unattended jump host for Grok seats** (interim Eva primary) | Fleet root by proxy; Air intermittent; contradicts 09-17 drafter tier; gateway still shadow. |
| Register-all Computers as the mesh | Multiplies full-shell executor surface; does not ingest taste; Linux fleet may not even support the product. |
| Cursor Cloud self-hosted workers as the Grok reachability story | Different product. Fine for Cursor Cloud Agents; orthogonal to Grok seats. |
| Second dispatcher / parallel control plane from Grok | Spine is Hub + existing Mac/forge/poller. |
| Reverse tunnels or DIY mesh originating on the Grok VM | Ad-hoc, unaudited, same key problem. |
| Dumping raw Cloud Code history / T1 / tokens into Hub or Grok memory | Injection + PII + credential leak. |

---

## 6. PCSE / Charter bright-line gaps (flag, do not silently paper over)

1. **Charter v0.1 is still draft / unsigned** and has no row for “shared vendor cloud agent VM” or “Computers local-exec.”
2. **No named bright-line for proxy fleet root** (local-exec on Air → existing SSH mesh). Effect equals key sprawl; text does not say so.
3. **PCSE (a–e) + predicate (f)** gate *publish/send/identity*, not *credential placement on a vendor VM*.
4. **Kill switch does not bind** Computers local-exec or the Grok cloud sandbox.
5. **Local-exec gateway on Air is still shadow** — 09-17 tier is policy, not enforcement.
6. **Taste classification is unspecified** — which Air files may enter Hub is a new allowlist, not a Charter clause.
7. **Credential-separation bastion was design-only** — there is no isolated fleet-control VM to point Grok at even if owner later accepts live shells.
8. **Shared-box seat isolation is unspecified** — one principal for blast radius until proven otherwise.

Do not treat this ADR as a Charter amendment. Charter edits still need owner sign-off + cooling-off.

---

## 7. Phased rollout

### P0 — this week (enough to operate)

Owner / Mac / Grok can execute without new infra.

- [ ] **Adopt this ADR as standing.** Hub memo `standing` + `audience:all-surfaces`. This file is the public one-pager.
- [ ] **Owner-hand:** Grok Bot → Agent → Execution on Local Computer → **Always require approval** (or Never). Do not set Always allow.
- [ ] **Mac frontstage (Air, when online):** one taste-export. Allowlist in §3. Write Hub standing memos + Grok profile facts. Receipt on Hub.
- [ ] **Grok seats:** fleet work = Hub work-packet only. No `ssh` via Air. No mesh install on the Grok VM.
- [ ] **Computers:** keep Air registered if useful for *owner-approved* read/export. Do not treat it as a jump host. Do not register the whole fleet “so Grok can SSH.”
- [ ] **If Air is offline:** context still comes from Hub; work still goes to pollers / next Mac session. Do not invent a tunnel.

### P1 — after P0 works

- [ ] Air-local taste-export script + cadence (LaunchAgent or forge packet). Allowlist versioned.
- [ ] Promote local-exec gateway from **shadow → enforce** only after the already-queued cross-family review passes.
- [ ] Bind kill-switch / freeze flag into local-exec and packet-open.
- [ ] Seat ACL: which Grok seats may *request* Computers at all (default: none unattended).
- [ ] Optional extra Computers registrations = interactive **read** surfaces, not a mesh substitute.
- [ ] Only if live Linux shell from Grok is still a real need: **separate** bastion / fleet-control host, scoped keys, owner written risk accept. Never the conversation VM.

---

## 8. Execute-next checklist (copy)

**Owner (minutes):**

1. Set Grok local-exec to Always require approval (or Never).
2. When Air is in hand: say yes to one Mac taste-export session.
3. Do **not** approve mesh/keys on the Grok VM unless you are explicitly accepting §5 row 1.

**Mac Codex / Cursor frontstage:**

1. Claim a packet: “Air taste-export v0 — allowlist §3, denylist §3, Hub standing + receipt.”
2. Do not let Grok seats run the export via local-exec + `ssh`.
3. Keep holding Class C / forge / ledgers.

**Eva / Adam / zhizi-grok:**

1. Read Hub for taste. Draft work-packets. Do not jump.
2. If a task seems to need live fleet shell, name the packet for Mac/poller — do not install `ssh` on the Grok VM.
3. Anti-signals: Hub write under another source; claiming “done” without a Mac/Codex receipt; any proposal to “just copy the keys so we’re not blocked.”

---

## 9. Supersedes

Eva interim (same-day): “Air jump **or** register more Computers; no mesh+keys on the Grok VM unless owner accepts.”

**Keep:** no mesh+keys on the Grok VM.  
**Replace:** Air jump / register-all as the *primary* pattern.  
**Use instead:** Hub context + Hub work-packets; Computers = gated read/export only.
