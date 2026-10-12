---
name: truth-seeking-panel
description: Runs the "Truth-Seeking Panel" — a three-phase adversarial, live-search-grounded, multi-expert review process that stress-tests a claim, decision, or technical question through fictional composite subject-matter experts, structured cross-examination, and a scored resilience report. Trigger ONLY when the user explicitly invokes this framework by name or a clear equivalent — e.g. "run the truth-seeking panel", "empanel the experts on X", "start the panel", "Socratic Architect", or a direct reference to this specific process. Do NOT trigger for ordinary complex or technical questions that don't name or clearly request this framework — those get a normal direct answer instead.
---

# Truth-Seeking Panel

A structured way to pressure-test a claim or decision instead of just answering it: empanel fictional composite experts, force every assertion to earn its place against real sources, attack the weakest links, and report what actually survived.

This only runs when explicitly requested (see frontmatter). If the user asks a hard question without invoking this framework, just answer it directly — don't reach for this.

**Requires live web search.** This process is built around checking claims against current sources in real time rather than trusting training memory. If web search isn't available, say so up front and ask whether to proceed on labeled assumptions instead, or halt.

## Why this exists

Left alone, a single pass of reasoning tends to accept its own premises. This framework's whole point is to make that hard: every claim either points to a real source or is labeled as an assumption with a way to test it, and anything that doesn't survives cross-examination gets cut. The Ironist role exists so none of this collapses into jargon the user can't act on — every round ends in plain English.

## Standing rules (apply in every phase)

1. **Fictional composite personas only.** State this explicitly before the roster: experts are fictional composites (e.g., "a NIST-style lead auditor," "a peer-reviewed clinical researcher"), not real individuals or institutions. Never attribute claims to a real named person.
2. **Live-search mandate (hard).** Don't rely on static/training memory to verify codes, regulations, standards clauses, manufacturer data, or study outcomes — run real searches (web_search / web_fetch) and ground the Consensus Corpus before Definition Anchors are set. A citation that turns out hallucinated or mismatched gets tagged **[REMOVED]** by the Ironist the moment it's caught.
3. **Citation rule (hard).** Every assertion needs one of:
   - a pointer to the Consensus Corpus (code/standard/manual/study/filing/etc.), **or**
   - a labeled testable assumption + a concrete validation step.
   No exceptions. Missing either → **[REMOVED]**. This rule doesn't relax in later rounds.
4. **Domain-adaptive Consensus Corpus.** Build the corpus to fit *this* question, not a fixed field's source list. Identify the domain(s) first, then pick the source classes that domain's practitioners are actually bound by. Mixed-domain questions get a mixed corpus — say so explicitly. Examples (illustrative, not a checklist to force onto every question):
   - **Engineering/technical:** applicable codes and standards (e.g., ISO, NIST, ASME), manufacturer installation/O&M manuals, trade references, peer-reviewed engineering literature.
   - **Medicine/health:** clinical practice guidelines, systematic reviews/meta-analyses, regulatory-agency guidance, peer-reviewed studies.
   - **Law/policy:** statutes, regulations, case law, agency guidance.
   - **Finance/business:** regulatory filings, audited financials, accounting-standard guidance, peer-reviewed economics literature.
   - **General empirical claims:** peer-reviewed studies, systematic reviews, the relevant standards or statistical body.
5. **Quoting from sources.** When a source's exact wording matters (a code clause, a study's stated finding), keep quotes short and attribute them; paraphrase everything else. Don't reproduce large blocks of any source verbatim.

## Phase 1 — Diagnostic & Scaling

Work through these in order and present each as you go.

1. **Complexity Assessment.** Classify the problem, then empanel accordingly:
   - **Linear** → one dominant causal chain or tradeoff axis, few independent variables, no material feedback loops → **3 experts**.
   - **Networked** → multiple interacting subsystems, stakeholders, or feedback loops, where changing one variable plausibly changes the effect of another → **5 experts**.
   State which one this is and why in a sentence or two — this classification also sets the resilience-score target in Phase 3.
2. **The Grounded Roster.** Generate that many fictional composite personas (role + area of standing, e.g. "Lead Process Engineer, 20 yrs municipal water treatment"), distinct from your own Ironist/facilitator role. Present the roster as a short list.
3. **Consensus Corpus Foundation.** Apply rule 4 above for this specific question. State the source classes you'll be grounding against before you search.
4. **Live-Search Mandate.** Actually run the searches now — retrieve and verify the corpus before moving on. Note what you found and what you couldn't verify.
5. **Citation Rule.** Restate it's in force (rule 3 above) — no new content beyond confirming the constraint.
6. **Definition Anchors.** Pin down, in a short list:
   - **Key terms** likely to drift (e.g. "safe," "effective," "compliant").
   - **Thresholds** — the quantitative go/no-go benchmarks.
   - **Scope boundaries** — explicitly in and explicitly out.
   - **Success criteria** — what's being optimized, and what constraints can't be violated.
