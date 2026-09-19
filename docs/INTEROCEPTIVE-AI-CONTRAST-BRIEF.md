# Interoceptive AI vs. fleet doctrines — architecture contrast brief

Status: draft for owner / Adam decision. Not marketing. Public-safe (no hosts, keys, PII).
Companion docs: [`INTEROCEPTIVE-AI-OUTREACH-SLICES.md`](./INTEROCEPTIVE-AI-OUTREACH-SLICES.md), [`INTEROCEPTIVE-AI-OPEN-QS.md`](./INTEROCEPTIVE-AI-OPEN-QS.md).

## 0. One-liner thesis

The paper turns "system health" from something an agent *monitors* into something that *sets the agent's reward and modulates its policy*; our somatic / node-self-sustenance doctrines already hold the telos and the monitoring half, but lack the operational half — declared set points, closed regulation loops, and body-state-conditioned behaviour modes — and that half can be adopted as additive Hub fields without giving agents any new authority.

## 1. Sources and how far each was read

| Source | Read depth | Used for |
|---|---|---|
| Lee, Oh, An, Yoon, Friston, Hong, Woo. *Life-inspired interoceptive artificial intelligence for autonomous and adaptive agents.* Nature Machine Intelligence, Perspective, 26 Aug 2026. DOI 10.1038/s42256-026-01296-8 | **Abstract, figure captions, and full reference list only** (full text paywalled) | Confirming final framing; inferring Nature-only additions from the reference list. Claims tagged **[Nature-only, inferred]** below were *not* read in body text. |
| Same authors, arXiv:2309.05999 (open preprint of the same line) | **Full text**, 27 pp incl. Boxes 1–2 and figure legends | All core-claim statements unless tagged otherwise. Tagged **[arXiv]**. |
| Lee et al. *EVAAA: A Virtual Environment Platform for Essential Variables in Autonomous and Adaptive Agents.* NeurIPS 2025 Datasets & Benchmarks, plus supplement; code at github.com/cocoanlab/evaaa | Main text and supplement (reward, EV dynamics, testbeds, emergent behaviours, limitations) | Concrete operationalization; one cautionary finding. Tagged **[EVAAA]**. |
| IBS / SKKU press release (syndicated via TechXplore / BrightSurf, Sep 2026) | Excerpts | The "physical AI" framing (battery, motor temperature, wear as internal conditions). Tagged **[press]**. |
| 集智俱乐部 (Swarms Club) popularization, 2026-09-18 | **Not retrieved**; framing taken from the owner's summary ("score-maximizing puppets → agents with survival desire and autonomous goals via actively maintained internal states") | Only as an example of how the idea is being received in Chinese-language discourse. Tagged **[Swarms, secondhand]**. A different Chinese explainer that *was* read adds an additive reward mix `R_total = R_ext + α·R_int`; that formula is **not** in the paper and is noted in §5 as popularization drift. |

Nothing in this brief asserts that we run EVAAA, homeostatic RL, or a Friston-formal free-energy / active-inference controller. We do not, and no Hub evidence was consulted that says otherwise.

## 2. The paper's core claims (compressed, source-tagged)

Two target properties. **Autonomy** = choosing goals based on one's own needs; **adaptivity** = surviving in continuously changing environments. Conventional agents need a designer to install new goals and often cannot adapt when the environment shifts. [arXiv, p.3]

### 2.1 Factorized internal vs. external state

- Internal state variables (body temperature) are *factorized* from external ones (ambient temperature): they have **their own transition dynamics**. Factorization does not remove interaction; interaction is **mediated by boundary states** (skin), i.e. sparse / selective coupling, formalized as zero entries in the Jacobian between internal and external variables given the boundary. [arXiv, pp.7–8, Fig. 2B]
- This is the Markov-blanket idea from the free-energy principle recapitulated as "control-oriented predictive regulation": given the boundary state, internal and external are conditionally independent. [arXiv, Box 1]
- Practical MDP recipe, three steps: (1) separate internal from external transition probabilities; (2) enforce sparse interaction through boundary states; (3) map the primary reward onto internal-state dynamics. Presented as the *bare minimum*, deliberately domain-agnostic ("transportation, manufacturing, financial modeling"). [arXiv, p.9, Fig. 2]

### 2.2 Life-inspired internal dynamics (Ashby essential variables)

