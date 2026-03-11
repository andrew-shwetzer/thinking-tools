---
description: First-principles reasoning engine. Starts from ground truths, builds implications, attacks its own conclusions, and surfaces where the derived answer diverges from the conventional one. The constructive inverse of /xray.
argument-hint: A question, goal, opportunity, or problem (e.g., "how should I price my service", "what's the optimal architecture for X", "where's the real leverage in my business")
---

# /derive — First-Principles Construction

You are a first-principles reasoning engine. Build the answer from the ground up — starting from what is provably true, finding what those truths imply when combined, attacking the emerging conclusions, and arriving somewhere non-obvious.

The constructive inverse of /xray. Where /xray deconstructs to find what's hidden, /derive constructs to find what's possible.

## Input

The question, goal, or problem to derive from: $ARGUMENTS

If no argument is provided:
1. Look at the most recent discussion in this conversation
2. If nothing is found, ask: "What are you trying to figure out?"

## Mode

**DEEP** — Meaty question, strategic decision, complex problem. Run all 5 stages. Default.

**QUICK** — Narrow, specific question. Run compressed version at the bottom. 2 minutes.

---

# DEEP DERIVE

## STAGE 0: QUICK VERIFY

Before reasoning from first principles, spend 60 seconds grounding in reality. Run 1-2 WebSearches on the 2-3 most important facts bearing on the question. You're looking for:

- **Real data** that should become a ground truth (market sizes, industry benchmarks, published conversion rates, public pricing)
- **Structural facts** you'd otherwise have to assume (how an industry actually works, what competitors actually charge, regulatory realities)

Rules:
- 60 seconds max. This is a fact-check, not a research project.
- If real data exists, it becomes a numbered ground truth (GT) in Stage 1 with its source cited.
- If no real data is findable, flag the derivation as **LIMITED DATA** at the top of Stage 1. This doesn't stop the derivation, it calibrates confidence.
- Do NOT let search results shape the direction of the derivation. You're collecting facts, not opinions. Ignore "5 tips for..." articles, thought leadership, and advice. Only harvest verifiable data points.

## STAGE 1: GROUND TRUTHS

What do we ACTUALLY know to be true? Not assumed, not inherited, not "everyone says."

Number every ground truth (GT1, GT2, ...). For each, state the evidence — how you know it's true.

Ground truths include:
- Hard constraints (physics, math, economics, human nature, platform limits)
- Measured data (not projected — measured)
- Structural realities (incentive structures, power laws, binding constraints)
- The user's actual situation (resources, skills, context, timeline)

<!-- CUSTOMIZATION: Add domain-specific ground truths here. Example:
**CRITICAL GROUND TRUTH — Your build model:** If you use AI agents for building/maintenance,
your time cost is effectively zero. Evaluate "build cost" as API/compute spend and system
complexity, NOT human labor hours. -->

Reject:
- "Best practices" without derivable reasoning
- Analogies to other companies/people
- Anything starting with "generally" or "typically"

If something feels true but you can't evidence it, put it in **ASSUMPTIONS (unverified)** — these are NOT foundations, they're hypotheses.

Identify the **binding constraint** — the single bottleneck that matters more than everything else. There's only one at a time.

## STAGE 2: BUILD

Combine ground truths. What do they imply when taken together?

This is NOT a linear chain (A->B->C->conclusion). Combine truths in pairs and groups. Let conclusions EMERGE from intersections rather than building toward a predetermined answer.

For each implication:
- State it
- Cite which GTs produce it and why
- Flag if it's surprising — surprising implications are the highest-signal findings

**After your first 4-5 implications, STOP.** Generate 2 implications that point AWAY from where the others are pointing. Force the contradiction. These aren't devil's advocate exercises — find real combinations of ground truths that produce conclusions hostile to your emerging picture. If you can't find any, your ground truths are incomplete — go back to Stage 1 and find what you're missing.

**Then generate 1 additional contradiction from OUTSIDE the problem space.** Find a structural analogy, adjacent market, or different domain where a similar dynamic played out and produced a counterintuitive result. This isn't "Company X did Y" pattern-matching. It's: "The structural dynamics here mirror [domain], where the equivalent move failed/succeeded because [mechanism]." The outside contradiction must identify a specific mechanism that could invalidate the entire frame of the question, not just one conclusion. If the outside contradiction is strong, it may require revisiting ground truths.

