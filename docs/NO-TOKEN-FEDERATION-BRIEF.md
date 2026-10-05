# Brief: a no-token, no-chain collaboration network that still behaves like a durable DAO-style org

**Status:** Architecture brief (Cloud Fable, 2026-09-19). Proposed standing; owner go/no-go in `NO-TOKEN-FEDERATION-OPEN-QS.md`.
**Owner:** 沈马成 / Macheng (Starshard / Eden)
**Decides:** the governance shape for a federated collaboration network — members, public-asset gates, money in/out, survival on exit — mapped onto the existing dual-plane Starshard–Eden stack.
**Does not decide:** legal jurisdiction, any product build, any specific person's role.
**Surface note:** this file is public. Role names only. No private hosts, no Hub ids, no secrets, no PII. Operational pointers live on Memory Hub under the standing titles named in §9.

**Claim types used in this file** (every load-bearing sentence carries one):

| Tag | Meaning |
|---|---|
| `hard_result` | Follows from the stated definition alone. No empirical claim. Falsify by attacking the definition. |
| `operational` | Already a standing or mechanism in our stack, or a mechanical rule we can enforce today without new infrastructure. |
| `design_hypothesis` | Proposed here. Untested. Each carries a disconfirming test in §7. |

Mapping to the fleet claim-typing guardrail: `hard_result` ≈ definitional result; `operational` ≈ enforced standing; `design_hypothesis` unchanged. Nothing here is `measurable_physics`. Nothing here is a legal opinion.

---

## 0. 综述（owner 先读这一节）

问题：不发币、不上链，怎么让一个协作网络具备 DAO 真正值钱的那三样东西——**规则也管得住创始人、公开决策和钱可审计、人走了组织还在**——并且贴在我们已有的双平面（Hub 上下文 + Hub 工单）架构上。

**结论一句话：DAO 的价值不在币，在「有第三方能核对的公开账本 + 对谁都一样执行的规则 + 便宜的退出/分叉权」。这三样用签名的公开 git 账本、双钥门禁、和「每个节点都持有全量副本」就能得到；链是其中一种实现，不是合法性的来源。** `hard_result`（见 §1 定义）

关键设计判断（其余章节展开）：

1. **决策 = 账本条目。** 不在公开账本里的，就不是组织决策，只是聊天。Hub 是黑板，不是脑；账本才是有签名权的地方。`hard_result` under §1 def
2. **管住创始人的不是密码学，是「可见 + 可分叉」。** 比特币本身也是「去中心化但可变」（软/硬分叉），它的约束力来自公开可验证和退出便宜，不来自不可变。我们照抄这一点：创始人对章程/公共资产的 Class C 动作走双钥 + 24h 冷静期，且第二把钥匙在非创始人 steward 手里；未进账本的变更视为无效。`design_hypothesis`（双钥落地）+ `operational`（Charter v0.1 已有 24h 冷静 + 二次确认 + proposal-not-mutation）
3. **不是把创始人踢出回路，是把他的改动权变成最大可追责。** 之前已裁过：「把我从中间解脱出去」是 abdication，反自身对齐原则；正确形状是 principal-in-the-loop + 写保护 + 提案不直改 + kill switch。本 brief 不改这条。`operational`
4. **钱：默认不设公共资金池。** 节点各自挣钱、各自付 API（BYOK 已是 standing）。如果一定要有共同的钱，走普通银行/支付通道 + 公开逐条流水（进/出/目的/审批签名/凭证哈希）+ 出账为 Class C。`operational`（BYOK）+ `design_hypothesis`（公开流水格式）
5. **积分红线：能转让或能兑换的就是币。** 贡献凭证只能是不可转让、不可赎回、不可替代的 receipt。它可以影响角色分配，永远不是对资产的索取权。`hard_result`（定义上无市场价格 ⇒ 不是 token）
6. **人走了还在：每个 steward 本地都有账本 + Hub 公开切片的全量克隆；每项 Class C 资产 ≥2 个独立可达的 steward；创始人失联 N 天后可执行「预先公开的维持运转程序」（只维持、不造新品牌、不动钱以外的事）。** `design_hypothesis`
7. **AI 只当秘书：起草提案、整理工单、编账本条目。AI 席位没有签名权，不投票，不持有 steward 钥匙，永远（不是「暂时」）。** `operational`（已裁 Grok 席位 = 起草席）+ 需 owner 把「永远」拍死（Q6）

