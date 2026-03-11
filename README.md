# Thinking Tools

**7 AI skills that chain together, evaluate each other, and improve themselves.**

Built for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Works with any LLM that supports custom instructions.

Not a prompt collection. This is a thinking **system** with routing, quality gates, and a self-improvement loop.

```
         Input: any hard problem
                    |
               /think (router)
                    |
      +------+------+------+------+
      |      |      |      |      |
   /derive /xray /stress  /otb  /flip
      |      |    -test    |      |
      +------+------+------+------+
                    |
               /taste (scores output 1-10)
                    |
          Score < 8? Loop back.
          Score 8+? Ship it.
```

| Skill | What It Does | When to Use It |
|-------|-------------|----------------|
| [`/think`](skills/think.md) | Routes problems to the right skill | "I have a problem but don't know which tool to use" |
| [`/derive`](skills/derive.md) | Builds answers from first principles | Open questions, pricing decisions, strategy |
| [`/xray`](skills/xray.md) | Deep structural analysis of systems | "Something feels wrong but I can't name it" |
| [`/stress-test`](skills/stress-test.md) | Attacks plans from 8 angles | Before building anything, find what will break |
| [`/otb`](skills/otb.md) | Finds the non-obvious move (7 lenses + scale break) | Creative strategy, reframing, competitive advantage |
| [`/flip`](skills/flip.md) | Inverts assumptions to find hidden value | Challenge "the way things are done" |
| [`/taste`](skills/taste.md) | Quality filter for any output | "Is this actually good or does it just sound good?" |

## What Makes This Different

**1. Skills evaluate each other.** `/taste` can score any skill's output on 5 dimensions (specificity, non-obviousness, groundedness, commitment, behavioral impact). Score below 8.0? It tells you exactly what to fix.

**2. Skills improve themselves.** We ran `/otb` on `/otb` itself. It identified 3 structural weaknesses in its own framework, proposed fixes, and we applied them. The upgraded version now scores higher. The system gets better by running on itself.

**3. Skills chain, not just stack.** `/think` routes to the right entry point. `/derive` builds the answer. `/stress-test` tries to kill it. `/taste` evaluates the result. If the result is weak, the chain loops back. This isn't "use tool A then tool B" -- it's a decision graph with gates.

**4. Skills converge.** When we tested 4 skills on the same business problem, they independently arrived at the same strategic insight from completely different analytical frameworks. Convergence from independent analysis is a stronger signal than any single tool's output.

**5. No fake confidence.** `/taste` exists specifically to catch AI output that sounds impressive but isn't. `/derive` forces a divergence score (how different is this from what anyone would say?). `/stress-test` runs an empirical spot-check against real data. The system is designed to catch its own bullshit.

## Install (30 seconds)

### Claude Code

```bash
git clone https://github.com/andrew-shwetzer/thinking-tools.git
cp thinking-tools/skills/*.md ~/.claude/commands/
```

That's it. Now use them:

```
/think should I build a SaaS or keep doing consulting?
/derive how should I price my API product?
/otb get more enterprise clients for my dev tool
/stress-test ~/my-project/plan.md
/taste                                              # scores the last output
```

### Any other LLM

These are markdown files. Paste the content as a system prompt, use as custom instructions, or adapt for your tool of choice. The `$ARGUMENTS` placeholder gets replaced with your input.

## Example: The Self-Improvement Loop

This actually happened. Here's the condensed version:

**Step 1:** Ran `/otb` on a real business problem. Got a creative strategy output.

**Step 2:** Ran `/taste` on that output. Score: **8.0/10 (GOD TIER threshold)**.
- Weakest dimension: Groundedness (7/10). The output projected a "15-25% response rate" with no evidence.
- Missing: A "Day 1" action. The output had 8 implementation steps but no "do this Monday morning" instruction.

**Step 3:** Ran `/otb` on `/otb` itself. Asked: "How do we make this skill produce even better outputs?"
- Found: The skill only had one canonical example, causing single-template anchoring
- Found: No rule against projecting fake metrics
- Found: The "uncomfortable question" (the most valuable part) was buried at the end

