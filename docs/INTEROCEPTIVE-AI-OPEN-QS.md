# Interoceptive AI — open questions for owner go / no-go

Scope: every question below concerns a **Hub schema change, a front-agent instruction change, or an external publication** proposed in [`INTEROCEPTIVE-AI-CONTRAST-BRIEF.md`](./INTEROCEPTIVE-AI-CONTRAST-BRIEF.md) §6 and gated in [`INTEROCEPTIVE-AI-OUTREACH-SLICES.md`](./INTEROCEPTIVE-AI-OUTREACH-SLICES.md) §4.

**Default rule: silence = no-go.** Nothing here proceeds without an explicit owner "go" recorded against the question ID. Agents may draft the change; they may not enact it. No question below grants any agent new authority to act — every proposal is additive, reversible, and read-only for decision-making until separately approved.

Decision record format (append under each question):

```
GO | NO-GO | DEFER — <date> — <owner> — <one-line reason / constraint>
```

---

## Q1 — Adopt an essential-variable (`ev`) block in somatic digests? (Brief E1)

- **Change:** optional `ev[]` block per node in the somatic digest: `{name, value, mu, sigma, viable_min, viable_max, z}`. Shadow mode only: emitted, never acted on.
- **Why:** converts organ metaphor into Ashby essential variables; prerequisite for every other item.
- **Risk if GO:** near zero — additive field, no reader is required to consume it.
- **Risk if NO-GO:** the rest of the brief stays theoretical; 节点自养 remains a slogan.
- **Reversal:** delete the block.
- **Depends on:** Q2 (which variables).
- **Decision:** _pending_

## Q2 — Which ~4 essential variables, and who owns their set points?

- **Change:** owner names the variable set and, per variable, μ (set point), σ (allowed deviation), and viability range. Illustrative candidates only — not a recommendation of specific infra: compute/quota budget headroom, storage headroom, backlog age, error or integrity rate.
- **Why:** the paper's own caveat is that AI set points are designer-defined. This makes the designer explicit. Agents must never widen their own σ.
- **Risk if GO:** wrong variables produce a confident but useless deviation vector; E1's kill criterion catches that.
- **Risk if NO-GO:** Q1 cannot proceed.
- **Reversal:** redefine; historical digests keep old values with a version tag.
- **Sub-question:** fixed set points (EVAAA-style) or owner-adjustable over time (allostatic)? Recommend fixed for v0.
- **Decision:** _pending_

## Q3 — Add `body_mode` and one instruction paragraph per mode to front agents? (Brief E2)

- **Change:** `body_mode ∈ {replete, strained, critical}` derived from `max|z|` and viability breaches; front-agent instructions gain a mode-conditioned paragraph (replete: exploration budget open; strained: exploit-only, no new surfaces; critical: draft-only). Alongside it, per essential variable, the owner names the **actuator and authority tier** (Brief insight 2): inside σ → automatic; between σ and the viability edge → agent drafts, human gates; beyond → node suspended to draft-only. Naming the actuator is documentation, not automation.
- **Why:** the paper's core delta over ordinary health management — internal state as a *modulator*, not an input — and its insistence that stability comes from a closed feedback loop, not from monitoring.
- **Risk if GO:** this is the first item that changes agent *behaviour*. It only ever *restricts* (strained/critical remove options; replete restores the status quo), so it cannot expand authority. Mode flapping is the practical risk; thresholds are tunable.
- **Risk if NO-GO:** digests remain prose that agents may ignore; "not blind to body condition" stays unenforced.
- **Reversal:** remove field and paragraph.
- **Depends on:** Q1 stable for an observation window.
- **Decision:** _pending_

## Q4 — Log a `node_viability = −‖z‖₂` reward-card beside external metrics? (Brief E3)

- **Change:** one logged scalar per node per digest. No decision consumes it.
- **Why:** gives 节点自养 an operational form and exposes the vanity-trap signature (external up, viability down).
- **Risk if GO:** none beyond log volume. Naming risk: keep it `node_viability`, never "wellbeing" or similar.
- **Risk if NO-GO:** no numeric contrast between internal and external scores.
- **Reversal:** stop logging.
- **Sub-question:** scalar L2 (EVAAA) vs lexicographic priority across variables (Brief insight 4). Recommend L2 for v0, revisit after Q1 data.
- **Decision:** _pending_

## Q5 — Add reset hysteresis (`restarts_in_window`, `since_last_reset`) with a viability penalty? (Brief E4)

- **Change:** two fields in the `ev` block plus a small subtraction in `node_viability` per recent unscheduled restart.
- **Why:** EVAAA agents learned to self-terminate to reset a damage variable; a health metric that resets on restart is gameable the same way.
- **Risk if GO:** legitimate scheduled restarts get penalized unless exempted; define "scheduled."
- **Risk if NO-GO:** viability score can be gamed by restart.
- **Reversal:** set penalty to 0.
- **Depends on:** Q4.
- **Decision:** _pending_