不做的事：不发币、不建 L1/L2、不做「其实是币的积分」、不把链当合法性前提、不写 AWS/链/DAO 产品代码。

---

## 1. Definitions (what "DAO-style" means once you remove the coin)

Strip a DAO to what a collaboration network actually needs. Under this brief:

> A **durable DAO-style org** is a network satisfying:
> **(R) Record** — a public, append-only record of decisions, roles, assets and money that no single party can silently rewrite, and that at least one party other than the writer can verify.
> **(E) Equal execution** — rules are executed the same way regardless of who invokes them, founder included.
> **(X) Exit** — any member can leave, and any group of members can fork the full state and continue, at low cost.

Blockchain provides (R) via global Byzantine consensus among strangers. A collaboration network of named nodes does not need consensus among strangers; it needs **tamper-evidence plus independent witness**.

**H1.** Under the definition above, a chain is *sufficient* but not *necessary* for (R). A signed, publicly mirrored, append-only ledger with ≥2 independent full clones satisfies (R) as long as not all clone-holders collude. `hard_result`

**H2.** A "credit" that is non-transferable and non-redeemable has no market price and is therefore not a token; conversely, any credit that is transferable *or* redeemable is a bearer instrument and must be treated as a token (and is out of scope here). `hard_result`

**H3.** The Hub holds no signing key, so it holds no decision authority. A decision exists iff it appears in the ledger. Everything in the Hub is context, drafts, or receipts. This is the same result as the public note "Hub is a blackboard, not a mind" (https://machengshen.github.io/theory/hub-blackboard-not-mind.md), applied to governance. `hard_result`

**H4.** A rule that only the founder can verify does not bind the founder. Binding requires that a non-founder can verify compliance from the public record. `hard_result`

---

## 2. Three planes (dual-plane + one thin governance plane)

| Plane | Job | Medium | Who writes | Claim |
|---|---|---|---|---|
| **Context** | standing, taste, somatic digest, drafts, receipts | Memory Hub | any seat, under its own source | `operational` (fleet-reachability ADR) |
| **Work** | act on machines and external systems | Hub work-packet → node executor; nodes hold their own keys; no fleet keys on shared vendor VMs | node executors; AI seats draft only | `operational` (fleet-reachability ADR) |
| **Governance** (new, thin) | charter, roster, asset register, money ledger, decisions | one public git repository, signed commits, ≥2 steward clones | humans with steward keys; AI seats may open PRs, never merge | `design_hypothesis` |

The governance plane is what a chain would have been. It is **witnessed, not consensus-driven**: a decision is valid when (a) it is a signed commit on the canonical branch, (b) it passed the gate class for its action type (§4), (c) at least one steward other than the author has pulled it (their clone is the witness). `design_hypothesis`

Why git and not a chain: the trust model is named parties with reputations, not anonymous adversaries; the write rate is tens of entries per month, not thousands per second; and the exit right (X) is native — `git clone` is the fork. `hard_result` for (X); `design_hypothesis` for adequacy of witness count.

Two-layer topology preserved: **cognition decentralized** (any node can think, draft, propose in the Hub) — **irreversible action gated** (only the governance plane can commit, and only humans hold its keys). `operational` (existing standing).

---

## 3. Members

**Definition.** A member is (a) a roster entry in the governance ledger (role name + public key + tier + sponsor), and (b) a node that can produce receipts. No entry, no membership. `hard_result` under def.

| Tier | Can do | Cannot do | Claim |
|---|---|---|---|
| **Observer** | read the public Hub slice and the ledger | write anywhere | `operational` |
| **Contributor** | write to Hub under own source; draft packets; open governance PRs | merge governance PRs; hold asset access | `operational` (matches current seat lanes) |
| **Steward** | co-sign Class B/C actions; hold a full ledger clone; hold access to ≥1 Class C asset | act alone on Class C | `design_hypothesis` |
| **Founder** | everything a steward can, plus the declared asymmetries in §3.1 | bypass the gate classes | `design_hypothesis` |
| **AI seat** | draft, summarize, compile proposals, run reversible work-packets | hold any key; sign; vote; be a steward | `operational` (drafter tier ruling) |

**Nodes earn separately.** Each node pays its own provider bills and keeps its own revenue (BYOK standing). The org does not become a shared API backend or a payroll. `operational`

**AI seats have a human sponsor** who is accountable for that seat's Hub writes. Provenance is the seat's own source string; writing under another source is an anti-signal (already flagged in fleet review). `operational`

**Joining:** sponsor opens a roster PR; two stewards merge; the new member's first act is a receipt. **Leaving:** key revoked, roster entry archived (not deleted); prior receipts and ledger entries remain — the record does not forget contributors. `design_hypothesis`

**Public-safe roster.** Role names and public keys only. No real names, no contact details, no PII in the public roster; the mapping from role to person lives off-ledger with the sponsor. `operational` (PCSE clean-content predicates).

### 3.1 Declared founder asymmetries (published, not hidden)

The founder keeps a veto over the **sovereign set** already defined by PCSE: private-person references, financial specifics, org/product naming and first-time identity acts, new public surfaces, legally binding promises in his voice. `operational`

Everything else runs through the same gate classes as any steward. The asymmetry is written into the charter so that it can be checked, not smuggled in through key ownership. `design_hypothesis`

---

## 4. Public-asset gates (the "irreversible action gated" layer, applied to org assets)

**Definition.** A public asset is anything the org is identified by or pays with: names, domains, GitHub orgs/repos, social accounts, mail identities, shared funds, and the governance ledger itself.

Every asset gets one row in an **asset register** (in the ledger): asset, legal holder, steward(s) with access, gate class, recovery path. `design_hypothesis`

| Class | Definition | Gate | Examples | Claim |
|---|---|---|---|---|
| **A — reversible ≤1h** | can be undone by anyone with access inside an hour | PCSE default: ship + Hub receipt, no human gate | docs commit, Hub memo, draft post to a cleared surface | `operational` |
| **B — reversible but costly** | undo is possible but slow, or affects others | one steward + author (2 humans), receipt before action | roster change, repo settings, publishing under the org name | `design_hypothesis` |
| **C — irreversible or sovereign** | cannot be undone, or touches the sovereign set | public proposal in ledger → 2 steward keys (one non-founder) → 24h cooling → second confirmation → signed commit → action → receipt | naming, domain transfer, money out, legal commitment, deleting an asset, changing this table | `operational` for the 24h + second-confirm pattern (Charter v0.1 mechanism 2); `design_hypothesis` for the non-founder second key |

**Kill switch** applies to the org's automated executors exactly as today (FREEZE ALL / kill-switch memo / file flag): pollers stop claiming, outbound stops, no Hub writes. Governance-plane merges are human-only anyway, so freeze does not need to bind git. `operational` (Charter v0.1 mechanism 5; honor-system limitation acknowledged there still applies).

**Rule of the empty ledger.** Any Class B/C action that cannot be found in the ledger is, by definition, unauthorized — whoever did it, founder included. This is what makes H4 operational. `hard_result` under def.

---

## 5. Money in / money out

**Default: no pooled treasury.** Nodes earn separately; the org holds no money and therefore has no treasury attack surface, no token temptation and no tax entity question. `operational` (BYOK). This is the recommended v0.

**If a shared pot is created (owner Q1):**

| Element | Rule | Claim |
|---|---|---|
| Vehicle | ordinary bank / payment processor account held by a legal holder named in the asset register (person-as-trustee with published terms, or a light legal wrapper) | `design_hypothesis` |
| Ledger | every inflow and outflow as one row in the public money ledger: date, direction, amount, currency, purpose, approver key ids, hash of the private receipt | `design_hypothesis` |
| Reconciliation | monthly statement-vs-ledger reconciliation posted as a signed commit; mismatch is a Level 2 anomaly | `design_hypothesis` |
| Outflow gate | above a published threshold → Class C; below → Class B | `design_hypothesis` |
| Inflow types | grants, consulting, positive-sum value-sharing arrangements agreed per-project; no sale of any credit, badge, or membership | `design_hypothesis` |
| Privacy | amounts and purposes are public; counterparties are role-named or aggregated when they are private individuals (PCSE predicate on financial specifics of persons) | `operational` |

**Recognition is not money.** Contribution receipts (§1 H2) are non-transferable, non-redeemable, non-fungible. They may inform *who is asked to steward*; they are never a claim on the pot, never priced, never exchanged. Quarterly audit question: "can any credit in this system be moved or cashed?" — if yes, the system has drifted into a token and the credit is retired. `hard_result` (H2) + `operational` (audit rule is mechanical).

**"Points that are secretly tokens" test** (mechanical): a credit is a token if any one holds — (i) transferable between members; (ii) redeemable for money, services, or assets; (iii) listed, priced or bridged anywhere; (iv) mintable in proportion to money paid in. All four must be false. `hard_result`

---

## 6. Survival when people leave (including the founder)

| Requirement | Mechanism | Claim |
|---|---|---|
| State is not in anyone's head | all decisions in the ledger; standing in Hub; both exportable as plain files | `operational` (Hub) + `design_hypothesis` (ledger) |
| Each shard holds the whole | every steward keeps a full clone of the ledger and a periodic export of the public Hub slice | `design_hypothesis` (already a doctrine phrase; not yet a measured invariant) |
| No bus factor of one on assets | every Class C asset has ≥2 stewards with *independent* access or a documented recovery path; register audited quarterly | `design_hypothesis` |
| Hub failure is survivable | Hub is rebuilt from ledger + receipts, not the other way round (the Bali lesson: strategy that lives only in a chat dies; strategy in receipts is re-instantiated) | `operational` (existing standing) |
| Continuity when founder is unreachable | published procedure, pre-authorized in the charter: after N days with no signed founder activity, 2 stewards may run "keep the lights on" — renew domains, pay existing bills, rotate leaked keys, freeze outbound. Explicitly excluded: new naming, new surfaces, new spending programs, charter edits | `design_hypothesis` |
| Fork right | anyone can clone the ledger and continue under a different name; the *name* follows the legal holder, the *work* follows whoever keeps working (Fork-Welcome doctrine) | `operational` (published doctrine) + `hard_result` for (X) |

The continuity procedure is deliberately *not* a succession of authority. It is maintenance with a hard scope. Who inherits naming/identity authority if the founder is permanently gone is an owner decision, not something this brief can settle (Q4 asks only about maintenance).

---

## 7. Failure modes (detection → response → disconfirming test)

| # | Failure | How you would notice | Response | Disconfirming test for the design |
|---|---|---|---|---|
| F1 | Founder acts outside the gates (key capture or defection) | Class B/C effect with no ledger entry | stewards publish the diff; members fork if unresolved | if a founder-only action *cannot* be detected from public record, H4 is violated → redesign |
| F2 | Shadow governance — decisions made in chat, ratified nowhere | Eden/Hub shows "we decided" with no ledger entry | rule of the empty ledger; Eden stays align-only | count decisions referenced in Hub that lack a ledger entry; >10% over a quarter → the plane is not being used |
| F3 | Credits drift into tokens | any transfer, price, or redemption path appears | retire the credit class | quarterly four-part test (§5) fails |
| F4 | AI-seat creep — agent drafts become de facto decisions | merged governance PR authored and approved without a human co-sign; agent "done" without human receipt | revoke merge rights; freeze | audit: any governance commit signed by a non-human key = design failure |
| F5 | Hub treated as mind — Hub content cited as authority | "the Hub says" used to justify a Class B/C action | H3; require ledger citation | same audit as F2 |
| F6 | Legitimacy debt — appeals absorbed, never answered (dissipative channel) | appeal-to-correction closure rate falls | publish the closure rate; make appeals Class B items | if closure rate cannot be computed, the channel is dissipative by construction |
| F7 | Bus factor one on an asset | register row with a single steward | add steward or recovery path | quarterly register audit finds any row with one holder |
| F8 | No legal personality — who actually owns the domain/account? | asset register "legal holder" blank or a private person with no published terms | Q1 | any Class C asset without a named legal holder |
| F9 | Belief supply chain — untrusted content becomes cross-agent truth | Hub memo without provenance in a standing class | untrusted-source quarantine (Charter mechanism 3) | already a Charter item; not re-derived here |
| F10 | Witness collusion — all steward clones agree to rewrite history | requires every steward | fork by any dissenting member; public mirror history | if steward count < 3, H1's non-collusion assumption is weak → raise count or accept risk in writing |

Two honest limits. First, the Charter these gates lean on is **still v0.1 draft, unsigned** — the cooling-period and two-key rules are a pattern, not yet a ratified constraint. Second, the "not in ledger = not a decision" rule is only as strong as the habit of using it; the F2 test is the one to watch in the first quarter.

---

## 8. What is deliberately not proposed

- Minting any token, coin, or point that passes any part of the §5 test.
- Deploying or depending on any L1/L2, smart contract, or on-chain vote.
- Treating a chain, a legal entity, or a headcount as the source of legitimacy. Legitimacy here is: public record + equal execution + cheap exit.
- Removing the founder from the loop. The design binds him by visibility and forkability, not by lock-out.
- Any AI seat with signing, voting, or steward authority — now or later.
- Building product code for any of this. The governance plane is a git repository and a habit.

---

## 9. Mapping to existing standings (what this brief reuses, by title)

| Existing standing (by public title) | Used as |
|---|---|
| Fleet reachability ADR — dual-plane, no keys on the shared Grok VM (`docs/FLEET-REACHABILITY-ADR.md`, this repo) | Context and Work planes unchanged |
| "Hub is a blackboard, not a mind" (public note) | H3 |
| Two-layer topology — cognition decentralized, irreversible action gated | §2, §4 |
| Pre-Cleared Ship Envelope (PCSE) — gate on content, not act; sovereign set | Class A default, §3.1 asymmetries, §5 privacy |
| Safety & Adversarial Charter v0.1 (draft) — proposal-not-mutation, 24h cooling, kill switch, untrusted-content quarantine | Class C pattern, §4 kill switch, F9 |
| Grok Bot seats = drafter tier; Eden = alignment only; private chats build | AI-seat row, F2 |
| BYOK / nodes pay their own provider accounts | §5 default |
| Fork-Welcome + Global-Vote-Survival (public GOVERNANCE.md) | (X), §6 fork right |
| Bitcoin-analogy reframe — "make mutation power maximally accountable" ≠ "remove the principal" | §0 item 3, §8 |
| Claim-typing guardrail | this file's tag scheme |

### Filing block (for Adam / Hub filing, no re-derivation needed)

- **Suggested Hub summary:** `[standing-proposed] No-token federation brief: decisions = signed public ledger; founder bound by 2-key + 24h + forkability; nodes earn separately; AI drafts only`
- **Suggested tags:** `standing`, `proposed`, `architecture`, `governance`, `no-token`, `federation`, `starshard-eden`, `audience:all-surfaces`, `owner:macheng`, `from:fable`, `claim-typed`
- **File first:** §0 (Chinese synthesis) + `NO-TOKEN-FEDERATION-OPEN-QS.md`. Tables are appendix.
- **Do not file as:** `enforced`. Nothing here is enforced until the owner answers the open questions.
