# Owner go/no-go — connect 引擎

**规则：** 每题回 `go` 或 `no-go`（可附一行条件）。**不回 = no-go。** 没有「再想想」选项；想再想就是 no-go，随时可重开。
**来源：** `docs/CONNECT-ENGINE-BRIEF.md`。每题标注它解锁哪一节、no-go 的默认后果。
**不问的事：** 具体发什么内容（Outreach 自决）、具体回应哪个人、任何产品代码、任何平台的具体排序机制。

| # | 问题 | go 意味着 | no-go 的默认（也是安全的） | Brief § |
|---|---|---|---|---|
| **Q1** | 是否接受 §4.3 的四个 Hub 对象为 standing：content packet 加一个 `hypothesis` 字段、`connect-observation/v0`、`connection-ledger/v0`、`reward-card/v0`？ | Outreach 从下一个 packet 起带假设；观察、ledger、card 开始在 Hub 里写；字段只能通过本仓库 PR 增加。 | 引擎停留在 brief。Outreach 继续按现有 packet 周循环发帖，不做观察、不写 card。 | §4.3, §5 |
| **Q2** | Zernio Analytics add-on：是否由你去 Zernio 后台确认现有套餐是否含 analytics，若不含则决定是否付费开启？（这是一笔支出，agent 不碰。） | 拿到 daily metrics、follower stats、post timeline（唯一的「互动速度」传感器）。per-post analytics 是否也需要 add-on 一并确认。 | 引擎只用无 add-on 也能拿到的东西：Zernio inbox 评论、Bluesky 公开 AppView、GitHub 公开 API、你的收件箱。没有 velocity、没有 follower 序列。card 更薄，但不违规。 | §3.1 |
| **Q3** | Zernio 发布凭证放哪？ **A** = 发布调用移到执行面（Mac/fleet 前台），Outreach 只起草 + 只读分析；**B** = 维持 Outreach 席位现有的 Zernio MCP，但发布调用必须在 packet 里读到 `owner_ack: go` + PCSE 通过才执行（fail-closed）。回 `go A` 或 `go B`。 | 对应形态成为 standing；任何不满足前置条件的发布调用视为违规并触发 F3。 | 引擎不经任何 agent 发布。你自己在 Zernio 后台按发布；agent 仍可起草和观察。 | §4.1, §6 F3 |
| **Q4** | 是否在 anchor 页面（spine / pipeline）加一个不设 cookie、不存 IP 的访问计数（自托管或同类服务），用来统计带 `?src=` 标记的访问？（涉及少量支出 + 你对自己页面的隐私立场。） | `anchor_tag` 变成真传感器：能看到哪篇帖、哪个平台把人带到了页面。 | 标记继续加（无害），但只有当对方把带标记的链接发回给我们时才有用。归因主要靠你的收件箱和 GitHub。 | §3.1, §8 |
| **Q5** | MVP 平台：Bluesky + LinkedIn（你需要在 Zernio 完成这两个平台的 OAuth；LinkedIn 卡住则用 Threads 替代）。X 暂缓（需在 Zernio 绑支付方式，且 X API 按量计费）。 | 4 周、每周 1 个 packet × 2 个平台变体；第一周假设 = 「anchor 链接放正文 vs 放首条回复」。 | 没有平台可发，引擎无法启动；brief 保留待用。 | §5 |
| **Q6** | 是否允许 agent 在**你逐条批准后**代发**公开**回复（不含任何私信）？ | 每条回复仍由人批准，但按发的动作由执行面完成；ledger 记录「我们回过」。 | v0 硬规则：agent 只把回复草稿写进 Hub，由你手动发送。任何 agent 发起的回复/私信调用视为 F5。 | §4.1, §6 F5 |
| **Q7** | QSC 判定分工：**go** = AI 只读公开回复文本判定 S（实质性），你只判定 F（是否进入了你的收件箱/GitHub），R 由 agent 按「是否我们先招惹」机械判定；**no-go** = 三项都由你判。 | 你每周看 ledger 的时间控制在 ≤5 行结果之内；S 的判定出现分歧 >30% 时按 §8 收紧规则。 | 你自己逐条判 S/R/F。更准，但每周多花几分钟，且和「result-only」有张力。 | §4.1, §8 |
| **Q8** | 是否允许 Outreach 按 `CONNECT-ENGINE-OUTREACH-SLICES.md` 的等级对外发这组切片（不升级等级、不带数字、不点名任何平台或任何人）？ | Outreach 可排期；每条按「running practice / design intent」标注发。 | 全部切片不外发；brief 只在 Hub 与本仓库内流转。 | Outreach slices |

**依赖关系：** Q1 是根——Q1 no-go 时 Q2/Q4/Q7 无意义。Q5 依赖你完成 OAuth。Q3 决定任何东西能不能经 agent 发出，独立于 Q1。Q2 与 Q4 都是支出，各自独立。Q6/Q8 独立。

**8 周后一定会问你的一件事（现在不用答）：** 看一遍 ledger 里的人——像一起做事的人，还是像观众？这是 RQ6，只有你能答；答案决定引擎是改内容、还是停。

**已拒绝、不再问：** 小红书、微信；任何爬取 / 非官方客户端 / 借登录态；付费投放；自动私信、自动回复、关注/取关；自建推荐系统或 feed generator（v0）；对陌生人做身份归并或资料补全；把粉丝数或曝光当目标；为此建仪表盘或新服务。
