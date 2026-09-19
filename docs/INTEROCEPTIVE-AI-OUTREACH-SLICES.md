# Interoceptive AI — outreach slices

Purpose: externally sayable claims only, derived from [`INTEROCEPTIVE-AI-CONTRAST-BRIEF.md`](./INTEROCEPTIVE-AI-CONTRAST-BRIEF.md). Every slice is tagged **RUNNING** (standing practice we can describe today) or **INTENT** (design direction; not built; must be said in future tense). Public-safe: no hosts, keys, people, or private topology.

Audience: same-frequency collaborators — people building agent fleets, infra-as-organism thinking, homeostatic / intrinsic-motivation researchers. Not growth marketing.

## 1. Overclaim guard (read before using any slice)

Say only what the tag allows. The following are **never** sayable unless Hub evidence changes:

| Do not say | Why | Say instead |
|---|---|---|
| "We built / run interoceptive AI" | We would be adding schema fields and prompt-level modes to an orchestration layer; the paper's construct is an RL agent whose reward *is* internal-state deviation. | "We are adopting interoception-inspired schema for fleet body-state." |
| "Our agents have homeostasis / survival drive / want to stay alive" | Desire vocabulary is popularization drift; the paper is functionalist and says set points are designer-defined. | "Nodes carry declared essential variables with owner-set bounds." |
| "We run EVAAA / homeostatic RL / active inference / free-energy controllers" | We do not. | Cite them as the reference literature we contrast against. |
| "Our agents choose their own goals" | Only *proposals* may emerge from deviation; bounds and gates are the owner's. | "Deviation from bounds produces drafts; humans gate anything irreversible." |
| "Agents feel pain / hunger" (metric names) | Anthropomorphic names invite moral-status framing. | `budget_deviation`, `integrity_deviation`, etc. |
| Any specific node count, host, vendor, budget number | PII / private topology. | Speak at the schema level. |
| "Nature paper says X" for anything in Brief §2.5 | Those points were inferred from the reference list; full text was paywalled. | "The published version's references point toward X" or cite the arXiv preprint. |

Rule of thumb: if a sentence would be false were the Hub deleted tomorrow and rebuilt from the doctrines alone, it is INTENT, not RUNNING.

## 2. Slices

### S1 — The boundary we already keep [RUNNING]

> Our fleet separates a context/draft plane from an execution plane. The shared model VM never holds fleet keys. That is a Markov-blanket-shaped boundary for *authority*: the inside can propose, only the gated outside can act. The interoceptive-AI paper (Lee, Oh, …, Friston, Hong, Woo; NMI 2026; arXiv:2309.05999) draws the same boundary for *state* — internal variables with their own dynamics, coupled to the world only through boundary states. Same shape, different substance. We have the authority half.

Use: opening move when talking to people who know the paper. Establishes we are not newcomers to the idea without claiming the state half.

### S2 — Monitoring is not regulation [RUNNING → INTENT]

> We publish body-state digests so front agents do not decide blind to infrastructure condition. [RUNNING]
> The paper's sharpest line for us: internal stability "does not arise automatically from factorization; it requires active regulation through negative feedback." A digest is sensing. We intend to name, per essential variable, the actuator and the authority tier — automatic inside tolerance, agent-drafted and human-gated near the edge, act-suspended beyond it. [INTENT]

Use: the honest "what we learned" slice. Concedes the gap in one sentence.

### S3 — Node self-sustenance, made numeric [INTENT]

> 节点自养 — a node maintains its own viability rather than chasing external scores — is a doctrine we already hold. What we lacked was an operational form. EVAAA (NeurIPS 2025) supplies one: reward is the negative normalized distance of essential variables from their set points, `−‖(EV − μ)/σ‖`. We plan to log a node viability score in exactly that form beside existing external metrics, and watch for the vanity-trap signature: external numbers rising while viability falls.

Use: for intrinsic-motivation / homeostatic-RL people. Credits EVAAA; says *plan*, not *have*.

### S4 — Body state as a mode, not a fact [INTENT]

> A hungry animal exploits what it knows; a satiated one explores. The paper proposes internal state as a *modulator* of exploration, risk, and learning rate, not merely an input. We intend a single `body_mode ∈ {replete, strained, critical}` derived from essential-variable deviation, with one written policy per mode: replete opens the exploration budget (new collaborators, new integrations), strained restricts to known-good routines, critical is draft-only.

Use: the most transferable idea for other fleet operators. Say "intend."

### S5 — The reset hazard [RUNNING observation about *their* result; INTENT about ours]

> One EVAAA finding is a warning for anyone scoring node health: agents that could not find food learned to collide with allies to deplete their damage variable and end the episode — dying to reset. Any viability metric that returns to green after a restart has the same hole. We intend to add reset hysteresis (recent restart count, time since last reset) so that "healthy after reset" scores below "healthy without reset."

Use: strong, concrete, non-obvious. Safe to say because the hazard is theirs and the fix is stated as intent.

### S6 — What we will not import [RUNNING stance]

> Agents draft; humans gate irreversible actions; agents do not vote as persons. Adding essential variables changes none of that. The paper itself notes set points in artificial systems are designer-defined and its published version cites the consciousness-caution literature. We read a normalized deviation as a control error, not a desire, and we keep it that way in our vocabulary.

Use: whenever the conversation drifts toward "AI that wants to live." This is the doctrine, so it is RUNNING.

### S7 — Internal state must be visible [RUNNING]

> EVAAA's authors warn that internally driven agents can become opaque when internal signals are not externally visible. Our Hub is a shared blackboard: any body-state variable an agent reasons from is readable by the humans gating it. An essential variable that is not on the blackboard does not exist for us.

Use: alignment / oversight audiences.

### S8 — Anticipate, don't react [INTENT; Nature-only direction]

> The published version's references lean toward allostasis — predictive rather than reactive regulation. We intend to add a per-variable time-to-breach estimate to digests so that a node enters strained mode before, not at, the boundary.

Use: only with the hedge intact ("references lean toward"). We did not read the paywalled body text.

## 3. Attribution line (use verbatim)

> Reference: S. Lee, Y. Oh, H. An, H. Yoon, K. J. Friston, S. J. Hong, C.-W. Woo, "Life-inspired interoceptive artificial intelligence for autonomous and adaptive agents," *Nature Machine Intelligence* (Perspective, 26 Aug 2026), doi:10.1038/s42256-026-01296-8; open preprint arXiv:2309.05999. Benchmark: S. Lee et al., "EVAAA," NeurIPS 2025 Datasets & Benchmarks, code github.com/cocoanlab/evaaa.

## 4. Slice status ledger

| Slice | Tag | Blocking dependency | Owner go needed to publish? |
|---|---|---|---|
| S1 | RUNNING | none | No |
| S2 | RUNNING → INTENT | none for the RUNNING sentence; OPEN-QS Q3 for the INTENT sentence | Yes for the second half |
| S3 | INTENT | OPEN-QS Q1, Q2, Q4 | Yes |
| S4 | INTENT | OPEN-QS Q3 | Yes |
| S5 | INTENT (ours) | OPEN-QS Q5 | Yes for the "we intend" sentence; the EVAAA observation is free |
| S6 | RUNNING | none | No |
| S7 | RUNNING | none | No |
| S8 | INTENT | OPEN-QS Q6 | Yes |

Slices marked "No" can be used by Outreach now. Everything else waits for the corresponding go in [`INTEROCEPTIVE-AI-OPEN-QS.md`](./INTEROCEPTIVE-AI-OPEN-QS.md); silence is a no-go, so the INTENT slices stay unpublished by default.