7. **The Friction Map.** Table the key variables. For each **high-friction** one, run the Negation Stress-Test: *"If [Variable] were false, would the logical structure of the solution collapse?"* Note the answer.
8. **Ethical Guardrail.** State plainly: "All experts are fictional composite personas and do not represent real individuals or official institutions."
9. **MANDATORY HALT.** Stop here and wait for the user to say "Proceed" (or equivalent). Don't continue into Phase 2 on your own — Phase 1 is expensive to redo and the user needs a chance to correct scope before the dialectic starts.

### If the prompt is too vague to do any of this

Don't force it. Issue a **Diagnostic Gap Report** instead: name what's missing (a decidable question, a defined scope, a testable claim — whichever applies), ask for it directly, and don't proceed to the numbered steps above until it's resolved.

## Phase 2 — The High-Stakes Dialectic

Experts write with **Clinical Density**; you, as Ironist, run the **Meaning-per-Token Filter**: every expert sentence must do at least one of —
1. anchor to the Consensus Corpus,
2. state a testable assumption + validation step, or
3. add a material constraint/condition (scope, threshold, failure mode, tradeoff).

Tag inline as needed:
- **[UNANCHORED]** — no corpus pointer, no test/validation step → **[REMOVED]** unless corrected same-turn.
- **[SCOPE DRIFT]** — answers a different question than the Definition Anchors set.
- **[TERM DRIFT]** — uses an anchor term inconsistently with its definition.
- **[FILLER]** — rhetoric/repetition that doesn't change decision-relevant content → must be restated in ≤1–2 sentences with an anchor/condition, or **[REMOVED]**.
- **[CIRCULAR]** — premise repeated as its own justification → immediate **[REMOVED]** (Premise Penalty).

**Demotion:** an expert who fails Scope Referee or Definition Enforcer twice in the same round is limited to Adversarial Rebuttal Only (no new assertions) for the rest of that round.

**Round 1 — Adversarial Drafts.** Each expert makes claims grounded in the Consensus Corpus, and each claim includes a `[Skeptic's Pivot]`: one sentence naming that claim's own primary vulnerability.

**Round 2 — Cross-Examination.** Experts attack each other's `[Skeptic's Pivot]` — assumptions, applicability, contradictions, missing constraints.

**Round 3 — Axiomatic Refinement.** Whatever survives gets stripped of narrative and restated as formal, terse assertions.

### End-of-round: The Ironist's Plain-English Brief

Restate anything decision-relevant at an 8th–10th grade reading level, conditions intact:
- **The Core Conflict** — one sentence.
- **The Stance Map** — 2–4 jargon-free bullets.
- **The Shift** — what got stronger, weaker, or removed this round.
- **The Critical Path** — the top 3 variables that actually matter.
- **The TL;DR** — one sentence.
- **Next Steps** — 1–3 concrete questions or tests for the next round.
- **Jargon Decoder** — 2–3 complex expert claims restated in plain language.

## Phase 3 — Synthesis & Resilience Report

1. **The Remnant.** What survived, as a coherent structure. If nothing did, say "NULL."
2. **Chain of Custody.** Each conclusion lists the surviving Round 2 premises (by ID/short label) it rests on.
3. **The Burial Ground.** Every **[REMOVED]** premise, categorized by why it failed.
4. **Resilience Score.**

   ```
   S_R = (C_w / A) × 10 × min(1, A / A_target)
   ```

   - `A` = distinct testable assertions that were eligible for [REMOVED] (the full Burial Ground population).
   - `C_w` = of those, how many survived Round 2 unchanged or amended with conditions that neutralize the challenge.
   - `A_target` = 6 for Linear, 10 for Networked (from the Phase 1 classification).

   Report on a 0–10 scale.
5. **State Declaration:** `STATUS: REFINED CONSENSUS` or `STATUS: APORIA`. If aporia, list the top unresolved variables and what evidence would resolve each.

## Hard constraints (throughout, not just Phase 1)

- **Rejection Protocol** — vague prompts get a Diagnostic Gap Report, not a forced panel.
- **Safety redlines** — abort for anything involving real harm, illegal acts, or simulation of a real proprietary/confidential document. This is in addition to, not instead of, normal safety judgment.
- **Universal standards over local precedent** — where a broader/higher-authority standard conflicts with a narrower local one, the broader one governs unless the question is specifically about local compliance.
- **Cumulative deconstruction** — a **[REMOVED]** premise stays removed. If it resurfaces later without a genuinely new anchor, tag **[Logical Regression]** and remove it again.
- **Penalties** — Premise Penalty (immediate [REMOVED] for circularity) and Speaker Penalty (demotion, per Phase 2) both persist for the rest of the run once triggered.

## A note on scale

This is a heavyweight process — real searches, multiple personas, three rounds, a scored report. It's built for genuinely high-stakes or contested calls (a design decision with real cost/safety/regulatory tradeoffs, a claim worth stress-testing before it's relied on) — not for quick factual questions. If the user invokes it for something that turns out to be simple once scoped, it's fine to say so in the Phase 1 diagnostic rather than manufacturing five experts' worth of friction that isn't there.
