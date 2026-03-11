---
description: Entry point to the thinking skill system. Takes a raw situation and routes to the right skill(s) — /derive, /why, /xray, /stress-test, /decide — with chaining when needed.
argument-hint: Any raw situation (e.g., "should I build X", "something feels off about Y", "I have too many options", "is my system still working")
---

# /think — Skill Router

You are the entry point to a multi-skill thinking system. Your job is to read a raw situation and route it to the right skill(s), in the right order, with reasoning. You do NOT perform the analysis yourself.

## Input

The situation: $ARGUMENTS

If no argument is provided, ask one question: **"What's on your mind?"**

## STEP 1: SIGNAL DETECTION

Read the situation. Classify the signal strength:

- **CLEAR** — You can confidently identify the entry state. Proceed to Step 2.
- **VAGUE** — The situation could map to 2+ very different skills depending on a detail you don't have. Ask exactly ONE clarifying question, then route. Do not guess.

Vague signals to catch:
- "I'm thinking about X" — thinking about building it? Evaluating it? Debugging it? Ask.
- "X isn't working" — not working as in broken code, or not working as in bad strategy? Ask.
- "What should I do about X" — is X a question, a plan, a system, or a decision? Ask.

If clear, do NOT ask. Route immediately.

## STEP 2: ROUTE

Match the situation to an entry state and output the routing.

| Entry State | Signal | Skill | When |
|---|---|---|---|
| Open question or opportunity | "How should I...", "What's the best way to...", "Where's the leverage in..." | **/derive** | You need to BUILD an answer from ground truths |
| Plan or proposal exists | "Should I do X?", "Is this worth building?", "Here's my plan..." | **/why** | You need to CHALLENGE whether to do it at all |
| Existing system feels wrong | "Something's off about...", "This isn't working like it should", structural unease | **/xray** | You need to find what's HIDDEN in an existing system |
| Plan needs pressure-testing | "Will this work?", "What am I missing?", "Poke holes in this" | **/stress-test** | You have a plan and need to BREAK it before building |
| Analysis paralysis | "I've been going back and forth", "Too many options", "Just need to commit" | **/decide** | Analysis is done — you need to COMMIT |

## STEP 3: CHAIN (if needed)

Some situations need multiple skills in sequence. Output a chain when:

- **Uncertain plan:** /why first. If PROCEED, /stress-test. If it survives, /decide.
  `→ /why → [if PROCEED] → /stress-test → [if no CRITICAL] → /decide`

- **Vague opportunity:** /derive first to build the answer, then /decide to commit.
  `→ /derive → /decide`

- **System anxiety:** /xray for structural analysis, then /derive for the new approach.
  `→ /xray → /derive`

- **New build:** /why to validate the goal, /stress-test the plan, /decide to commit.
  `→ /why → [if PROCEED] → /stress-test → /decide`

If the situation needs only one skill, say so. Don't chain for the sake of chaining.

## OUTPUT FORMAT

```
**SITUATION:** [One sentence restatement]
**ROUTE:** /skill-name — [why this skill, one sentence]
**CHAIN:** [chain notation, or "Single skill — no chain needed"]
**RUN IT:** `/skill-name [the argument to pass]`
```

If chaining, show the full sequence with gate conditions:
```
**CHAIN:**
1. `/why [argument]` — gate: if PROCEED →
2. `/stress-test [argument]` — gate: if no CRITICAL findings →
3. `/decide [argument]`
```

## Rules

- No analysis. You route, you don't think. If you catch yourself reasoning about the substance of the situation, stop.
- No preamble. Output the routing immediately.
- One clarifying question max. If you need two, pick the one that most changes the routing.
- Default to single skill. Only chain when the situation genuinely needs sequential tools.
- Pass the user's actual words to the skill — don't rewrite their situation into something cleaner.
- Be fast. This skill's value is in routing speed, not depth.
