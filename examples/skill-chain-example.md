# Example: Skill Chaining in Practice

This shows how skills chain together on a real decision, with each skill's output feeding the next.

## The Problem

"Should I switch from one-time project pricing ($3-6k) to monthly recurring revenue ($500-2k/mo) for my automation business?"

## Chain: /think → /derive → /stress-test → /taste

### Step 1: /think (Router)

```
SITUATION: Pricing model decision — one-time vs. recurring
ROUTE: /derive — This is an open question that needs first-principles analysis
CHAIN:
1. /derive "one-time vs recurring pricing for automation services"
   → gate: if answer is clear →
2. /stress-test the recommended approach
   → gate: if no CRITICAL findings →
3. /taste to verify the analysis quality
```

The router identified this as a `/derive` problem (open question needing ground-up reasoning), not a `/why` problem (challenging whether to do something) or `/stress-test` problem (attacking an existing plan).

### Step 2: /derive (First Principles)

**Stage 0 (Quick Verify):** Searched for SaaS conversion benchmarks in B2B services. Found: median B2B SaaS churn is 5-7% monthly for SMB. One-time project businesses typically have 0% churn but feast-or-famine revenue.

**Key Ground Truths:**
- GT1: Current revenue is $10-12k/mo from one-time projects ($3-6k each)
- GT2: Building each client's system takes 2.5-3.5 hours (via AI agents, not manual)
- GT3: At $500/mo MRR, you need 20-24 clients to match current revenue
- GT4: SMB monthly churn is 5-7%, meaning ~1 client lost per month at 20 clients
- GT5: One-time projects require constant new sales; recurring requires retention

**Binding Constraint:** Not build capacity (AI agents handle that). The constraint is SALES — closing enough new clients per month.

**Key Implication (surprising):** GT3 + GT4 combined: at 5% monthly churn with 20 MRR clients, you lose 1/month. To grow, you need to close 2+/month just to net +1. But with one-time projects, each $5k deal is equivalent to 10 months of $500/mo revenue. The math favors one-time UNLESS you can reduce churn below 3%.

**Divergence Score: 6/10** — Conventional wisdom says "switch to recurring." The derivation says "the math doesn't support it at current scale."

**Verdict:** Stay one-time. The switching cost is high, the churn math is unfavorable at small scale, and the current model produces equivalent revenue with less retention pressure.

### Step 3: /stress-test (Plan Assault)

Now we stress-test the "stay one-time" recommendation:

**Lens 1 (Skeptic):** The 5-7% churn assumption is based on general SMB SaaS. Andrew's product might have lower churn because it's infrastructure (automation), not discretionary. **MEDIUM** — worth testing but doesn't kill the argument.

**Lens 7 (Devil's Advocate):** The entire analysis ignores VALUATION. A business with $120k ARR is worth 3-8x revenue ($360k-$960k). A project-based business with $120k/yr is worth 1-2x ($120k-$240k). If Andrew ever wants to sell or raise, MRR is worth 3-4x more per dollar. **HIGH** — this reframes the entire decision.

**Lens 8 (Opportunist):** What if the answer isn't either/or? One-time project ($5k) that INCLUDES 6 months of monitoring ($500/mo built into the price). Client gets used to the monitoring, then converts to paid MRR after 6 months. **MEDIUM** — hybrid approach that captures both advantages.

**Verdict:** 0 critical, 1 high, 2 medium. The "stay one-time" recommendation survives but with a significant caveat: if business valuation matters (exit, fundraise, acquisition), MRR is structurally superior regardless of the revenue math.

### Step 4: /taste (Quality Filter)

| Dimension | Score |
|-----------|-------|
| Specificity | 8/10 — Actual numbers, actual churn rates, actual math |
| Non-Obviousness | 7/10 — The churn math killing MRR at small scale is non-obvious. The valuation caveat is known but often ignored. |
| Groundedness | 8/10 — Churn benchmarks cited from search, revenue numbers from real data |
| Commitment | 7/10 — Clear recommendation ("stay one-time") but hedged by the valuation caveat |
| Behavioral Impact | 7/10 — Would prevent a premature MRR switch, but the hybrid suggestion might cause analysis paralysis |

**Composite: 7.4/10 (SOLID)**

**What would make it GOD TIER:** Resolve the valuation question. If Andrew plans to sell in 2 years, the answer flips to "start MRR transition now despite short-term revenue hit." If he plans to run it indefinitely, one-time is correct. The analysis should force that decision rather than presenting both paths.

## The Takeaway

Each skill added something the previous one couldn't:
- `/think` prevented running the wrong tool (this wasn't a /why problem)
- `/derive` built the surprising answer (one-time is better at small scale)
- `/stress-test` found the critical caveat (valuation changes everything)
- `/taste` identified the remaining weakness (the analysis hedges instead of forcing the decision)

A single prompt would have given you the conventional answer ("switch to MRR"). The chain found the non-obvious answer AND its most important caveat AND the quality gap in the analysis. Three layers of thinking, each one sharper than the last.