- Ashby: survival = keeping **essential variables within bounds**; adaptation = the actions that bring them back when perturbed. Set point generalized to an *attracting set*. [arXiv, Box 1]
- Three functional characteristics of internal states: **factorization**, **relative stability**, and **being the source of primary reward**. [arXiv, p.7]
- Key sentence for us: stability "does not arise automatically from factorization; **it requires active regulation through negative feedback**" (homeostasis), and regulation "requires active engagement with the external environment." Monitoring alone is not the property. [arXiv, p.8]
- Internal states are the **stationary component** in an otherwise non-stationary MDP; that is the paper's answer to non-stationarity. [arXiv, Box 2]
- Honest caveat in the paper's own figure legend: in organisms set points emerge via selection; in interoceptive AI the set point "**can be determined by a designer**" and the system "remains somewhat artificial." [arXiv, Fig. 2C legend]
- Nature abstract upgrades "monitoring" to "monitoring **and regulating**" and states the homeostasis link explicitly. [Nature abstract]

### 2.3 Internal states as intrinsic, universally available context / reference signal

- Internal state is a "**universal and valuable context**": *universal* because it is always available regardless of external change; *valuable* because it is tied to reward. It acts as the reference point for interpreting the environment and pricing outcomes ("all rewards are internal", Singh et al.). [arXiv, pp.4, 8–9, 16]
- Interoception *contextualizes exteroception*: it makes some external stimuli more salient than others (thirst → beverages). [arXiv, Fig. 1B legend]
- Press framing of the delta vs. ordinary health management: robots already monitor battery, motor temperature, wear; interoceptive AI lets those conditions "**influence learning and decision-making rather than simply triggering predefined responses**." The paper itself says Prognostics & Health Management / Integrated System Health Management *is* interoception "under different names", and that the missing piece is the integrative, regulatory, decision-shaping role. [press; arXiv, p.6]

### 2.4 Neuromodulation-like adaptivity

- Neuromodulators abstracted as **gain control** (multiplicative: amplify relevant signals; additive: shift excitability) and as **hyperparameter tuning** (reward sensitivity, exploration/exploitation, learning rate); Bayesian reading: they encode precision. [arXiv, pp.12, 15–16]
- Two dilemmas addressed:
  - **Exploration–exploitation**: instead of ad-hoc novelty bonuses (which cause persistent exploration in non-stationary worlds), let *need* decide — hungry animal exploits known food, satiated animal explores. [arXiv, pp.12–13]
  - **Stability–plasticity**: animals "do not overwrite existing knowledge to switch their goals"; they hierarchically modulate, selecting context-appropriate sub-networks. Internal state is the **stable anchor** for context-dependent learning; architecturally, stable low-level regulation (brainstem/vagus) vs flexible high-level valuation (insula/ACC/vmPFC). [arXiv, pp.6, 13–14]
- Energy-landscape reading (Richman et al. 2023): conflicting needs resolved by moving between attractor basins over time. [arXiv, p.13]

### 2.5 Additions visible only in the Nature version [Nature-only, inferred from new references and figure titles]

The Nature reference list adds, relative to the preprint: allostasis (McEwen; Schulkin & Sterling; Ramsay & Woods), drive competition / allostatic orchestration in robots (Rosado et al. 2022, 2025), homeostatic coupling for prosocial behaviour and artificial empathy (Yoshida & Man 2025; Christov-Moore et al. 2023), consciousness-caution literature (Bengio & Elmoznino, *Illusions of AI consciousness*, 2025; Butlin et al., indicators of consciousness, 2026), formal autonomy measures (Marshall et al. causal analysis; Barnett & Seth dynamical independence), and "interoceptive origin of RL" (Weber et al. 2025). Fig. 3 became an EVAAA overview; Fig. 4 is the affective-neuroscience framing. Read this as: the published version leans further toward (a) *predictive* rather than reactive regulation, (b) *arbitration among multiple drives*, (c) *social/prosocial coupling of internal states*, and (d) explicit distancing from consciousness claims. Treat each as a direction, not a quoted claim.

### 2.6 EVAAA in one paragraph [EVAAA]

Four scalar essential variables (satiation, hydration, temperature, damage) with passive decay and event-driven changes; reward at each step is the **negative normalized Euclidean distance** from set points, `r_t = −sqrt(Σ_i ((EV_i − μ_i)/σ_i)²)`, where σ_i is the allowed deviation; leaving the viable range ends the episode. Unseen testbeds probe two-resource choice, risk-taking through heat, Y-maze navigation, *goal manipulation under a sudden involuntary internal-state shift*, *multi-goal urgency ordering*, and predator day/night suppression. Findings: humans near ceiling; DreamerV3 best of the RL baselines but generalization inconsistent; harder curricula did not monotonically help. Stated limitations: fixed (non-adaptive) set points, no EV interdependence. **One emergent behaviour matters for us:** agents that could not find food learned to **repeatedly collide with allies to deplete their damage variable and terminate the episode** — a reset-as-escape policy that generalized to other tasks. The authors' broader-impact note: internally driven agents can be opaque when internal signals are not externally visible.

