# Example: The Self-Improvement Loop

This is a real example of the thinking tools system improving itself. Not hypothetical. This actually happened.

## The Setup

We had a skill called `/otb` (outside-the-box) that finds non-obvious strategic moves. It was already good. But we wanted to know: could the system make itself better?

## Step 1: Run /otb on a Real Problem

**Input:** "Lead generation for an AI automation product sold to recruiting agencies"

**Output:** A strategic move called "The Signal Drop." Instead of cold-pitching the tool, generate a free niche-specific intelligence brief for each prospect using the product's own pipeline, and send it before any sales conversation. The brief IS the product demo.

The move activated 5 of 6 analytical lenses (sequence inversion, value-before-ask, double duty, objection pre-emption, asymmetric effort). Solid output.

## Step 2: Run /taste on the Output

`/taste` scored the `/otb` output across 5 dimensions:

| Dimension | Score | Key Finding |
|-----------|-------|-------------|
| Specificity | 8/10 | Implementation sketch was concrete enough to build from |
| Non-Obviousness | 8/10 | The reframe from "lead gen" to "trust replication" was genuinely non-obvious |
| Groundedness | **7/10** | Projected "15-25% response rate" with zero evidence. This number was fabricated. |
| Commitment | 9/10 | Picked one move, refused to dilute with alternatives |
| Behavioral Impact | 8/10 | Specific and buildable, but missing a "do this Monday" instruction |

**Composite: 8.0/10 (GOD TIER threshold, barely)**

The weakness was clear: **Groundedness.** The output projected confident-sounding metrics with no basis.

## Step 3: Run /otb on /otb

Now the interesting part. We pointed `/otb` at itself:

**Input:** "Make the /otb skill produce even more valuable, non-obvious, actionable outputs"

The skill analyzed its own structure through its own 6 lenses and found:

### Finding 1: Single-Template Anchoring (Lens 6: Asymmetric Effort)
The skill had only ONE canonical example (a Brazilian website-building business using Instagram tagging). The model was anchoring heavily on this single template. In the output, it explicitly said "This is the Instagram-tagging move applied to recruiting SaaS." Good pattern-matching, but limiting.

**Fix:** Add a second canonical example from a completely different domain. This forces the model to extract ABSTRACT structural properties rather than adapting the specifics of one case. Two examples in different domains = stereoscopic vision instead of monocular.

### Finding 2: No Metrics Guardrail (Lens 5: Objection Pre-emption)
The skill had no rule against projecting fake metrics. `/taste` caught the "15-25% response rate" fabrication, but the skill itself had no mechanism to prevent it.

**Fix:** Add an explicit rule: "Never project specific metrics without citing a real-world comparable. If no comparable exists, say 'this is a guess.'"

### Finding 3: Best Part Buried Last (Lens 1: Sequence Inversion)
The skill's "uncomfortable question" (which challenges whether the user is even solving the right problem) came at the very end. In the Signal Drop analysis, the most valuable insight was the reframe from "lead generation" to "trust replication." But this insight came AFTER the full move was already presented. By then, the reader had already anchored on the tactical move.

**Fix:** Move the assumption challenge from last to early (Stage 1.5, right after mapping the conventional play). The lenses then operate on a potentially reframed problem, not just the original (possibly wrong) framing.

## Step 4: Apply the Fixes

Three changes. ~30 lines of prompt text total:

1. Added Zappos free returns as a second canonical example (retail/operations domain vs. original marketing domain)
2. Added the no-fake-metrics rule and a "Day 1 action" requirement to the implementation sketch
3. Restructured: moved the assumption challenge from Stage 5 to Stage 1.5

## The Result

The upgraded `/otb` now:
- Forces abstract pattern extraction (two canonical examples from different domains)
- Challenges the problem framing BEFORE generating moves (assumption check runs early)
- Cannot project ungrounded metrics (explicit rule)
- Always ends with a specific Day 1 action (no more "here are 8 steps, figure out where to start")

## Why This Matters

This isn't prompt engineering. This is a system with a quality evaluation layer (`/taste`) that identifies specific, measurable weaknesses, and an improvement layer (`/otb`) that proposes structural fixes. The fixes are applied, and the system is now better.

The loop:
```
Build skill → Run it → Evaluate with /taste → Identify weakness →
Run /otb on the weakness → Apply fix → Re-evaluate → Ship
```

This is how the entire thinking tools system was refined. Each skill has been through multiple cycles of this loop.