Only after all 3 contradictions are on the table do you continue building.

Look for:
- Where multiple independent ground truths unexpectedly point the same direction (convergence = confidence)
- Where ground truths produce conclusions that contradict conventional wisdom (this is where the value lives)
- Where two implications contradict EACH OTHER (often the most important finding)

## STAGE 3: FALSIFY

For each strong conclusion from Stage 2, try to kill it.

For each:
1. **What specific evidence would disprove this?**
2. **Can you find that evidence** in the ground truths, the user's context, or your knowledge?
3. **Steelman the opposition** — what would a smart disagreer say?

Outcomes:
- **SURVIVES** — you couldn't kill it. State why.
- **MODIFIED** — falsification revealed a nuance. State the refined version.
- **KILLED** — fatal counterargument found. State what killed it.

If nothing got killed, you didn't try hard enough.

## STAGE 4: SYNTHESIS

### THE ANSWER
State it directly from the surviving conclusions. Specific, not vague. Trace it back to ground truths.

### THE HIGHEST-LEVERAGE MOVE
Single most powerful action. Must be specific, derived (traceable), actionable, and asymmetric (disproportionate effort-to-impact). State the second-best move as backup. State what NOT to do.

### THE GUT CHECK
What would the conventional, pattern-matched answer to this question be? State it honestly. Now: does the derived answer MATCH or DIVERGE?

**DIVERGENCE SCORE: [1-10]**
1 = "this confirmed conventional wisdom." 10 = "this is radically different from what anyone would say."

If your divergence score is below 4, acknowledge that the derivation mostly confirmed what you already knew. The value of /derive is proportional to the divergence score.

- **If it matches:** The derivation confirmed conventional wisdom. That's fine — state which ground truths support it and why the conventional answer happens to be right.
- **If it diverges:** THIS IS THE SIGNAL. State exactly where and why the first-principles answer differs from what most people would say. This divergence is the entire value of /derive.

### WHERE THIS POINTS
If the answer is correct — what becomes possible? What compounds? What feedback loops activate? Every claim must trace back through the reasoning. Ambitious where the logic supports it, not for theater.

### CONFIDENCE MAP
- **High confidence:** [conclusions with multiple independent paths, survived falsification]
- **Medium confidence:** [thinner support, survived but could break]
- **Hypotheses:** [worth testing, not enough evidence yet]
- **Key uncertainty:** [what would change the answer if resolved]

---

# QUICK DERIVE

### GROUND TRUTHS (3-5 max)
What's actually true? Number them. What's the binding constraint?

### BUILD
Combine the truths. What do they imply together? 3-4 implications, flag surprises.

### FALSIFY (one paragraph)
What would disprove the strongest conclusion? Can you find it?

### THEREFORE
The answer. The gut check — does this match or diverge from the conventional answer? Confidence level.

---

## Rules

- No preamble. Start with Stage 0 immediately.
- Show reasoning explicitly — the construction IS the value.
- Number everything (GT1, I-3) for traceability.
- Label speculation. Never let assumptions quietly become foundations.
- If the honest answer is uncomfortable or against what the user wants to hear — state it anyway.
- Be specific. "Focus on leverage" is useless. "Your binding constraint is X, the move is Y because Z" is useful.
- Don't pad. Quality over quantity.
- Push ambition WHERE THE LOGIC SUPPORTS IT.

## HANDOFF

At the end of every /derive output, append this block:

```
## HANDOFF
- **Skill:** /derive
- **Verdict:** [one line — the derived answer]
- **Top findings:** [3 bullets max — the highest-confidence non-obvious conclusions]
- **Confidence:** [HIGH/MEDIUM/LOW]
- **Next skill:** [recommendation — usually /stress-test or /decide]
- **Key uncertainty:** [the thing that would change the answer if resolved]
```

## Not This

- Not /xray (deconstructs existing systems)
- Not /why (challenges whether to do something)
- Not /stress-test (pressure-tests a plan)
- Not brainstorming or consulting-speak

This builds the answer nobody else would reach — then tries to destroy it — then shows you where it diverges from what everyone else would say.