## Q6 — Add per-variable `time_to_breach` and let it trigger `strained` early? (Brief E5; Nature-only direction)

- **Change:** linear trend per EV over recent digests; `ttb_hours` field; optional early `strained` trigger when `ttb_hours` falls under a threshold.
- **Why:** anticipatory (allostatic) rather than reactive regulation. Note the source basis is the published version's reference list, not read body text.
- **Risk if GO:** false strained alarms if trends are noisy; the trigger half can be disabled while keeping the field.
- **Risk if NO-GO:** modes switch only after a breach.
- **Reversal:** remove trigger, then field.
- **Depends on:** Q1, Q3.
- **Decision:** _pending_

## Q7 — Plasticity gate: defer doctrine/schema edits while `body_mode ≠ replete`? (Brief E6)

- **Change:** proposals that modify standing doctrine or Hub schema during strained/critical mode are queued with a note, not blocked, and surface for human review when replete or on explicit human pull.
- **Why:** stability–plasticity — do not rewrite knowledge while under duress. Mirrors "humans gate irreversible action" for the memory layer.
- **Risk if GO:** this is a genuine process change and can become a bottleneck; kill criterion is an unreviewed queue.
- **Risk if NO-GO:** none immediate; this is the most speculative item.
- **Reversal:** remove the deferral rule; queued items are released unchanged.
- **Depends on:** Q3 proven stable.
- **Recommendation:** DEFER until Q3 has data.
- **Decision:** _pending_

## Q8 — Run the one-off Hub field factorization audit (`internal | external | boundary`)? (Brief E7)

- **Change:** a labelling pass over existing Hub fields; produces one count (reward-relevant fields that are `external`). No schema change unless Q9 follows.
- **Why:** the paper's factorization applied to state, not just authority. The count itself is the deliverable.
- **Risk if GO:** analyst time only.
- **Risk if NO-GO:** we do not know how much of what we score is external.
- **Reversal:** discard labels.
- **Decision:** _pending_

## Q9 — Persist the factorization tag as a schema field and restrict reward-cards to `internal | boundary`?

- **Change:** make Q8's labels a first-class field; `node_viability` and `body_mode` may read only `internal` and `boundary` fields.
- **Why:** structurally excludes vanity metrics from self-sustenance scoring.
- **Risk if GO:** mis-tagged fields silently drop out of the score; requires Q8 to be reviewed by a human first.
- **Risk if NO-GO:** exclusion stays a convention rather than a constraint.
- **Depends on:** Q8 complete and reviewed.
- **Decision:** _pending_

## Q10 — Vocabulary: adopt "interoceptive" externally, or keep "somatic"?

- **Change:** naming only. Options: (a) keep "somatic / body-state" and cite interoception as the literature; (b) rename the digest line "interoceptive digest."
- **Why:** (a) avoids the overclaim line entirely; (b) is more discoverable to the research community but invites "you built interoceptive AI?"
- **Recommendation:** (a). Use "interoception-inspired" as an adjective only.
- **Risk either way:** low; this is about the overclaim guard.
- **Decision:** _pending_

## Q11 — Publish the INTENT slices (S2 second half, S3, S4, S5-intent, S8)?

- **Change:** Outreach may use future-tense slices from the slices doc.
- **Why:** they are the interesting ones; but each says "we intend," which becomes false if the corresponding Q is a NO-GO.
- **Constraint:** each INTENT slice may be published only after its dependency Q is GO (mapping in slices §4). RUNNING slices S1, S6, S7 need no go.
- **Decision:** _pending_ (per-slice)

## Q12 — Fetch and read the paywalled Nature full text?

- **Change:** someone with institutional access reads the published body text and confirms or strikes every **[Nature-only, inferred]** tag in the brief (§2.5, M10, M11, M15, insight 7, S8).
- **Why:** the brief is arXiv-grounded by design; the inferred items are directions, not quotes.
- **Risk if NO-GO:** the inferred items stay hedged; that is acceptable.
- **Decision:** _pending_

---

## Recommended decision order

1. Q8 (audit; pure measurement) and Q2 → Q1 (variables, then the block).
2. Q4 (reward-card logging) once Q1 emits data.
3. Q3 (`body_mode`) after an observation window on Q1.
4. Q5, Q6 after Q3.
5. Q9 after Q8 is reviewed.
6. Q7 last; recommend DEFER.
7. Q10, Q11, Q12 are independent of the schema chain and can be decided any time.

## What happens on silence

Nothing. No field is added, no instruction changes, no INTENT slice is published. The RUNNING slices (S1, S6, S7) describe standing doctrine and may be used regardless. The brief stays as a reference document.