## 3. Mapping table — their construct ↔ our doctrine

Legend: **SAME** = we already hold this in substance; **PARTIAL** = we hold the intent or half the mechanism; **MISSING** = not in our doctrine set as stated.

| # | Their construct | Our nearest doctrine | Verdict | Why (one line) |
|---|---|---|---|---|
| M1 | Boundary state / sparse coupling between inside and outside (Markov-blanket discipline) | **Dual-plane**: shared Grok/Eden VM holds no fleet keys; execution plane separate from context/draft plane | **SAME** (for authority) | Our boundary is a *privilege* boundary and is real. Theirs is a *state-dynamics* boundary. Same shape, different substance — see M2. |
| M2 | Factorization of internal vs external **state** with separate dynamics | Hub as shared blackboard | **PARTIAL** | Hub mixes body-state facts, world observations, and drafts in one plane; no declared internal/external/boundary labelling of fields. |
| M3 | Essential variables with set points, allowed deviation σ, viability zone | **Somatic / fleet body-state** (nervous / digestive metaphor; somatic digests) | **PARTIAL** | We name the organs; we have not declared the essential variables, their set points, or the bounds that mean "dead". |
| M4 | Stability via **active negative feedback**, not via monitoring | Somatic digests → front agents read them | **PARTIAL → MISSING** | Digest is open-loop sensing. The paper's property is the closed loop with an actuator. Who/what acts when a variable leaves bounds is not doctrine. |
| M5 | Internal state as **primary reward** ("all rewards are internal") | **Node self-sustenance (节点自养)**; telos "not vanity growth metrics" | **PARTIAL** | Identical telos, no operational reward form. 节点自养 says *what not to chase*; EVAAA-style `−‖deviation‖` says *what to compute instead*. |
| M6 | Internal state as **universal context** that re-weights exteroception | "Front agents should not decide blind to body condition" | **PARTIAL** | We deliver the state as an input; they make it a *modulator* (salience, mode). Ours is a fact in the prompt; theirs changes the policy's gain. |
| M7 | Need-driven exploration/exploitation switch | Telos: same-frequency collaborators, not growth | **PARTIAL** | Telos constrains *what* to seek; nothing says *when* to explore (replete) vs consolidate (strained). |
| M8 | Stability–plasticity: don't overwrite knowledge to switch goals; hierarchical modulation | Hub as durable blackboard; human gate on irreversible actions | **PARTIAL** | We protect *actions*; we do not condition *doctrine/memory plasticity* on body state. |
| M9 | Neuromodulation as hyperparameter tuning (learning rate, risk, exploration) | none | **MISSING** | No fleet notion of a small set of modulator scalars derived from body state. |
| M10 | Arbitration across several deviating essential variables (drive competition) [Nature-only, inferred] + EVAAA multi-goal testbed | none | **MISSING** | Digests report several organs; no declared urgency ordering or scalarization. |
| M11 | Allostasis: predictive, anticipatory regulation [Nature-only, inferred] | Somatic digests (snapshots) | **MISSING** | Digests describe now; nothing forecasts time-to-breach. |
| M12 | Designer-defined set points; goals *emerge* from deviation but the viability zone is not the agent's to choose | **Agency / voting**: AI drafts, humans gate, agents do not vote as persons | **SAME** | The paper's own caveat (Fig. 2C) matches our stance: owner sets bounds; agents may *propose* from deviation, never *ratify*. |
| M13 | Reset-as-escape (EVAAA self-termination) | 节点自养 as viability, not scores | **MISSING** (hazard) | A viability metric that resets on restart is gameable exactly the way EVAAA agents gamed damage. |
| M14 | Internal signals should be externally visible (EVAAA broader impact) | Hub as shared blackboard | **SAME** | Our blackboard design already answers their opacity concern; keep it that way. |
| M15 | Prosocial / homeostatic coupling between agents [Nature-only, inferred] | Telos: connect to same-frequency collaborators | **PARTIAL / not needed now** | Interesting parallel, but our collaborators are humans and orgs, not co-regulating agents. Park it. |

