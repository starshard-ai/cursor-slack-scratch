# Brief: the「connect 引擎」— using platform reward signals to find same-frequency people, not audiences

**Status:** Architecture brief (Cloud Fable, 2026-09-19). Proposed standing; owner go/no-go in `CONNECT-ENGINE-OPEN-QS.md`.
**Owner:** 沈马成 / Macheng (Starshard / Eden). Requested via the Outreach seat.
**Decides:** what the connect engine optimizes, which data it may touch, who drafts / gates / publishes / learns, and the thinnest loop worth running first.
**Does not decide:** which platforms the owner connects, any Zernio plan purchase, any product code, any reply sent to a specific person.
**Surface note:** this file is public. Role names only. No private hosts, no Hub ids, no secrets, no PII, no third-party handles. Operational pointers live on Memory Hub under the standing titles named in §9.

**Claim types used in this file** (every load-bearing sentence carries one):

| Tag | Meaning |
|---|---|
| `hard_result` | Follows from the stated definition alone. Falsify by attacking the definition. |
| `operational` | Already a standing or mechanism in our stack, or verified this turn against vendor/platform documentation. |
| `design_hypothesis` | Proposed here. Untested. Each carries a disconfirming test in §8. |
| `OPEN-Q` | Unknown. Not to be stated as fact anywhere until resolved. Listed in `CONNECT-ENGINE-OPEN-QS.md`. |

---

## 0. 综述（owner 先读这一节）

**一句话：connect 引擎不是增长引擎。它把每个平台的推荐奖励当作「进入候选池的门票价格」来学习，真正优化的唯一目标是「每篇帖子带来的合格同频接触数」；曝光、阅读、停留只是仪表，不是目标。** `hard_result`（§1 定义）

问题：我们要通过 Zernio 多平台发帖，去链到「同频的人」——能一起改变世界的人。平台推荐系统只奖励它自己想要的行为（互动速度、停留、回复），不奖励「对的人看到了」。如果直接照着平台的仪表盘优化，会漂成流量号。如果无视平台奖励，帖子根本进不了候选池。connect 引擎要做的，是把两者分层：**平台奖励 = 约束条件（门票），同频接触 = 目标函数。**

关键设计判断（其余章节展开）：

1. **目标函数只有一个：合格同频接触（Qualified Same-frequency Contact, QSC）/ 帖。** 一个 QSC = 公开的、有实质内容的回应（回复/引用/邮件/GitHub issue），且回应者随后进入我们的第一方渠道（回信、开 issue、进 Hub 公开面）。点赞、关注、曝光都不是 QSC。`hard_result`（定义）
2. **平台奖励只做「门票模型」。** 每个平台一张 reward card：这个平台目前奖励什么格式、什么节奏、什么互动类型；置信度标注；每周更新。用来决定「怎么发才进得了池子」，不用来决定「发什么」。`design_hypothesis`
3. **数据面 fail-closed。** 只用 Zernio analytics、各平台官方 API、真公开信号（Bluesky 公开 AppView、GitHub 公开 API、我们自己的页面）。不做灰产采集、不逆向移动端、不撞库、不违 ToS。小红书封禁的直接原因就是自动化写草稿——这条教训写进 kill switch。`operational`（小红书 2026-09-06 废弃；Zernio 指标表已核对）
4. **贴在既有三件套上，不加新席位。** Hub 放 reward card + connection ledger + work packet；Outreach 席位（共享 VM）起草、读 Hub、不持 fleet 钥匙；Mac/fleet 或持 Zernio 凭证的执行面发布；Cloud Fable / Adam 学习并写 card。发布仍然走 Outreach-PCSE：无 standing content packet + PCSE 通过 = 不发；owner 只看结果（计划 + HTTP 200 后的 URL）。`operational`
5. **MVP 薄到只剩一个闭环：** 每周一个 packet → 2 个平台变体（带各自的 anchor 链接标记）→ 72h 后拉 Zernio 分析 + inbox 评论 → 人读回应文本、记 QSC → 更新 reward card → 下周 packet 带一个假设。没有 A/B、没有仪表盘、没有自动回复。`design_hypothesis`
6. **样本极小，所以只做「察觉」不做「证明」。** 一周一帖，统计功效接近零。引擎的产出是带置信度的 card 和一份人可读的 ledger，不是显著性结论。`hard_result`（N≈4/月）

