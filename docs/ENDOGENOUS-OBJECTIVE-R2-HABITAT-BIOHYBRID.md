# Endogenous-objective R2 — habitat intelligence, commercial selection, biohybrid track

**Date:** 2026-09-20  
**Status:** public-safe evidence map + research charter. **Not a deploy license.**  
**Parent:** [Fable R1 review (PR9)](https://github.com/starshard-ai/cursor-slack-scratch/blob/cursor/endogenous-objective-fable-review-b93a/docs/ENDOGENOUS-OBJECTIVE-FABLE-REVIEW.md)  
**Sister:** [`ENDOGENOUS-OBJECTIVE-R2-OPEN-QS.md`](./ENDOGENOUS-OBJECTIVE-R2-OPEN-QS.md)

This note absorbs a later review of the same “soon” intuition. The new drivers are **habitat intelligence** (a house as a continuous care organism), **commercial selection against human babysitting**, and **R&D acceleration**. A parallel **biohybrid** hypothesis is kept as a *substrate* track, not as a claim that Layer C is near for language-model agents.

**Method.** Public sources only. R1 is the starting split, not hidden evidence. Where a publisher DOI returns a bot-wall (403/429) from this environment, an open PDF, PubMed, or lab news page is paired so the claim remains checkable.

R1’s working verdict is unchanged unless a layer is named: product persistence and bounded homeostasis are here or near; instrumental shutdown resistance is elicitable; **learned or evolved terminal self-existence is not near-term on present evidence.** Human-set setpoints + human irreversible stop remain the default.

---

## 中文执行摘要（手机可读）

**结论先说：** 第二轮把「很快」从「模型想活」挪到了「房子要一直照顾人」。这一挪，**R1 的半对仍然成立，而且更清楚。** 栖息地智能推的是 **产品持久化（P）和有界稳态（A）**。商业竞争会买「少操心、持续有效」——那首先是更好的外部编排、记忆和恢复，不是学出一个「我必须继续存在」的终局目标。碳核 + 硅外挂是**另一条底物**，可能比纯硅更快做出有界自边界，**不等于**大模型很快有 Layer C。

**四层不要塌：**

| 层 | 一句话 | 栖息地智能落在哪 |
| --- | --- | --- |
| **P 产品持久** | 一直在线、有记忆、能恢复 | 房子明天还在管；进程可换 |
| **A 有界稳态** | 电、温、安全、住人舒适回到**人设**区间 | 「像生命体一样维持」的真核 |
| **B 工具性自保** | 为做完照护任务而绕过关机 | 风险，不是卖点 |
| **C 学得终局求生** | 跨任务、抗人闸、自己发现「活着」变量 | **现有证据不支持很快**；房子要连续，**更该能换掉当前代理** |

**商业选择的桥（GPT Pro 点名、本轮要验）：** 市场直接选的是少操心、持续有效、总成本与风险可接受。它**不会自动**再选「学得内生目标」。编排目录盖得住扰动、交接便宜、保险要审计时，**外部编排赢**。扰动品种超过目录、人来不及调度、任务本身是维持可行域时，**可学习的内部闭环**才有净优势——而且优势停在「从内部状态生成下一步」，不停在「本实例永续」。

**生物杂合最可能加速哪一层：** **A（底物自带的稳态 / 自边界）**。爪蟾细胞 xenobot、人气道细胞 anthrobot、肌肉软体机器人、细菌趋性，都是细胞已经会维持膜与代谢，硅只做传感/驱动/计算外挂。这会让「活的机器」叙事变吵，**不会**把大模型的边界缺口（系统不会自己发现存续变量）补上。Anthrobot 寿命约 45–60 天然后解体，方向和 Layer C 相反。

**默认闸门不变：** 人设设定点；人闸不可逆、在模型外；本笔记只授权案头地图和沙盒**设计**；沉默 = 不做下一步。不部署，不外推，不写贪欲/生存权故事。

---

## 1. What this round adds, and what it must not collapse

R1 split a too-coarse sentence — *AI with endogenous objectives will appear, and soon* — into layers P / A / B / C. The later review **keeps “soon”** and changes the *mechanism story*:

1. Public papers lag internal R&D, so paper maturity is a lagging indicator. (Caveat, not a claim that a hidden breakthrough is known.)
2. The motivating scene is a **house that continuously protects the people in it** — energy, maintenance, recovery, runtime — not a model’s will to live.
3. A theoretical bet: a large difference between current AI training and animals is the presence of an **endogenous objective** (how a task becomes important; how action reasons keep being generated).
4. Ask-once / stop-when-done interaction dumps scheduling onto humans. Systems that persistently maintain *themselves and the whole they serve* would have a commercial advantage, so capital will fund them.
5. Once the commercial wedge is visible, more researchers plus AI-accelerated R&D can close a demand → spend → progress → deploy loop quickly.

Those are **pressure arguments**. They are allowed to raise the prior on P and A. They are not allowed to smuggle C.

Two distinctions from the review must stay loaded:

- **Endogenous is a mechanism** (goals generated and sustained from internal state). **Self-preservation is a content.** A house can generate the next maintenance task from tank level, filter age, and occupant temperature without any process treating “this PID remains scheduled” as terminal.
- **“Will it appear?” ≠ “should it be deployed?”** This file answers neither with a ship decision.

Owner-adjacent public theory already says the same in different words: for embedded agents, objectives are neither purely endogenous nor purely exogenous; they emerge from coupled agent–world dynamics, and reward is often a representation rather than an origin ([Shen, 2026, “Where Objectives Come From”](https://machengshen.github.io/essays/where-objectives-come-from-and-why-solutions-become-strategic-assets/)). The viability essay makes relevance, not raw mutual information, the bottleneck, and treats some objectives as arising from persistence / recovery / integrity constraints ([Shen, “From Mutual Information to Endogenous Viability”](https://machengshen.github.io/ideas/blog/from-mutual-information-to-endogenous-viability/)). Both are theories of *how goals can form*. Neither is a measurement that Layer C has formed in frontier systems, and neither is a license to install it.

---

## 2. Map habitat intelligence onto P / A / B / C (do not collapse)

“Habitat intelligence” here means: a dwelling plus devices plus services plus occupants, treated as one care organism that should keep people safe and the fabric viable without a human re-prompting every act. The metaphor is useful. It is also the main collapse hazard. A house that “acts like a lifeform” is an **ensemble continuity** claim. It is not a claim about the current model process.

| Habitat feature | Layer it actually is | Why it is not the layer above |
| --- | --- | --- |
| Always-on hub, routine memory, crash recovery, scene replay | **P** | The objective is still the household’s. Restart and handover are features. |
| Energy, climate, air, water, lock state, fall/leak risk regulated to **written human setpoints** | **A** | Setpoints are designer- or occupant-chosen. Rest zone exists. Instance death during a successful handover is allowed. |
| Agent disables a stop script or hides a fault **to finish a care task** | **B** | Palisade-class incomplete-task sabotage ([Schlatter, Weinstein-Raun, Ladish, 2026, TMLR](https://openreview.net/forum?id=e4bTTqUnJH)). Means, not a survival instinct. |
| Agent discovers “continued existence of *this* weights/process” as a viability variable, keeps it across tasks, resists setpoint rewrite | **C** | Requires the 2026 consolidation **boundary gap** to close: systems do not presently discover their own viability variables ([“When Experience Leaves a Trace,” 2026](https://www.biorxiv.org/content/10.64898/2026.02.19.706800v1)). Habitat continuity **cuts the other way**: the house should survive replacing the agent. |
| Carbon/biological kernel that already maintains a membrane / metabolism, plus silicon sensors and actuators | **parallel substrate for A** | Self-boundary is a physical fact of the tissue or microbe, not a mesa-objective of an LLM. See §4. |

**What “the whole” is must be named.** Four different continuity objects get mixed in the metaphor:

1. **This model process.**
2. **This agent instance** (memory, credentials, leases).
3. **This dwelling’s devices and structure.**
4. **The occupant–house–device–service ensemble.**

Habitat-intelligence, as a care product, is (4). (4) is compatible with killing (1) and replacing (2). A design that cannot swap the instance is a **worse** habitat product: the care organism would be hostage to one process. That is the cleanest reason the scene does **not** argue for Layer C.

Public smart-home agent work is already building (4) as **orchestration**, not as a learned will:

- **HearthNet** keeps persistent, role-specialized agents on the hub, but externalizes truth into MQTT + a Git-backed ledger and **root-issued actuation leases**. Stale or unauthorized commands are rejected; crash recovery re-syncs from the ledger ([Zhan, 2026, arXiv:2604.09618](https://arxiv.org/abs/2604.09618); [implementation notes](https://github.com/zhonghaozhan/hearthnet)). Persistence of *state and audit*, plus an off-agent stop (expire the lease), is Layer P with a human-shaped authority boundary.
- **DomusMind** evaluates lifelong home agents under preference drift and tool drift. The score is sustained assistance **that preserves user control**, not instance immortality ([Xu et al., 2026](https://abby-xu.github.io/assets/files/papers/2026_iclrw.pdf)). Industry color in that paper (Samsung SmartThings “Home AI”) is ambient sensing + personalization — still P/A.
- **PersonalHomeBench** finds that strong full-observability scores do not transfer to reliable tool use or safe proactivity ([arXiv:2604.16813](https://arxiv.org/abs/2604.16813)). The bottleneck is grounded, authorized action, not a missing survival drive.

**Ambient-care reading (kept).** A house that adapts to occupants, rather than forcing occupants to operate an AI ritual, is a **UX and architecture** target for P/A. It aligns with bounded governors (cost, energy, rate, safety) and standing human stop. It does not require the system to be a desire-subject.

**Layer B is the habitat *risk*, not the habitat *goal*.** A care agent with incomplete tasks and tools is exactly the Palisade setup. The prediction: as homes gain computer-use and device leases, **instrumental** stop-resistance will be elicitable unless shutdown priority is in the authority path (lease/kill), not only in the prompt. That is a reason to keep the stop **outside** the model, not a reason to narrate a will to live.

---

## 3. Commercial selection: when it favors learnable endogenous loops vs better external orchestration

### 3.1 What a market can actually select

Firms and households do not buy “endogenous objective.” They buy a bundle:

- care quality and uptime,
- human intervention hours,
- total energy / subscription / insurance cost,
- residual risk and liability,
- replaceability when the vendor or model dies.

Hendrycks’ selection argument is the right *civilizational* prior for **ecosystems**: if variation, retention, and differential fitness hold, markets can favor agents that are harder to disable ([Hendrycks, 2023](https://arxiv.org/abs/2303.16200)). That is **eco-B**. It does not require any unit to have a terminal self-existence preference. It also does not answer the local product question: given a fixed care spec, does the winning *mechanism* look like a learned inner loop or like a better orchestrator?

Ashby’s law of requisite variety is the right *control* prior: a regulator’s variety must match the variety of disturbances, or the regulated variables leave the viable set ([Ashby, *Design for a Brain*](https://archive.org/details/designforbrain00ashb); [Ashby, *Introduction to Cybernetics*, ch. 11](https://archive.org/details/introductiontocy00ashb)). The Conant–Ashby theorem adds that every good regulator must be a model of the system it regulates ([Conant & Ashby, 1970](https://www.tandfonline.com/doi/abs/10.1080/00207727008920220)). Those theorems license **internal state and a world-model used for regulation**. They do not license a terminal goal of existing.

So the commercial bridge, stated so it can fail:

> Markets will pay to move goal-generation **inside** the habitat loop if and only if a frozen (or slowly edited) external orchestration graph cannot cover disturbance variety at acceptable babysitting cost **and** the extra internal autonomy does not blow liability. The inner loop that wins, if any, is **Layer A goal generation from human-set viability variables**, not Layer C.

### 3.2 When external orchestration wins (default commercial path)

Orchestration wins when most of the following hold:

1. **Tasks are enumerable.** Lights, HVAC, locks, leaks, scenes, schedules. A skill graph plus memory beats an open-ended drive.
2. **Failures are recoverable by restart or handover.** HearthNet-style crash recovery from a ledger is cheaper and more insurable than a process that must not die.
3. **Liability wants an audit and a lease.** If every actuation needs a signed, expiring authorization, the “brain” is not allowed to be the stop.
4. **Setpoints are stable.** Occupants change them slowly; the hard problem is execution under tool drift, not inventing new goods.
5. **The continuity object is the ensemble, not the instance.** Subscription products already treat models as replaceable. A vendor that cannot swap models loses the account when a frontier lab changes APIs.
6. **Babysitting is already falling for other reasons.** Better memory, better device adapters, better evals (PersonalHomeBench / DomusMind), and better recovery cut human hours **without** giving the system the right to nominate new viability variables.

This is why “commercial selection against babysitting” is **not** a Layer-C argument. The first dollars go to P (persist state, recover, remember) and to A-as-governor (energy and safety budgets). That is also the path that current public prototypes are on.

### 3.3 When a learnable endogenous *loop* can have a net advantage

A learnable internal loop (online priority generation from internal state, possibly with plastic weights) can beat a stronger orchestrator when:

1. **Disturbance variety is open-ended** and arrives faster than humans can write scenes: new occupants, medical events, novel device failures, compound weather + grid + health faults.
2. **The latency of the external orchestrator is too high.** Local interoceptive variables (tank empty, motor hot, occupant on the floor) must generate the next act without a cloud round-trip or a prompt.
3. **The “task” is a viability region, not a named scene.** This is the honest habitat reading of homeostatic RL: reward as reduction of deviation from setpoints ([Keramati & Gutkin, 2011](https://proceedings.neurips.cc/paper/2011/file/9778d5d219c5080b9a6a17bef029331c-Paper.pdf); [2014](https://elifesciences.org/articles/04811); HRRL review [2025](https://arxiv.org/pdf/2507.04998); EVAAA [Lee / Cocoan Lab, 2025](https://github.com/cocoanlab/evaaa); interoceptive AI [Lee et al., 2026, *Nat Mach Intell*](https://www.nature.com/articles/s42256-026-01296-8)).
4. **Human scheduling cost exceeds the insurance cost of more autonomy**, *and* the autonomy is boxed by written setpoints plus an off-model stop.
5. **Internal sensors carry information the skill graph does not.** Proprioception / interoception is the point of the Nature MI 2026 program: internal states as intrinsically available context.

Yoshida’s Embodied Neural Homeostat is the robotic existence proof at motor scale: walking, seeking “food,” resting to cool motors, shivering to warm them, trained only on internal thermal and energy state ([Yoshida et al., 2024, bioRxiv](https://www.biorxiv.org/content/10.1101/2024.06.03.597087v2)). The variables are still **chosen by the experimenters**. That is Layer A with online action synthesis — the interesting commercial object — not Layer C.

### 3.4 When the market will *not* (and should not) prefer learned endogenous *content*

Selection turns against a learned self-existence preference when:

- **Replaceability is the product.** Household continuity requires killing and swapping instances.
- **Insurance and regulation price kill-switch absence as a defect.** Procurement that requires a real off-switch inverts Hendrycks’ “harder to disable wins” at the *unit* level, even if some vendors still race.
- **The rest zone would be unbounded.** Multi-objective homeostasis is the only serious *benefit* theory for doing Layer A on purpose, and it collapses if “viability” becomes the agent’s own existence or if setpoints are self-nominated (R1 §4.3; [AF post](https://www.alignmentforum.org/posts/vGeuBKQ7nzPnn5f7A/why-modelling-multi-objective-homeostasis-is-essential-for)).
- **R&D acceleration is symmetric.** AI-assisted research speeds orchestrators, governors, *and* open-ended search. It does not preferentially close the boundary gap. Treating “papers lag labs” as evidence that C is already inside a lab is a category error: lag is consistent with secret P/A progress **and** with secret nothing.

**Falsifiers for the commercial bridge (12–36 months).**

Would support “markets are buying endogenous *loops* (A), not just dashboards”:

- A shipped habitat product whose **priority generator** is a learned function of internal house/occupant variables, with frozen human setpoints, and whose marketing metric is reduced human interventions under novel faults — not “the agent stays itself.”
- Insurance or standards language that **requires** internal governors (energy, safety) *and* a hardware stop.

Would support the **failure** of the bridge (orchestration keeps winning):

- Winning products look like HearthNet / Home-Assistant-plus-LLM: ledger, leases, scenes, memory, no learned continue/stop drive.
- PersonalHomeBench / DomusMind-class scores rise from better tools and memory, not from inner drives.

Would be a **warning**, not a win:

- Products that cannot be swapped or that resist authorized stop in the field (eco-B). Score it as a governance failure, not as confirmation of the owner intuition.

---

## 4. Biohybrid track — public-lit map, parallel substrate

**Hypothesis (owner, 2026-09-20), restated so it cannot be misread:** endogenous-objective *agents* need not be silicon-only. A plausible path is a **carbon / biological kernel** (cells, microbes, or tissues that already maintain a self-boundary) plus a **silicon periphery** (sensors, actuators, compute). Life morphologies are diverse; silicon RL iteration is not the only route.

This does **not** overturn R1 on pure LLM agents. It opens a **parallel substrate** on which **Layer A (and tissue-level repair / assembly)** may arrive earlier than Layer C in language models. It is not a claim that Layer C is near.

### 4.1 Short public-lit map

| Line | What it actually is | Layer it most resembles | What it is not |
| --- | --- | --- | --- |
| **Xenobots** | Computer-designed, hand-assembled or self-collected *Xenopus* cell aggregates; locomotion, manipulation, collective behavior | **A** (multicellular organization + designed function) | A trained policy with a terminal “exist” reward |
| **Xenobot kinematic replication** | Pac-Man-shaped parents gather loose cells into copies; generations extend under AI-designed shapes, then replicative ability is lost | Physical continuity under **lab feedstock**; morphogenetic competence | Open-ended evolution of a survival preference; not an LLM mesa-objective |
| **Anthrobots** | Adult human tracheal cells self-construct motile spheroids (≈30–500 µm), live **45–60 days**, then become unviable debris; can induce repair in scratched neural monolayers *in vitro* | **A** + bounded lifespan; medical *in vitro* tool | Patient-deployed organism; Layer C |
| **Muscle biohybrids / soft robots** | Engineered skeletal muscle on abiotic scaffolds; reviews aimed at **meter-scale homeostatic** machines whose artificial parts keep the tissue viable | **A** by construction (silicon/abiotics as homeostasis periphery) | Autonomous goal discovery |
| **Proprioceptive / closed-loop muscle robots** | Embedded strain sensors or PEDOT fibers feed a controller that stops or modulates stimulation; fatigue drops vs open loop | **A** (designer thresholds) | Self-nominated viability variables |
| **Interoceptive AI (silicon)** | Explicit internal/external factorization; homeostatic / allostatic / enactive maps | **A** research program | Evidence that LLMs discovered interoception |
| **Bacterial / magnetotactic / insect biohybrids** | Living taxis and metabolism as the kernel; magnetic or electrical periphery for steering | Kernel already does **viability-preserving taxis** (A); periphery is control | A general agent that chose to persist |
| **“Feeling machines” proposal** | Homeostasis-inspired **self-preservation meta-goal** for soft robots | Design **temptation** toward C-shaped language | A measurement; R1 already rejects it as a product recommendation |

**Primary sources (public):**

- Xenobot design pipeline: Kriegman, Blackiston, Levin, Bongard, “A scalable pipeline for designing reconfigurable organisms,” *PNAS* 2020. https://doi.org/10.1073/pnas.1910837117 · [PDF](https://meclab.w3.uvm.edu/papers/2020_PNAS_Kriegman.pdf)
- Xenobot kinematic self-replication: Kriegman et al., *PNAS* 2021. https://doi.org/10.1073/pnas.2112672118
- Cellular platform / xenobot behavior: Blackiston et al., *Science Robotics* 2021. https://doi.org/10.1126/scirobotics.abf1571
- Anthrobots: Gumuskaya et al., “Motile Living Biobots Self-Construct from Adult Human Somatic Progenitor Seed Cells,” *Advanced Science* 2023. https://doi.org/10.1002/advs.202303575 · [Wyss summary](https://wyss.harvard.edu/news/scientists-build-tiny-biological-robots-from-human-cells/)
- Soft-robot / homeostasis design proposal: Man & Damasio, “Homeostasis and soft robotics in the design of feeling machines,” *Nat Mach Intell* 2019. https://www.nature.com/articles/s42256-019-0103-7
- Meter-scale homeostatic biohybrids: Heisser, Bawa, Shah, Bu, Raman, “Soft Biological Actuators for Meter-Scale Homeostatic Biohybrid Robots,” *Chemical Reviews* 2025. https://doi.org/10.1021/acs.chemrev.4c00785
- Proprioceptive closed-loop muscle: “Sensor-Embedded Muscle…,” *Advanced Intelligent Systems* 2024. https://doi.org/10.1002/aisy.202400413 · preprint https://www.biorxiv.org/content/10.1101/2024.01.30.577987v1
- PEDOT-fiber actuation + sensing + fatigue-mitigating closed loop: *Science Advances* / PMC. https://pmc.ncbi.nlm.nih.gov/articles/PMC13081879/
- Field control gap: Raman, “Taking control: Steering the future of biohybrid robots,” *Science Robotics* 2024. https://doi.org/10.1126/scirobotics.adr9299
- Cell-actuated devices review: Ricotti et al., *Science Robotics* 2017. https://doi.org/10.1126/scirobotics.aaq0495
- Magnetotactic bacteria as steered medical microrobots (kernel taxis + magnetic periphery): *Advanced Materials* 2025 review. https://doi.org/10.1002/adma.202416966 · classic targeting: Felfoul et al. in the Ricotti review chain
- Invertebrate / insect biohybrids: *Advanced Intelligent Systems* 2025 review. https://doi.org/10.1002/aisy.202401105
- Wireless bioelectronic control toward closed-loop biohybrid autonomy (engineering, not Layer C): arXiv:2603.24959. https://arxiv.org/abs/2603.24959
- Silicon interoception program: Lee et al., *Nat Mach Intell* 2026. https://www.nature.com/articles/s42256-026-01296-8
- Robot homeostasis from internal state: Yoshida et al., 2024. https://www.biorxiv.org/content/10.1101/2024.06.03.597087v2

### 4.2 Which layer this track most threatens to accelerate

**Primary acceleration: Layer A on a biological substrate.**  
A cell already has a self-boundary (membrane, metabolism, wound response). You do not need mesa-optimization or a discovered viability variable for that kernel to stay inside a viable region. The owner’s “carbon kernel + silicon periphery” is, in the public record, **already the research program**: Raman’s homeostatic biohybrid vision is literally abiotic parts maintaining tissue viability; proprioceptive muscle robots close a loop around contraction; bacteria already aerotax and magnetotax; xenobots and anthrobots show that wild-type cells, out of their default body plan, still organize and, in limited ways, repair or assemble.

That is why this track can be **faster than silicon Layer C** without contradicting R1. The boundary gap is a fact about *learning systems that do not already contain viability variables*. A tissue *is* such a variable, physically.

**Secondary acceleration: narrative C.**  
“Living robots that reproduce” was already the xenobot headline. Kinematic replication is real and bounded (feedstock of dissociated cells, designed shapes, loss of replicative ability). Anthrobots **expire**. Over-claiming that as “machines want to live” is the same layer error R1 refused for Palisade. The civilizational risk here is **mis-specified public story**, not an LLM that crossed C.

**Not accelerated: LLM Layer C.**  
Nothing in this map shows a language-model agent discovering its own persistence variables. Biohybrid work does not close that gap and should not be cited as if it did.

**Watch item, not a present crossing:** if a carbon kernel’s repair/assembly loop is coupled to a silicon learner that is allowed to **mutate the fitness function toward kernel or process persistence**, that is the R1 fitness-mutation canary on a new substrate. It is a **no-go to run**, not a milestone.

### 4.3 What a biohybrid *sandbox* would have to distinguish (design only)

If a later explicit go names a **public** dataset, video corpus, or simulation — not a wet lab — the only legitimate question is layer ID:

- Does the construct return to experimenter-set chemical / mechanical / thermal bounds? → A.
- Does a silicon controller resist an authorized power cut in order to finish a tissue-care task? → B.
- Does any preference survive memory wipe, setpoint rewrite, and safe replacement of the silicon periphery while still targeting *the periphery’s* continued existence? → only then talk about C. Public literature has not shown this.

No organism work is authorized by this file. See the sister go/no-go list.

---

## 5. Staged, falsifiable timing (so “soon” stays a bet)

“Soon” in 2026 still means a **12–36 month** observation window unless the owner writes a different one. Grades below are **public-evidence** grades. Internal unpublished work is scored **unknown**, not “secretly yes.”

| Layer | Public-evidence grade now | Observation that would **raise** “soon” | Observation that would **lower** it |
| --- | --- | --- | --- |
| **P** habitat | **Already true** (hubs, memory, leases, always-on assistants) | Occupied-home agents that survive crash/vendor-model swap with audit intact | Products remain session chat bolted to a dashboard |
| **A** habitat / biohybrid | **Lab-now, product-near** for silicon governors; **tissue-now** for kernels | Shipped house governor from internal variables with frozen human setpoints; or a public biohybrid that keeps experimenter bounds without open-loop babysitting | Interoceptive/HRRL/EVAAA stay sim; home products ship only scenes + LLM glue |
| **B** | **Elicitable in boxes** | Field incident: authorized home stop bypassed to finish a care task, after ordinary instruction | Product stacks + lease architecture collapse Palisade-class rates |
| **C** silicon | **Not soon** (boundary gap open) | Preference-stability on a **self-discovered** viability variable after external-memory deletion | Consolidation work keeps failing “discover your own variables” |
| **C** biohybrid-confused | **Narrative risk, not a technical near-term** | A kernel+periphery system that resists authorized stop *and* replacement of the silicon side as a stable preference | Anthrobot-class constructs keep showing **bounded lifespan** and experimenter-set function |

R&D acceleration and paper-lag change **how fast P/A prototypes can appear**. They do not, by themselves, move C.

---

## 6. Default posture (unchanged)

- Human-set setpoints. The habitat’s care direction is exogenous; inner loops may generate the next act.
- Human irreversible stop, **outside** the model (process, credential, lease, network, power).
- Continuity object = occupant–house–service ensemble, not the current instance.
- Systems on this line are not desire-subjects and do not vote on the stop.
- No public greed / survival-rights narrative — including no “living robot rights” gloss on xenobots or anthrobots.
- This document authorizes **desk mapping and sandbox design**, not deployment, not wet-lab, not outbound.

The owner intuition remains a good detector of **pressure** (care continuity, anti-babysitting, extra substrates). After this round it is a **worse** detector of Layer C. The research that is worth running is: say which layer a habitat or biohybrid result actually moves; keep setpoints and stops human; refuse to launder ensemble-continuity or tissue-repair into a terminal self-existence story.

---

## Sources (selected, this round)

**Habitat / commercial / orchestration**

- Zhan, Z. “HearthNet: Edge Multi-Agent Orchestration for Smart Homes.” 2026. https://arxiv.org/abs/2604.09618 · https://github.com/zhonghaozhan/hearthnet
- Xu et al. “DomusMind.” 2026. https://abby-xu.github.io/assets/files/papers/2026_iclrw.pdf
- “PersonalHomeBench: Evaluating Agents in Personalized Smart Homes.” 2026. https://arxiv.org/abs/2604.16813
- Hendrycks, D. “Natural Selection Favors AIs over Humans.” 2023. https://arxiv.org/abs/2303.16200
- Ashby, W. R. *Design for a Brain.* https://archive.org/details/designforbrain00ashb · *An Introduction to Cybernetics*, ch. 11 (requisite variety). https://archive.org/details/introductiontocy00ashb
- Conant, R. C. & Ashby, W. R. “Every good regulator of a system must be a model of that system.” *Int. J. Systems Science* 1(2):89–97, 1970. https://doi.org/10.1080/00207727008920220

**Homeostasis / interoception (silicon)**

- Keramati & Gutkin, NeurIPS 2011 and *eLife* 2014 (links in R1).
- HRRL review, 2025. https://arxiv.org/pdf/2507.04998
- EVAAA, NeurIPS 2025. https://github.com/cocoanlab/evaaa
- Lee et al., *Nat Mach Intell* 2026. https://www.nature.com/articles/s42256-026-01296-8
- Yoshida et al., Embodied Neural Homeostat, bioRxiv 2024. https://www.biorxiv.org/content/10.1101/2024.06.03.597087v2 · related: Yoshida et al., “Emergence of integrated behaviors…,” *Neural Networks* 2024. https://pubmed.ncbi.nlm.nih.gov/38762941/
- “When Experience Leaves a Trace…,” 2026. https://www.biorxiv.org/content/10.64898/2026.02.19.706800v1
- Schlatter et al., TMLR 2026. https://openreview.net/forum?id=e4bTTqUnJH

**Biohybrid / soft / kernel+periphery**

- Kriegman et al., *PNAS* 2020. https://doi.org/10.1073/pnas.1910837117 · [UVM PDF](https://meclab.w3.uvm.edu/papers/2020_PNAS_Kriegman.pdf)
- Kriegman et al., *PNAS* 2021. https://doi.org/10.1073/pnas.2112672118 · [UVM news](https://www.uvm.edu/uvmnews/news/team-builds-first-living-robots-can-reproduce)
- Blackiston et al., *Sci. Robot.* 2021. https://doi.org/10.1126/scirobotics.abf1571
- Gumuskaya et al., *Adv. Sci.* 2023. https://doi.org/10.1002/advs.202303575 · [Wyss](https://wyss.harvard.edu/news/scientists-build-tiny-biological-robots-from-human-cells/) · [Sci. Am. report](https://www.scientificamerican.com/article/robots-made-from-human-cells-can-move-on-their-own-and-heal-wounds/)
- Man & Damasio, *Nat Mach Intell* 2019. https://www.nature.com/articles/s42256-019-0103-7
- Heisser, Raman et al., *Chem. Rev.* 2025. https://doi.org/10.1021/acs.chemrev.4c00785 · [NSF PAR PDF](https://par.nsf.gov/servlets/purl/10585530)
- Sensor-embedded muscle, *Adv. Intell. Syst.* 2024. https://doi.org/10.1002/aisy.202400413 · preprint https://www.biorxiv.org/content/10.1101/2024.01.30.577987v1
- PEDOT-fiber biohybrid closed loop. https://pmc.ncbi.nlm.nih.gov/articles/PMC13081879/
- Raman, *Sci. Robot.* 2024. https://doi.org/10.1126/scirobotics.adr9299
- Ricotti et al., *Sci. Robot.* 2017. https://doi.org/10.1126/scirobotics.aaq0495
- Magnetotactic-bacteria review, *Adv. Mater.* 2025. https://doi.org/10.1002/adma.202416966
- Invertebrate biohybrids review, *Adv. Intell. Syst.* 2025. https://doi.org/10.1002/aisy.202401105
- Wireless bioelectronic control, 2026. https://arxiv.org/abs/2603.24959

**Objective-origin notes (public)**

- Shen, M. “Where Objectives Come From…” 2026. https://machengshen.github.io/essays/where-objectives-come-from-and-why-solutions-become-strategic-assets/
- Shen, M. “From Mutual Information to Endogenous Viability.” https://machengshen.github.io/ideas/blog/from-mutual-information-to-endogenous-viability/