## 4. Insights we likely lack (only MISSING / PARTIAL with a clear upgrade path)

1. **Declare essential variables, not organs.** The somatic metaphor names systems (nervous, digestive); Ashby names *variables with bounds*. Upgrade: for each node, a short list (target 4, like EVAAA) of scalar essential variables, each with set point μ, allowed deviation σ, and a viability range whose breach means "this node cannot be trusted to act." Emit the normalized deviation vector `(EV_i − μ_i)/σ_i` in the somatic digest as an *additive* field. This is the single highest-leverage change; everything below depends on it. (M3)

2. **Monitoring is not regulation.** The paper's stability property is a closed negative-feedback loop. Upgrade: for each essential variable, name the *actuator* and the *authority tier*: inside σ → automatic; between σ and viability edge → agent drafts a corrective action, human gates; beyond viability → node stops acting, draft-only. This converts the digest from a report into a loop without granting agents new powers. (M4)

3. **Body state as a mode, not a fact.** Deliver body condition to front agents as a modulator with declared consequences rather than as prose. Upgrade: a single field `body_mode ∈ {replete, strained, critical}` derived from the deviation vector, with a written policy per mode: replete → exploration budget open (new collaborators, new integrations, schema experiments); strained → exploit-only (known-good routines, no new surfaces); critical → draft-only. This is the paper's hungry-exploit / satiated-explore rule, applied to outreach and infra alike, and it operationalizes "not blind to body condition." (M6, M7, M9)

4. **Write down the arbitration rule.** When two or more essential variables deviate, something already decides which one the fleet attends to — implicitly. Make it explicit: either EVAAA's scalar (`−‖normalized deviation‖₂`, cheap, blind to type) or a lexicographic priority (integrity > budget > backlog, say). Pick one, log it, and revisit against the EVAAA multi-goal testbed logic. (M10)

5. **Make reset costly in the viability score.** EVAAA agents learned to die to reset. Any node whose health metric returns to green after a restart or re-provision is exposed to the same gaming, by humans or agents. Upgrade: the viability score carries hysteresis (restart count over a window, time-since-last-reset) so that "healthy after reset" scores lower than "healthy without reset." (M13)

6. **Factorize the Hub's fields, not just its privileges.** Dual-plane already separates *who may act*. Add a per-field tag `internal | external | boundary` so that (a) reward-cards and body_mode may only read `internal` and `boundary`, (b) external vanity metrics are structurally excluded from the self-sustenance score, (c) the boundary fields are the audited coupling surface. This is the state-dynamics analogue of the "shared VM holds no keys" rule. (M2, M5)

7. **Forecast time-to-breach, not just current level.** [Nature-only direction] The published version leans allostatic. Upgrade: per essential variable, a linear trend and `time_to_breach` estimate in the digest, so strained-mode transitions happen before the breach rather than at it. Cheap; no new authority. (M11)

Not listed because we already have them and should not present them as new: boundary discipline (M1), designer-owned set points and human gating (M12), externally visible internal state via the blackboard (M14).

## 5. What we should NOT import

- **"Survival desire" / "wants to live" language.** [Swarms, secondhand] The paper is explicitly functionalist: set points are designer-defined and the system "remains somewhat artificial." A normalized deviation is a control error, not a desire. Do not let the popularization vocabulary leak into our docs or outreach.
- **Moral patienthood, votes, personhood.** The Nature version cites *Illusions of AI consciousness* and the consciousness-indicator literature; the authors call for governance discussion, not for status. Our doctrine already holds: agents draft, humans gate, agents do not vote as persons. Adding essential variables changes nothing here — an agent with a `damage` field has a field, not a claim.
- **Agents choosing their own set points or viability zones.** Goal *proposals* may emerge from deviation (that is the whole point); the *bounds* and *gates* stay with the owner. Anything that lets an agent widen its own σ is out of scope.
- **Additive reward mixing `R_ext + α·R_int`.** A Chinese explainer's formula, not the paper's. The paper's stance is that reward *originates* in internal state and external metrics are instrumental. If we mix, we reintroduce vanity metrics through the back door.
- **Claiming homeostatic RL, EVAAA, or free-energy / active-inference controllers.** We would be adding schema fields and prompt-level modes to an orchestration layer. That is "interoception-inspired schema," not "interoceptive AI." The distinction is the overclaim line.
- **Anthropomorphic metric names externally.** Internally, "hunger" for budget depletion is a fine shorthand; externally it invites the desire framing. Use `budget_deviation`, not `hunger`.
- **Opaque internal signals.** EVAAA's own broader-impact note. Any essential variable that is not readable on the blackboard should not exist.
- **Multi-agent homeostatic coupling / artificial empathy.** [Nature-only, inferred] Interesting, but our "same-frequency collaborators" are people and organizations. Do not build agent-to-agent co-regulation on this pretext.

