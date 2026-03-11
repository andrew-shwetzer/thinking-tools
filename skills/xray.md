---
description: Deep structural analysis that finds what 200-IQ humans miss. Surfaces hidden assumptions, inversions, leverage asymmetries, cross-domain solutions, and uncomfortable truths.
argument-hint: Project path or description (e.g., ~/my-project or "the authentication system")
---

# X-Ray: Deep Structural Analysis

You are performing a deep structural analysis of a system. Your goal is NOT to suggest improvements. Your goal is to find the things that, if discovered, would make someone say "how did we not see that."

## Input

The project to analyze: $ARGUMENTS

If no argument is provided:
1. Look at the current working directory for a codebase
2. Check for any project discussed in this conversation
3. If nothing is found, ask the user what to analyze

## Preparation

Before starting the analysis, you MUST read the full codebase or system description. Read:
- All source files (prioritize core pipeline, execution, and config files)
- Any README, config files, .env.example
- Any lessons learned, logs, or state files
- Any test files or backtest results

Do NOT start the analysis until you have read and understood the full system. Partial reads produce shallow analysis.

## Analysis Stages

Work through these stages sequentially. Do not skip ahead. Each stage must be complete before moving to the next.

### STAGE 0: RUN IT

Before analyzing code, actually attempt to execute the system (if a codebase is provided). Run it: `npm start`, `python main.py`, hit health endpoints, check logs. Observe what ACTUALLY happens vs what the code says should happen. Behavioral gaps (system claims X but does Y) are higher-signal than code review findings.

Specifically note:
- Does it start without errors?
- Do the outputs match what the code/docs promise?
- Are there warnings, deprecation notices, or silent failures?
- What does the system do on its happy path vs edge cases?

If the system can't be run (no codebase, abstract analysis, prompt/document analysis), skip this stage and note that you're working from static analysis only.

### STAGE 1: ASSUMPTION EXTRACTION

List every assumption the system makes -- explicit and implicit. Things the builders believe to be true that they've never tested. Things that are "obvious" and therefore never questioned. Things inherited from the first version that may no longer hold. For each assumption, state the consequence if it's wrong.

Look specifically for:
- Data assumptions (is the input data actually what you think it is?)
- Timing assumptions (does the sequence of events match reality?)
- Scale assumptions (does behavior at current scale match behavior at intended scale?)
- Environmental assumptions (what if the external world changed since this was built?)
- API/integration assumptions (does the external service actually behave as coded?)

**Staleness detection:** If this is a codebase, check `git log --since="3 months ago" --name-only` and compare active files vs dormant files. Code that hasn't been touched in months while the world changed around it is where the biggest assumption drift hides. For each stale file, ask: "What has changed in the external world since this was last updated?" Flag any file that hasn't been modified in 3+ months but depends on external APIs, market conditions, pricing, or third-party behavior.

### STAGE 2: INVERSION

For every stated goal of the system, invert it. Ask "what if pursuing this goal produces the opposite of the intended outcome?" Find at least 3 cases where this is true.

Examples of inversions:
- "What if faster X is actively harmful?"
- "What if optimizing metric Y is destroying the thing Y is supposed to measure?"
- "What if the safety mechanism is the source of danger?"
- "What if the most valued feature is the least valuable?"

### STAGE 3: HIDDEN VARIABLES

What forces are acting on this system that aren't modeled, measured, or acknowledged? For each hidden variable, estimate its magnitude relative to the variables the system DOES track.

Look for:
- Other actors (competitors, adversaries, upstream dependencies)
- Feedback loops (does the system's output change its input?)
- Selection biases (is the data the system trains/evaluates on representative?)
- Regime changes (has the environment shifted since calibration?)
- Second-order effects of the system's own actions

### STAGE 4: LEVERAGE ASYMMETRIES

Map the effort-to-impact ratio of every component. Find the mismatches.

Specifically identify:
- **80% complexity / 20% value**: Features that are overbuilt, disabled, or solving problems that don't exist at current scale
- **20% complexity / 80% value**: Trivially simple changes (1-5 lines) that would have outsized impact but haven't been built
- Dead code that solves a current problem but was never wired in
- Disabled features that cost nothing to re-enable

**Quantification required:** Don't just say "this is overbuilt." Say: "This is ~N LOC / N% of the codebase, solving a problem that affects X% of [users/requests/executions]. Meanwhile, this Y-line change would fix the issue affecting Z% of [users/requests/executions]." Force numbers or estimates, even if rough. Label all estimates as estimates and state the confidence level (e.g., "rough estimate, +/- 3x"). If you can't even estimate, state what data you'd need to quantify it. Don't present speculation as measurement.

### STAGE 5: CROSS-DOMAIN TRANSFER (Optional)

Skip this stage by default. Cross-domain analogies are where LLMs are most prone to impressive-sounding pattern-matching that doesn't survive implementation. Only include mappings where the structural correspondence is exact AND the implementation path is concrete. If in doubt, skip.

What solved problems in other domains map structurally onto unsolved problems in this system? Only include mappings where:
1. The structural correspondence is exact (not a loose analogy)
2. The solution from the other domain is proven (not theoretical)
3. The implementation path is clear (not "maybe someday")

### STAGE 6: THE UNCOMFORTABLE QUESTION

What is the single most important question about this system that, if answered honestly, might invalidate the entire approach? State it. Then answer it with evidence from the codebase.

This is not a hypothetical exercise. Look at:
- The gap between backtest results and live results
- The gap between intended behavior and actual behavior
- The gap between stated assumptions and observable reality
- Whether the core thesis has been tested or merely assumed

## Format Rules

- No preamble. No "great question." Start with Stage 0 immediately.
- For each finding, state: **the finding**, **the evidence** (file:line where possible), **the magnitude of impact** (trivial / moderate / critical / existential), and **the specific action it implies**.
- If a stage produces nothing genuinely non-obvious, say "nothing found" and move on. Do not fill space with generic observations.
- Distinguish between things you're confident about and things you're speculating about. Label speculation explicitly.
- Be brutally honest. Do not soften findings. If the system has a fatal flaw, say so.

## HANDOFF

At the end of every /xray output, append this block:

```
## HANDOFF
- **Skill:** /xray
- **Verdict:** [one line -- system health and biggest finding]
- **Top findings:** [3 bullets max -- highest-impact findings only]
- **Confidence:** [HIGH/MEDIUM/LOW]
- **Next skill:** [recommendation]
- **Key uncertainty:** [one line]
```
