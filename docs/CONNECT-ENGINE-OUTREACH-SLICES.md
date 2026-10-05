# Outreach slices — connect 引擎 (externally sayable only)

**Purpose:** conclusions the Outreach seat may use verbatim or paraphrase. Nothing else from `CONNECT-ENGINE-BRIEF.md` is cleared for external use.
**Rule:** every slice carries a claim type and a "sayable as" level. **Do not upgrade a level in a post.** "Running practice" = true today and verifiable; "design intent" = what we are building toward, not yet running.
**Anchors to link:** https://machengshen.github.io/spine/ and https://machengshen.github.io/pipeline/ (both must return HTTP 200 at post time, per existing rule); this repo's `docs/CONNECT-ENGINE-BRIEF.md` once merged.
**Not sayable:** any number (we have measured nothing yet); that any platform account is connected or that any post has been published through the engine; that Zernio analytics are enabled on our plan; that any platform's ranking works a particular way; the names of people who respond; the name of any platform we left, or anything disparaging about it; that agents reply to anyone.

## Slices

| # | Slice (EN) | 切片（中文） | Claim | Sayable as |
|---|---|---|---|---|
| S1 | We publish to find people, not to build an audience. The only number we optimize is how many substantive, unsolicited responses a post gets from people who then actually follow through — by writing back, opening an issue, or continuing the conversation. | 我们发帖是为了找到人，不是为了积累受众。我们唯一优化的数字，是一篇帖子带来多少「主动、有实质内容、并且后续真的跟进」的回应——回信、开 issue、把对话接下去。 | hard_result (under our definition) | design intent |
| S2 | A recommendation system decides who *might* see a post; it cannot decide who *should*. So we treat what each platform rewards as the price of admission to a pool, and treat what we say as the way the right people in that pool select themselves. Two levers, kept separate. | 推荐系统决定的是「谁可能看到」，决定不了「谁应该看到」。所以我们把平台奖励当作进入候选池的门票价格，把内容本身当作让池子里对的人自我选择的方式。两个杠杆，分开用。 | hard_result | design intent |
| S3 | Reach is necessary and not sufficient. A post can be seen by ten thousand people and connect us to none of them. We track reach as an instrument reading, never as a goal. | 曝光是必要条件，不是充分条件。一篇帖子可以被一万人看到、却没有链到任何一个人。我们把曝光当仪表读数，不当目标。 | hard_result | design intent |
| S4 | We read only what platforms officially return about our own posts, plus signals that are public by protocol design. No scraping, no unofficial apps, no borrowed sessions, no growth tools. If a signal is not available that way, we go without it. | 我们只读平台官方接口返回的、关于我们自己帖子的数据，加上协议层面本来就公开的信号。不爬取、不用非官方客户端、不借登录态、不用增长工具。拿不到就不要。 | operational (rule in force for the fleet's public work) | running practice |
| S5 | No agent of ours replies to a person, sends a message to a person, or follows anyone on our behalf. Agents draft; a human speaks. | 我们的 agent 不回复任何人、不私信任何人、不代表我们关注任何人。agent 起草，人来说话。 | operational (current seat ruling) | running practice |
| S6 | Nothing is posted without a typed content packet that passed a public-safety check and got an explicit go. The check runs before every post, and the owner sees only the result: the plan and the live links. | 没有经过公开安全检查、没有拿到明确放行的类型化内容包，不发任何东西。检查在每次发帖前跑，owner 只看结果：计划和上线后的链接。 | operational (existing Outreach-PCSE loop) | running practice |
| S7 | Shared context lives in a memory hub; the seat that drafts posts holds no infrastructure keys; publishing runs where the credentials already live. The connect engine is a set of notes in that hub, not a new service. | 共享上下文在记忆 Hub；起草帖子的席位不持有任何基础设施钥匙；发布在凭证本来所在的地方执行。connect 引擎就是 Hub 里的几类笔记，不是一个新服务。 | operational (dual-plane ADR) + design_hypothesis (engine as hub notes) | running practice (planes) / design intent (engine) |
| S8 | When someone responds, we keep exactly three things: where the reply is, whether it engaged the idea, and whether they followed through. We do not look up who they are. | 有人回应时，我们只记三件事：回应在哪、是否真的在讨论这个想法、后续有没有跟进。我们不去查这个人是谁。 | design_hypothesis (ledger schema) | design intent |
| S9 | On open networks where anyone can write their own feed algorithm, "the algorithm" is many small, readable algorithms. We prefer those networks because what they reward can be inspected rather than guessed. | 在任何人都能自己写 feed 算法的开放网络上，「算法」是许多个小的、可读的算法。我们偏好这类网络，因为它奖励什么可以查看，而不用猜。 | operational (protocol fact) + design_hypothesis (preference pays off) | design intent |
| S10 | We post one thing a week with one stated hypothesis about how it will travel, then read what came back. The sample is tiny, so we call the output a notebook, not a result. | 我们一周发一篇，附一个关于它会怎么传播的假设，然后读回来的东西。样本极小，所以产出叫笔记，不叫结论。 | design_hypothesis | design intent |

## One-paragraph versions

**EN (≤70 words):** We publish to find people, not audiences. The only number we optimize is substantive, unsolicited responses that lead somewhere — a reply, an issue, a conversation. Platform reach is the ticket price, not the prize. We read only what platforms officially return about our own posts, agents never speak to anyone for us, and nothing goes out without a public-safety check and an explicit go.

**中文（≤100 字）：** 我们发帖是为了找到人，不是为了积累受众。唯一优化的数字是「主动、有实质内容、并且有后续」的回应。平台曝光是门票价格，不是奖品。我们只读平台官方返回的、关于自己帖子的数据；agent 不代替我们和任何人说话；没有公开安全检查和明确放行，什么都不发。

## Overclaim guard for Outreach

If a post needs "we run this today", only **S4, S5, S6, and the planes half of S7** qualify. Everything else is "we are designing" and must be phrased that way. No slice may be accompanied by a number, a platform ranking claim, a named responder, or the name of any platform we do not use.