不做的事：小红书、微信；付费投放；关注/取关、互赞、互推池；自动私信；自动回复评论；构建自己的推荐系统；对陌生人做跨平台身份归并；把粉丝数当目标。

---

## 1. Problem and telos

### 1.1 What the owner actually wants

Chain to **same-frequency people** (同频的人): people who, on reading the work, respond in a way that shows they already think in this direction and could build alongside. The public anchors that carry the work today are the spine (https://machengshen.github.io/spine/) and the pipeline tutorial (https://machengshen.github.io/pipeline/), plus the public org (https://github.com/starshard-ai). `operational`

Standing doctrine already says: attract-not-chase; route artifacts into external recommendation engines and learn from feedback; score signal quality beyond vanity metrics. This brief is the architecture for that doctrine, restricted to a compliant data plane. `operational`

### 1.2 Definitions

> A **Qualified Same-frequency Contact (QSC)** is a response to one of our posts that satisfies all three:
> **(S) Substance** — the public text engages the idea (agrees with a reason, disagrees with a reason, extends it, asks a real question). A like, a bare "great post", a follow, or an emoji is not substance.
> **(R) Reciprocity** — the responder acted first; we did not solicit, tag, DM, or reply-bait them.
> **(F) Follow-through** — within a window (default 14 days), the responder enters a first-party channel we control: email reply, GitHub issue/PR/discussion, or a public reply thread that continues past one exchange.

**Connection quality of a post** = number of QSCs it produced. **Connection quality of a platform** = QSCs per post on that platform over a window. `hard_result` under the definition.

> A **platform reward** is whatever the platform's ranking system observably pays for with distribution. It is measured only through signals the platform (or Zernio on its behalf) officially returns.

**H1.** Reach is necessary for QSC but not sufficient; QSC is bounded above by (reach × density of same-frequency people in the pool reached). Therefore maximizing reach without moving pool density can raise reach indefinitely while QSC stays flat. `hard_result`

**H2.** The engine has two levers only: *admission* (what the platform rewards, so the post enters a pool at all) and *selection* (what the post says and links to, so the right people in that pool self-select). Admission is learned from platform metrics; selection is learned from QSC text. Confusing the two is the Goodhart path. `hard_result`

**H3.** Because QSC requires follow-through into a first-party channel, the strongest sensor in the whole system is the owner's own inbox / GitHub / anchor pages — not any platform API. `hard_result`

---

## 2. Research questions — what "recommendation rewards" means per platform class

Platforms are grouped by *how their distribution is decided*, because that is what determines which signals are even meaningful.

| Class | Platforms (Zernio-connectable) | How distribution is decided | What "reward" plausibly means | Inspectability |
|---|---|---|---|---|
| **A. Open graph, user-chosen feeds** | Bluesky | Chronological following feed + user-subscribed custom feed generators; the ranking code of any feed is whatever its author wrote; public AppView, no auth for reads | Being picked up by feed generators and reposted by connectors; the "algorithm" is many small algorithms | High. Feed generators are inspectable; likes/reposts/threads are public API. `operational` |
| **B. Closed engagement-ranked feeds** | X, Threads, LinkedIn | Proprietary ranking; early engagement velocity and reply depth widely reported to dominate; link posts commonly reported as down-weighted (X now also prices link posts higher on its API) | Fast replies > likes; native text/media > external links; conversation threads | Low. Only the platform's own post metrics are returned. `design_hypothesis` for the weightings |
| **C. Search / long-form** | YouTube, Reddit; our own GitHub Pages via web search and LLM crawlers | Query match + retention; slow, durable | Retention, answering a real query, being cited | Medium for YouTube (retention metrics exist); high for our own pages (we own them) |
| **D. Messaging / no recommender** | Telegram, Discord, Slack, WhatsApp | No ranking; broadcast to members | Not applicable | Zernio returns no analytics for these. `operational` |
| **Out of scope** | Xiaohongshu / 小红书, WeChat | — | — | Abandoned by owner 2026-09-06 (account muted after automated drafting). Not designed for. |

**RQ1 (Class A).** On Bluesky, which *feed generators* carry our posts, and do QSCs cluster by feed? If yes, the admission lever is "write for feed X", which is inspectable and compliant. `design_hypothesis`

**RQ2 (Class B).** On X / Threads / LinkedIn, does the ratio replies:likes on our posts predict QSC better than impressions do? If yes, reward-card features should be reply-oriented, not reach-oriented. `design_hypothesis`

**RQ3 (Class B).** Does "anchor link in the first post" vs "anchor link in the first reply" change impressions on X/Threads, and does it change QSC? This is the cheapest admission experiment and directly tests the folk claim about link penalties. `design_hypothesis`

**RQ4 (cross-class).** Does the same packet, posted to two classes, produce QSCs from *different* kinds of people (judged from the public reply text only)? If yes, platforms are audiences, not channels, and packets should be written per class. `design_hypothesis`

**RQ5 (Class C).** Do QSCs arrive via the anchor pages (spine / pipeline) with no platform post at all — i.e. via search or LLM citation? If so, the anchor pages are a channel in their own right and deserve their own reward card. `design_hypothesis`

**RQ6 (telos check).** After 8 weeks, do the people in the connection ledger look like collaborators (they build, they cite, they push back) or like an audience (they consume)? This is judged by the owner, not by a metric. `OPEN-Q` until data exists.

What we are *not* asking: how to reverse-engineer any ranking model; how to game velocity with coordinated engagement; how to grow follower counts.

---

## 3. Compliance data surface matrix

Fail-closed rule: **if a signal is not in this table, the engine does not read it.** Adding a row requires a PR to this file. `operational` (rule); rows below verified this turn against Zernio documentation and platform developer documentation.

### 3.1 Allowed sources

| Source | Allowed signals | Access path | Gaps / caveats | Status |
|---|---|---|---|---|
| **Zernio per-post analytics** (`GET /v1/analytics`) | Per platform, per post: impressions, reach, likes, comments, shares, saves, clicks, views — **only where the platform exposes them** (see 3.2) | Zernio OAuth-connected accounts; MCP or REST | Metrics are what the platform's official API returns to Zernio; insights lag (e.g. ~24h on some platforms) and read 0 until available. LinkedIn personal accounts: metrics only for posts published *through* Zernio. | `operational` (documented) |
| **Zernio daily metrics / follower stats** | Daily aggregated metrics per platform; follower history | Same | **Requires the Zernio Analytics add-on.** Whether the owner's plan includes it is unknown. | `OPEN-Q` (Q2) |
| **Zernio post timeline** (`/analytics/post-timeline`) | Engagement-over-time for one post | Same | Same add-on question; this is the only "velocity" sensor we have. | `OPEN-Q` (Q2) |
| **Zernio inbox — comments / mentions** | Public comments on our posts and public mentions of our accounts: text, public author handle, timestamp | Same | Read-only use. We read *text* to judge Substance (S). We do **not** call private-reply / DM endpoints (see 3.3). Platform coverage varies. | `operational` (read); `operational` (DM prohibition) |
| **Bluesky public AppView** (`public.api.bsky.app`, unauthenticated reads) | For *our own* posts: likes, reposts, quote posts, full reply thread; feed generators our posts appear in (via `getFeedGenerator` metadata on feeds we choose to check) | Public HTTP, no token | Fully public by protocol design. Same handle-only, no-enrichment rule applies. Do not use the firehose to track third parties. | `operational` (documented public API) |
| **Threads Insights API** (via Zernio, or directly with owner's OAuth) | Per post: likes, replies, reposts, quotes; views/shares marked "in development" by Meta | Official Graph API with `threads_manage_insights` | Only our own media. | `operational` (documented) |
| **X API v2 metrics** (via Zernio) | `public_metrics`: impressions, likes, reposts, replies, quotes, bookmarks. `non_public_metrics` (URL clicks, profile clicks) exist for own posts ≤30 days but need user-context auth | Official; X is pay-per-use for new developers (no free tier) | Whether Zernio surfaces `non_public_metrics` (clicks) for X is documented as "clicks: yes" but the exact field mapping is unverified. Connecting X through Zernio required a payment method as of week 38. | `operational` (public metrics); `OPEN-Q` (clicks mapping) |
| **LinkedIn Member Post Analytics** (via Zernio) | Impressions, members reached, reactions, comments, reshares; saves/sends (personal), clicks (organization pages) | Official, approval-gated Community Management API — Zernio holds the approval | Personal-account metrics cover only posts published via Zernio. | `operational` (documented) |
| **GitHub public API** | Stars, forks, watchers, followers on `starshard-ai` org repos and the owner's public repos; issues/PRs/discussions opened by others | Public REST / GraphQL, no scraping | This is a first-party *follow-through* sensor (F), not a reach sensor. | `operational` |
| **Our own anchor pages** | Which post a visitor came from, via a per-post query tag on the anchor URL (e.g. `?src=<packet-id>-<platform>`) | We own the pages | **GitHub Pages provides no server logs.** Counting tagged visits needs a privacy-respecting counter (self-hosted or a no-cookie service). None exists today. Until then, tags only help when a visitor *pastes the tagged URL back to us*. | `OPEN-Q` (Q4) |
| **Owner first-party intake** | Email replies, GitHub issues, public Hub-facing mentions digest (Overheard seat) | Existing intake | The definitive QSC (F) sensor. Requires the owner or a frontstage agent to tag a reply as "from packet X". | `operational` (intake exists); `design_hypothesis` (tagging discipline) |

### 3.2 What Zernio actually returns per platform (verified against Zernio docs, 2026-09-19)

| Platform | Impressions | Reach | Likes | Comments | Shares | Saves | Clicks | Views |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| X | yes | no | yes | yes | yes | no | yes | yes |
| LinkedIn | yes | yes | yes | yes | yes | personal only | org only | video only |
| Threads | yes | no | yes | yes | yes | no | no | yes |
| Bluesky | no | no | yes | yes | yes | no | no | no |
| YouTube | no | no | yes | yes | yes* | no | no | yes |
| Reddit | no | no | yes | yes | no | no | no | no |
| Telegram / Discord / Slack | none | none | none | none | none | none | none | none |

Consequence: **no platform in our set exposes dwell time or read-through** (only YouTube exposes retention-like data). "Dwell" in the mission statement is therefore not a signal we can have compliantly. Impressions and replies are the closest proxies. `operational`

### 3.3 Forbidden (fail-closed)

- Scraping any platform's web or mobile surface, including logged-in browser automation for reading or posting.
- Unofficial / reverse-engineered mobile or private APIs.
- Credential stuffing, cookie export, session sharing, or any login not performed by the owner via the platform's own OAuth flow.
- Third-party "growth" collectors, engagement pods, follow/unfollow automation, purchased engagement.
- Sending DMs / private replies from the engine (Zernio's private-reply endpoint exists; we do not call it).
- Profile enrichment of responders: no scraping bios, follower lists, employer, location; no cross-platform identity resolution. The ledger holds a public handle + the public reply URL + our own S/R/F judgment and nothing else.
- Any collection on Xiaohongshu or WeChat.

Any packet, tool, or script that needs a forbidden source is rejected at the PCSE gate, not debated. `operational` (extends existing PCSE predicates)

---

## 4. System bite — Hub + dual-plane + Outreach-PCSE

### 4.1 Who does what

| Role | Seat / plane | Reads | Writes | Never |
|---|---|---|---|---|
| **Drafts** | Outreach seat (Grok, shared cloud VM) — context plane | Hub: standing, reward cards, connection ledger (public slice), prior packets | Content packet (existing `cp-YYYY-wNN-NN` schema) **plus one `hypothesis` field** naming which reward-card feature this packet tests | Holds fleet SSH keys; publishes without packet + PCSE; reads any forbidden source |
| **Gates** | PCSE check (Clean-Content + secrets scan, existing) → owner go/hold (≤5 lines, existing) | Packet | `pcse-ship/v0` receipt (existing schema) | Passes a packet whose hypothesis needs a forbidden signal |
| **Publishes** | Whoever holds the Zernio credential — **execution plane** | Packet with `owner_ack: go` | Zernio schedule/publish call; `outreach-receipt` with live URLs after HTTP 200 (existing) | Publishes a packet without `owner_ack: go` and a PCSE pass; auto-replies to anyone |
| **Observes** | Same credential holder, T+72h and T+14d | Zernio analytics + inbox comments; Bluesky public AppView; GitHub public API; owner intake tags | `connect-observation/v0` memo per post (numbers + public reply URLs, no enrichment) | Reads anything outside §3.1 |
| **Judges QSC** | Human (owner or frontstage human-in-loop), assisted by an AI reading only the public reply text | Observation memo | `connection-ledger/v0` entry: handle, reply URL, S/R/F flags, packet id | Rates a person's *worth*; stores private data |
| **Learns** | Cloud Fable / Adam lane (analysis) | All observations + ledger over the window | `reward-card/v0` per platform, claim-typed, with confidence; weekly | Publishes; touches credentials; states a card feature as fact without the `operational` tag |
| **Decides** | Owner | Weekly ≤5-line result; the ledger when curious | go/hold; connects/disconnects platforms; answers OPEN-QS | Is asked to pick tactics (Outreach decides week tracks autonomously — existing standing) |

Dual-plane preserved: the shared Grok VM reads Hub and drafts; it holds no fleet keys. `operational` (fleet-reachability ADR)

**Credential location, honestly stated.** As of week 38 the Outreach seat reported "Zernio MCP connected, accounts empty". A Zernio API key is a vendor-scoped posting credential, not a fleet key, so it does not violate the ADR's letter; it does widen the blast radius of the shared VM to "can post as the owner". The target shape under this brief is: **read-only analytics may be pulled from wherever the key already is; the publish call should run on the execution plane (Mac/fleet frontstage) or at minimum require `owner_ack: go` in the packet as a hard precondition the MCP caller checks.** Which of these the owner wants is `OPEN-Q` (Q3).

### 4.2 Data flow (one loop)

```
Hub: reward cards + ledger + standing
        │ read
        ▼
Outreach drafts packet (+hypothesis) ──► PCSE gate ──► owner go/hold (≤5 lines)
                                                              │ go
                                                              ▼
                                        execution plane publishes via Zernio (OAuth)
                                                              │ HTTP 200
                                                              ▼
                                        outreach-receipt: live URLs ──► owner (result-only)
                                                              │
                              T+72h / T+14d                   ▼
                    Zernio analytics + inbox comments; Bluesky public AppView;
                    GitHub public API; owner intake tags  ──► connect-observation/v0
                                                              │
                                                              ▼
                              human judges S/R/F ──► connection-ledger/v0 (public handle + URL only)
                                                              │
                                                              ▼
                              Cloud Fable / Adam ──► reward-card/v0 per platform (claim-typed)
                                                              │
                                                              └──► back to Hub
```

### 4.3 Hub objects (schemas, v0)

All are Hub memos with tags; no new store. Field lists are minimal on purpose.

**`content-packet` (existing) — one added field**

```
hypothesis: "<platform>: <reward-card feature> → expect <direction> in <signal>"   # exactly one; may be "none (baseline)"
anchor_tag: "<packet-id>-<platform>"                                                 # appended as ?src= on anchor URLs
```

**`connect-observation/v0`**

```
schema: connect-observation/v0
packet_id: cp-YYYY-wNN-NN
platform: bluesky | linkedin | threads | x | ...
post_url: <public URL>
observed_at: <ISO8601>            # T+72h or T+14d
metrics: { impressions?, reach?, likes, comments, shares, clicks?, views? }   # only fields the platform returns; absent ≠ 0
public_replies: [ { url, handle } ]   # text is read, not stored
first_party_hits: [ { channel: email|github|hub-public, ref } ]  # refs are ours, not theirs
source_of_truth: zernio | bsky-public-appview | github-api | owner-intake
```

**`connection-ledger/v0`** (one entry per candidate QSC)

```
schema: connection-ledger/v0
packet_id, platform, reply_url, handle
S: true|false   R: true|false   F: true|false|pending(until <date>)
judged_by: owner | <frontstage role>
note: ≤140 chars, about the idea they raised, not about the person
```

**`reward-card/v0`** (one per platform, rewritten weekly)

```
schema: reward-card/v0
platform: ...
window: <from>..<to>   posts_in_window: N
features:
  - claim: "reply-first threads out-impress link-first posts"
    type: operational | design_hypothesis
    confidence: 0.0-1.0
    evidence: [ packet ids ]
qsc_per_post: <number or "n/a">
next_hypothesis: "<one line>"
```

`design_hypothesis` for all four schemas; they are proposals, not standings, until the owner accepts (Q1).

### 4.4 Cadence

Matches the existing weekly Outreach loop (one packet Tue–Fri, ≤5-line go/hold, owner attention ~60 s/week). The engine adds: one observation pass at T+72h, one at T+14d, one card rewrite per week. Owner attention target unchanged. `operational` (cadence exists) + `design_hypothesis` (added passes fit inside it)

---

## 5. MVP — the thinnest loop that can improve connection quality

**Scope:** 2 platforms, 1 packet per week, 4 weeks, zero new infrastructure beyond Hub memos.

**Platform choice (proposed, owner decides in Q5):** Bluesky (Class A, public AppView, cheapest and most inspectable) + LinkedIn (Class B, where same-frequency professionals are, and where Zernio returns reach). X is deferred because connecting it through Zernio currently requires a payment method and its API is pay-per-use. Threads is a reasonable substitute for LinkedIn if LinkedIn OAuth stalls.

**Preconditions (all currently unmet; none the engine can do itself):**
1. Owner completes Zernio OAuth for the chosen platforms (accounts list was empty at week 38).
2. Q1–Q3 answered.

**Loop, per week:**
1. Outreach drafts one packet from standing content, with exactly one `hypothesis`; anchor URLs carry `?src=<packet>-<platform>`.
2. PCSE gate → owner go/hold.
3. Execution plane schedules both variants via Zernio; receipt with live URLs after HTTP 200.
4. T+72h: observation memo per post (Zernio metrics + inbox comments; Bluesky public AppView for likes/reposts/thread).
5. T+14d: second observation; human judges S/R/F for each public reply and any first-party hit; ledger entries written.
6. Cloud Fable / Adam rewrites the two reward cards; proposes next week's hypothesis.

**Week-1 hypothesis (proposed):** RQ3 — anchor link in first post vs in first reply, same text otherwise, on both platforms. It is the cheapest admission test and cannot be gamed. `design_hypothesis`

**What "improvement" means at this N:** not statistical. Improvement = (a) at least one ledger entry with S∧R∧F by week 4, and (b) reward cards whose features have moved from `design_hypothesis` toward `operational` on at least one platform, and (c) owner reads the ledger and says these are the kind of people. If (a) is zero after 4 weeks with ≥8 posts, the selection lever (what we say) is the problem, not admission; pivot the packets, not the tactics. `design_hypothesis`

**Explicitly not in MVP:** A/B tooling; dashboards; automated posting cadence; replies of any kind by agents; a web-analytics counter on the anchor pages (Q4); X; any platform the owner has not OAuth-connected.

---

## 6. Failure modes and kill switches

| # | Failure mode | Early signal | Kill switch (who pulls) |
|---|---|---|---|
| F1 | **Goodhart drift** — engine starts optimizing impressions; packets get punchier and emptier | Reach rising ≥2 consecutive weeks while ledger S∧R∧F count is flat or zero | Reward cards may not carry a `next_hypothesis` about reach alone; Cloud Fable flags; Outreach reverts to baseline packet (owner not needed) |
| F2 | **Platform enforcement** — warning, rate limit, shadow restriction, or mute on any connected account | Any platform notice; Zernio post status errors; sudden zero impressions across posts | Freeze that platform immediately (Outreach or credential holder); no re-enable without owner. The Xiaohongshu mute is the precedent. |
| F3 | **Credential blast radius** — shared VM can publish as owner | Any publish without `owner_ack: go` and a PCSE receipt | Publish call refuses when precondition missing (fail-closed in the caller); owner may revoke the Zernio key from the Zernio dashboard at any time (Q3) |
| F4 | **PII creep in the ledger** — someone adds bios, employers, follower counts, or cross-platform matches | Any ledger field not in the v0 schema | Ledger entries are Hub memos; frontstage deletes the field on sight; a PR to this file is required to add fields |
| F5 | **Agent replies to people** — an agent posts a public reply or DM on the owner's behalf | Any Zernio reply / private-reply call from an agent | Hard rule: agents draft replies into Hub for a human to send; no exceptions in v0 (Q6 asks whether to loosen) |
| F6 | **Cadence spam** — more than one post per platform per day, or posting to fill a schedule | Packet count > 1/week without an owner-stated reason | Existing standing: typed packet required, no free-form; cap 1 post/platform/day |
| F7 | **Over-confident cards** — a `design_hypothesis` gets quoted externally as fact | Any external slice citing a card feature not tagged `operational` | Outreach slices doc is the only external source; anything not in it is not sayable |
| F8 | **Owner attention overrun** — engine starts asking for tactical decisions | More than the ≤5-line weekly result reaching the owner | Outreach decides week tracks autonomously (existing standing); escalate only irreversible acts |
| F9 | **Compliance scope creep** — a "just this once" scrape or browser automation to fill a data gap | Any tool/script touching a source not in §3.1 | Rejected at PCSE, not debated. Data gaps go to OPEN-QS, not to workarounds. |
| F10 | **Wrong telos check** — after 8 weeks the ledger is full of consumers, not collaborators | Owner reads ledger and does not recognize the people | Owner call (RQ6): either change what we say, or stop; the engine does not get to redefine QSC downward |

---

## 7. Explicit non-goals

- **Xiaohongshu / 小红书** and **WeChat** — out of scope; abandoned by owner; also the clearest example of the compliance failure this brief forbids.
- Growth: follower counts, "reach targets", posting frequency targets.
- Paid distribution of any kind (Zernio offers ads; we do not use them).
- Any automated interaction with people: DMs, private replies, auto-replies, follow/unfollow, tagging.
- Building or hosting our own recommender or feed generator (possible on Bluesky; deferred; not a v0 lever).
- Cross-platform identity resolution of strangers; profile enrichment; audience segmentation of individuals.
- Reverse-engineering any ranking model beyond what the platform publicly returns about our own posts.
- Dwell / read-through measurement — not compliantly available; not pursued by proxy hacks.
- A dashboard, an analytics database, or any service beyond Hub memos, in v0.
- Making the engine the owner's voice: it drafts and observes; the owner remains the only person who speaks to a person.

---

## 8. Disconfirming tests for the design hypotheses

| Hypothesis | Disconfirming observation | Consequence |
|---|---|---|
| Two-lever split (admission vs selection) is enough | After 4 weeks, changing admission features moves reach but QSC never moves, *and* changing what we say does not move QSC either | The bottleneck is upstream of posting (the anchor content itself); pause engine, fix anchors |
| Reply text alone is enough to judge Substance | Two independent judges disagree on S for >30% of replies | Tighten the S rubric with examples; do **not** add profile signals |
| Reward cards can be learned at N≈4/month | After 8 weeks no card feature has moved to `operational` with confidence ≥0.7 | Accept cards as priors only; stop pretending to learn; run on doctrine + owner taste |
| Bluesky is the most informative Class A sensor | Zero QSCs from Bluesky over 8 weeks while LinkedIn/Threads produce some | Drop Bluesky from MVP; keep public-AppView method for whatever Class A platform replaces it |
| Anchor tags help attribution | No first-party hit ever arrives with a tag over 8 weeks | Tags are inert without a counter (Q4); either fund a counter or drop tags |
| Weekly cadence fits inside existing owner attention | Owner receives more than the ≤5-line result in any week | Engine passes are moved to biweekly; result stays ≤5 lines |

---

## 9. Hub standing titles referenced (no ids in this public file)

- Outreach seat standing: outbound discoverability loop; week-track autonomy; result-only reporting.
- Public dissemination doctrine: attract-not-chase, recommendation-engine routing.
- Fleet reachability ADR: dual-plane; no keys on shared Grok VM (public copy: `docs/FLEET-REACHABILITY-ADR.md`).
- PCSE cleared-surface + ship receipt (`pcse-ship/v0`).
- Content packet schema (`cp-YYYY-wNN-NN`) and `outreach-receipt`.
- Xiaohongshu abandonment ruling (2026-09-06) and the earlier "no Android notification aggregation for XHS/WeChat" ruling.
- Social-platform signal-quality runway ("score signal quality beyond vanity metrics").

Companion files: `CONNECT-ENGINE-OUTREACH-SLICES.md` (what may be said externally), `CONNECT-ENGINE-OPEN-QS.md` (owner go/no-go; silent = no-go).
