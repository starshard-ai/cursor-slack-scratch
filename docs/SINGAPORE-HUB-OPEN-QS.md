# Owner go/no-go — Singapore hub + heavy harness

**规则：** 每题回 `go` 或 `no-go`（可附一行条件）。**不回 = no-go。** 没有「再想想」选项；想再想就是 no-go，随时可重开。
**来源：** `SINGAPORE-HUB-BRIEF.md`、`SINGAPORE-HUB-MESH-CHECKLIST.md`、`SINGAPORE-HEAVY-HARNESS.md`。
**不问的事：** 具体私钥、具体地址、具体美元数字（你自己在厂商后台设上限）、任何「把钥匙拷到 Eden 云机」。

**建议默认（Fable）：** Q1 go · Q2 no-go（先用现有枢纽公钥）· Q3 no-go（Pro 延后）· Q4 go A（Cursor CLI 先）· Q5 go（你设上限，agent 不填数字）· Q6 go（Always require approval）· Q7 no-go（claims 先关）· Q8 go（双平面红线重申）。

| # | 问题 | go 意味着 | no-go 的默认（也是安全的） | 解锁 |
|---|---|---|---|---|
| **Q1 钥匙分发** | 是否现在把新加坡枢纽**公钥**授权到 **seoul** 和 **bangkok-mini**？（tokyo/rescue 已通；只追加公钥一行，私钥不离开新加坡。） | Mac/Adam 按 checklist §3 做；P0 验收要这两台 `BatchMode=0`。 | 枢纽只保证 tokyo。seoul/bangkok 保持 `Permission denied`。Computers 跳板不受影响。 | Brief §3, checklist §3 |
| **Q2 哪一把钥匙** | 是否先 `ssh-keygen` 一把**专用** `id_ed25519_sg_hub`，再授权？回 `go` = 专用钥匙；`no-go` = 先用新加坡现有 `id_ed25519`（今天打通 tokyo 的那把）。 | 新身份、更干净的库存；checklist 用 `-i` 专用文件。 | 不新造钥匙，避免两把同时半授权。tokyo 已通的那把继续当枢纽身份。 | Brief §3, checklist §2 |
| **Q3 Pro** | 是否把 **Pro**（现离线 / 超时）算进 v0 必须打通？ | 主机在线后按 checklist 授权；P0 可以等它。 | **v0 不含 Pro。** 不挡 seoul/bangkok/harness。主机醒了再开一题。 | Brief F6, checklist §1 |
| **Q4 先装哪个 harness** | 新加坡交互重型编码的第一工具。回 **`go A`** = Cursor CLI（`agent`）；**`go B`** = Codex 交互优先；**`go C`** = OpenCode 优先。`no-go` = 本周不装。 | 按 harness 笔记 §3 只装选中的那一个作交互默认；Codex **登录**（给 poller）仍建议同日做，除非你写「登录也延后」。 | 不装新 CLI。Cloud Agent 继续做公开 PR。poller 保持 claims=off。 | Harness §2–§3 |
| **Q5 花费上限** | 你是否在装/登录之前，自己在 Cursor / Codex（及若选了 C 的 OpenCode 供应商）后台设好用量或账单上限？**不要把数字回在这道题或公开 PR 里。** | Agent 才允许 `agent login` / `codex login` / OpenCode `/connect`。无上限数字写入 Hub 或 git。 | 不登录、不装会拉配额的工具。本 brief 停在设计。 | Harness §1, §5 |
| **Q6 Computers 审批** | 新加坡作为 Computer：Grok Bot「Execution on Local Computer」设为 **Always require approval**（或 Never）。禁止 Always allow。 | 每条 Eden local-exec 要你点头。避免共享对话席把常开枢纽当无审批跳板。 | 不把本 brief 当成「可以 Always allow」的授权。现状若已是 Always allow，视为未决风险，不扩大使用。 | Brief §2.3, F4 |
| **Q7 poller claims** | 是否打开新加坡 / seoul 的 `FLEET_CLAIMS_ENABLED`？（今天关闭；东京 Codex 未登录。） | poller 可领 Codex 工单。先有 Q4/Q5 的登录。 | **保持关闭。** 装 CLI ≠ 打开无人值守领单。 | Harness §3.2, §4 |
| **Q8 双平面红线** | 重申：即使新加坡枢纽打通，也 **禁止** 在共享 Eden/Grok VM 上装舰队私钥或把 Tailscale 当主跳板。 | 09-18 ADR 继续有效；新加坡是执行面，不是拷钥匙的借口。 | 本 brief 整份不升 standing；按 09-18 ADR 停在「Grok 只起草」。 | Brief §1, ADR |

**依赖：**

- Q8 是根。Q8 `no-go` = 整份 brief 不升 standing（仍可当设计稿读）。
- Q1 不依赖 harness。可以只打钥匙、不装 CLI。
- Q2 在 Q1 之前更好：先定用哪把公钥，再追加。
- Q4 依赖 Q5：没上限就不要 login。
- Q7 依赖 Q4/Q5 里 Codex 已登录，且 Q6 不是 Always allow。
- Q3 独立；默认 no-go。

**已拒绝、不再问：**

- 把 Air `~/.ssh` 整目录拷到新加坡或 Eden VM
- 把新加坡私钥拷到 Eden VM / 写进本仓库
- 用 Cursor Cloud self-hosted workers 当 Grok 达舰队的主路径
- 为了打通组网在 Eden VM 上自建反向隧道
- 把 Claude Code 当新加坡 MVP（本题的起因就是部分座位禁/挡它）
- 在公开文件里写具体美元、私钥、组网地址、machine id

**你回完之后谁干活：** 执行面（owner / Mac / Adam）跑 checklist 与安装。Cloud Fable / 本 Cloud Agent **不** SSH、**不** 代设账单、**不** 发明凭证。