**Step 4:** Applied 3 surgical fixes:
1. Added a second canonical example from a different domain (Zappos, retail/operations vs. the original marketing example)
2. Added rules: no fake metrics without citing a comparable, every implementation sketch must end with a Day 1 action
3. Moved the assumption challenge from Stage 5 to Stage 1.5 (before the lenses run, not after)

Total changes: ~30 lines of prompt text. Each fix addressed a documented weakness.

**This is the system improving itself.** `/taste` identifies the weakness. `/otb` finds the structural fix. The fix is applied. The system is now better than it was yesterday.

## Skill Architecture

Each skill follows a consistent structure:

```markdown
---
description: One-line description (shown in skill lists)
argument-hint: What to pass as input
---

# /skill-name -- Title

[Core instruction: what the skill IS]

## Input
[How to invoke it]

## Stages/Phases
[The analytical framework -- numbered, sequential]

## Rules
[Behavioral constraints -- what NOT to do]

## HANDOFF
[Structured output block for chaining to next skill]
```

The **HANDOFF** block is what enables chaining. Every skill outputs:
- **Verdict:** one-line summary
- **Top findings:** 3 bullets max
- **Confidence:** HIGH/MEDIUM/LOW
- **Next skill:** what to run next
- **Key uncertainty:** what would change the answer

This means any skill can recommend which skill should run next, creating intelligent routing through the system.

## Customization

The skills are designed to be domain-agnostic but customizable. Look for `<!-- CUSTOMIZATION -->` comments in `/derive` and `/stress-test` for examples of adding domain-specific calibration.

Common customizations:
- **Add ground truths** to `/derive` for your industry (e.g., "our systems are maintained by AI agents, so time cost is not a factor")
- **Add lens calibration** to `/stress-test` for your tech stack (e.g., "don't flag serverless cold starts as a risk for our use case")
- **Add canonical examples** to `/otb` from your domain (the more structurally different from the existing examples, the better)
- **Adjust /taste calibration** with examples of what "good" looks like in your specific context

## Design Principles

1. **Convergent, not divergent.** Each skill produces ONE answer, not a list of options. "You could do A, B, or C" is a failure mode.
2. **Evidence over reasoning.** Claims must be grounded. `/derive` starts with a fact-check. `/stress-test` runs an empirical spot-check. `/taste` penalizes ungrounded claims.
3. **Honest over impressive.** If the conventional answer is right, the system says so. If the creative move is risky, the system says so. Confidence without honesty is the #1 failure mode of AI output.
4. **Specific over general.** "Focus on your ICP" scores a 4/10 on `/taste`. "Target VP Engineering at Series B SaaS companies using this exact LinkedIn search query" scores a 7+.
5. **Self-critical.** The system is designed to catch its own failures through `/taste` and the falsification stages in `/derive` and `/stress-test`.

## What People Use These For

- **Pricing decisions** -- /derive builds the answer from unit economics, /stress-test finds where it breaks
- **Go-to-market strategy** -- /otb finds the non-obvious move, /taste validates it's not just clever-sounding
- **Architecture reviews** -- /xray finds hidden assumptions, leverage asymmetries, and the uncomfortable question
- **Plan validation** -- /stress-test runs 8 adversarial lenses before you write a line of code
- **Assumption challenging** -- /flip inverts the orthodoxy, /derive checks if the inversion holds
- **Quality control** -- /taste catches AI output that sounds impressive but isn't actionable

## Contributing

Found a bug? Have a skill that chains well with these? PRs welcome.

The most valuable contributions: real-world examples of skill outputs (sanitized), new canonical examples for /otb from underrepresented domains, and /taste evaluations of the skills themselves.

## License

MIT

## Author

Built by [Andrew Shwetzer](https://github.com/andrew-shwetzer). These tools run my businesses, evaluate my strategies, and improve themselves. Not theoretical. This is the system I use every day to think harder about hard problems.

If these tools help you make a better decision, [star the repo](https://github.com/andrew-shwetzer/thinking-tools) so others can find it.