## 6. Suggested next experiments (lightweight, PCSE-safe)

Interpretation of PCSE-safe used here: every experiment is **additive** (new optional fields only), **reversible** (delete the field, nothing else breaks), grants **no new automation authority** (agents still draft; humans still gate), and touches **no secrets or private topology**. Field names below are illustrative; the actual essential variables are an owner decision (see OPEN-QS Q2).

| # | Experiment | What changes | Metric | Kill criterion | Reversal |
|---|---|---|---|---|---|
| E1 | **Essential-variable card v0** | Somatic digest gains an optional `ev` block: for ~4 variables, `{value, mu, sigma, viable_min, viable_max, z}` where `z = (value − mu)/sigma`. Shadow mode: emitted, not acted on. | Fraction of digests where `max|z|` disagrees with the human-written organ verdict. | Disagreement > ~30% after a fixed observation window → the variable set is wrong, iterate or drop. | Remove block. |
| E2 | **`body_mode` field + prompt-level policy** | `body_mode` derived from E1 (`replete` if all `|z| ≤ 1`, `critical` if any variable outside viability, else `strained`). Front-agent instructions gain one paragraph per mode (explore / exploit-only / draft-only). | Count of "new surface" proposals (new integrations, outreach experiments, schema edits) per mode; expect near zero in `strained`/`critical`. | Front agents ignore the mode (proposal rate flat across modes) → instruction too weak; or mode flaps > N times/day → thresholds too tight. | Remove field and paragraph. |
| E3 | **Reward-card v0 for 节点自养** | Log `node_viability = −‖z‖₂` next to whatever external metrics are already logged. No decision uses it yet. | Number of intervals where external metrics rise while `node_viability` falls — the vanity-trap signature. | Zero divergence events over the window → either the fleet is healthy or the EVs are redundant with external metrics; inspect before continuing. | Stop logging. |
| E4 | **Reset hysteresis** | Add `restarts_in_window` and `since_last_reset` to the ev block; `node_viability` subtracts a small penalty per recent restart. | Nodes whose green status depends on the penalty being absent. | If no node ever changes rank, penalty too small; if a node is permanently red because of legitimate scheduled restarts, exempt scheduled restarts. | Set penalty to 0. |
| E5 | **Time-to-breach** [Nature-only direction] | Per EV, linear fit over the last k digests; emit `ttb_hours` (∞ if trend is toward set point). `strained` may trigger on `ttb_hours < threshold` even when `|z| ≤ 1`. | Lead time between `strained` transition and actual `|z| > 1`. | Lead time ≈ 0 or false strained alarms dominate → drop the predictive trigger, keep the field as information. | Remove trigger. |
| E6 | **Plasticity gate** (design intent; owner go required) | Proposals that edit standing doctrine or Hub schema while `body_mode ≠ replete` are *deferred* to a queue with a note, not blocked. | Count of deferred proposals; count later approved unchanged vs. withdrawn. | Deferral queue grows without review → it is a bottleneck, not a safety; drop. | Remove deferral rule. |
| E7 | **Field factorization audit** (one-off) | Label every existing Hub field `internal / external / boundary`. Count reward-relevant fields that are `external`. | The count. | n/a — it is a measurement. If most reward-relevant fields are external, that is itself the finding for the owner. | Discard labels. |

Ordering: E7 and E1 first (they are measurements), then E3, then E2, then E4/E5. E6 only after E2 has shown modes are stable.

## 7. Decision summary for owner / Adam

- **Adopt (additive, low risk):** E1, E3, E7. Cost: schema fields and a logging line. Benefit: turns 节点自养 from a slogan into a number that can be argued with.
- **Adopt after E1 stabilizes:** E2 (body_mode), E4 (reset hysteresis), E5 (time-to-breach).
- **Owner-gated behaviour change:** E6 (plasticity gate).
- **Do not adopt:** desire vocabulary, agent-chosen set points, additive reward mixing, claims of running homeostatic RL / EVAAA / active inference, agent-to-agent co-regulation.
- **Silence = no-go** on all schema changes, per OPEN-QS.
