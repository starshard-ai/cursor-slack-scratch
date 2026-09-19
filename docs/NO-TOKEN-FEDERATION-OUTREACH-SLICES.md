# Outreach slices — no-token federation (externally sayable only)

**Purpose:** conclusions the Outreach seat may use verbatim or paraphrase. Nothing else from the brief is cleared for external use.
**Rule:** every slice carries a claim type and a "sayable as" level. Do not upgrade a level in a post.
**Anchor to link:** `docs/NO-TOKEN-FEDERATION-BRIEF.md` in this repo (public) once merged; the public note "Hub is a blackboard, not a mind" (https://machengshen.github.io/theory/hub-blackboard-not-mind.md); public GOVERNANCE.md (https://github.com/MachengShen/system-evolution-public/blob/main/GOVERNANCE.md).
**Not sayable:** that a charter is signed (it is a draft); that any money ledger exists (none does); that any steward set exists (none is named); any comparison that disparages token projects; any number we have not measured.

| # | Slice (EN) | 切片（中文） | Claim | Sayable as |
|---|---|---|---|---|
| S1 | We are designing a collaboration network with no token and no chain that still keeps the three things a DAO is actually for: a public record nobody can silently rewrite, rules that run the same for the founder as for anyone, and a cheap exit/fork. | 我们在设计一个不发币、不上链的协作网络，但保留 DAO 真正有用的三样：谁也不能悄悄改写的公开记录、对创始人和对任何人一样执行的规则、便宜的退出/分叉权。 | hard_result (under our definition) | design intent |
| S2 | A blockchain is one way to get a tamper-evident record. For a network of named collaborators, a signed public git ledger with several independent full clones is another. We chose the second. | 区块链是拿到防篡改记录的一种方法。对一个成员实名互认的网络来说，带签名的公开 git 账本加几份独立完整克隆是另一种。我们选后者。 | hard_result + design_hypothesis (adequacy) | design intent |
| S3 | A decision exists only when it is in the public ledger. Chat, group rooms and the shared memory hub are for thinking; the ledger is for deciding. | 决策只在进了公开账本时才存在。群聊和共享记忆 Hub 用来思考，账本用来决定。 | hard_result (definitional) | design intent |
| S4 | The founder is bound the same way everyone is: irreversible actions need two human keys, one of them not his, plus a cooling period — and the whole state can be forked by anyone. Visibility and forkability do the binding, not cryptography. | 创始人被约束的方式和所有人一样：不可逆动作需要两把人类钥匙（其中一把不是他的）加冷静期，而且整个状态任何人都能分叉。约束靠的是可见和可分叉，不是密码学。 | design_hypothesis | design intent |
| S5 | Nodes pay their own bills and keep their own revenue. By default the network holds no pooled money at all. | 节点各自付账、各自挣钱。默认这个网络不持有任何公共资金。 | operational (BYOK is current practice) | running practice (for the "pay own bills" half); design intent (for "no pooled money" as a rule) |
| S6 | If a contribution credit can be transferred, redeemed, priced or bridged, it is a token. Ours can do none of those, so it is a receipt, not a currency. | 贡献凭证只要能转让、兑换、定价或桥接，它就是币。我们的四项都不能，所以它是收据，不是货币。 | hard_result | design intent |
| S7 | AI agents draft proposals, compile packets and write receipts. They hold no keys, sign nothing, vote on nothing. | AI 起草提案、整理工单、写收据。不持钥匙、不签字、不投票。 | operational (current seat ruling) | running practice |
| S8 | Shared context lives in a memory hub; execution happens on nodes that hold their own credentials; nothing sensitive sits on a shared vendor VM. Governance is a third, thin layer on top of that: a public ledger. | 共享上下文在记忆 Hub；执行在各自持有凭证的节点上；共享的云端 VM 上不放任何敏感钥匙。治理是叠在上面的第三层薄层：一个公开账本。 | operational (first two) + design_hypothesis (third) | running practice (planes) / design intent (ledger) |
| S9 | Anyone can clone the ledger and continue the work under another name. A fork that does it better is a success of the design, not a threat to it. | 任何人都能克隆账本、换个名字继续干。分叉做得更好，是设计的成功，不是威胁。 | operational (published Fork-Welcome doctrine) | running practice (as stated policy) |

**One-paragraph version (EN, ≤60 words):** No token, no chain. Decisions exist only in a signed public ledger that any member can fork. Irreversible actions need two human keys and a cooling period; the founder is not exempt. Nodes pay their own way; the network holds no pooled money by default. AI drafts, humans sign.

**一段版（中文，≤80 字）：** 不发币、不上链。决策只存在于可被任何成员分叉的签名公开账本里。不可逆动作要两把人类钥匙加冷静期，创始人不例外。节点各自付账，网络默认不持有公共资金。AI 起草，人签字。

**Overclaim guard for Outreach:** if a post needs "we run this today", only S5 (first half), S7, S8 (first two planes) and S9 qualify. Everything else is "we are designing".
