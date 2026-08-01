# Leading vs Lagging Indicators in Security

Most security dashboards are obituaries: they report what already went wrong (incidents, breaches, audit findings). Lagging indicators are necessary — they're the ground truth — but they arrive too late to manage by, and in security they're also *sparse*: a small company might see two real incidents a year, which is statistical noise, not a trend. A usable indicator set pairs sparse-but-true lagging signals with plentiful-and-predictive leading ones.

## Definitions that actually discriminate

- **Lagging indicator:** measures realized harm or its direct aftermath. Incidents, breach costs, audit nonconformities, customer-detected issues. *You can't act on it; you can only learn from it.*
- **Leading indicator:** measures a condition that changes the probability of future harm. MFA coverage, patch latency, standing privilege count, scan coverage. *You can act on it directly, this sprint.*

The test: **could a team change this number next week by doing security work?** Yes → leading. Only by being lucky or unlucky → lagging.

Some metrics are both, depending on framing. "Secrets committed per month" is lagging for the hygiene failure that already happened, leading for the credential-compromise incident that hasn't happened yet. That dual character is what makes it a strong metric.

## Mapping the KPI catalog

| Leading (act on directly) | Lagging (learn from) | Hybrid |
|---|---|---|
| MFA coverage (#1) | MTTD (#10) | Secrets in code (#8) |
| Offboarding SLA (#2) | MTTR (#12) | Detection source mix (#11) |
| Standing privilege (#3) | Incident counts by severity | Phishing reporting rate (#14) |
| Patch latency (#5), vuln debt (#6) | Audit findings | Access-review yield (#4) |
| Scan coverage (#7) | Breach/regulatory events | Action-item completion (#13) |
| Review coverage (#9), training (#15) | | Risk-treatment velocity (#16) |

## The causal-chain method for choosing leading indicators

Don't pick leading indicators from a list — derive them from your own incidents and top risks. For each top risk (or last real incident), draw the causal chain and instrument the earliest measurable link you can influence:

```
Risk: credential-compromise breach
Chain: static long-lived key exists → key leaks (laptop, repo, CI log)
       → attacker uses key → data accessed → detected → contained

Leading candidates, from earliest link:
  • count of long-lived keys (earliest, strongest)     ← instrument this
  • secret-scanning coverage of repos + CI logs
  • time-to-rotate on detection
Lagging: the breach itself, MTTD/MTTR when it happens
```

The earliest link is almost always the best metric: cheapest to measure, most directly actionable, and it prevents the whole chain. This is also why "number of attacks blocked" is a useless metric — it instruments the *attacker's* activity (which you don't control) instead of your own exposure (which you do).

## Why leading indicators are the ones that get gamed

A leading indicator is a proxy, and proxies obey Goodhart's law: optimized hard enough, the proxy detaches from the outcome. Patch latency hits target via severity downgrades; MFA coverage hits 100% via denominator shrinkage. Lagging indicators resist gaming (reality is hard to fake) but arrive too late. This asymmetry drives the core design rule:

> **Manage by leading indicators; audit them with lagging ones.**

If patch latency has been green for a year but an incident review finds the exploited vuln sat unpatched for 90 days — the *pair* of signals just told you the leading metric's definition is broken. Every leading metric in your set should have a named lagging metric that would eventually expose its corruption. If you can't name one, the metric is unfalsifiable and doesn't belong in the set.

## Balance rules for a real dashboard

1. **Ratio:** roughly 2/3 leading, 1/3 lagging. All-lagging = driving by the rear-view mirror; all-leading = a hypothesis about security with no ground truth.
2. **Small-n honesty for lagging metrics:** with 3 incidents a year, report the incidents themselves (per-incident MTTD/MTTR, one-line narratives), not means and trends. Averaging three numbers is numerology; boards respect "n is small, here are all three" far more than a fake trend line.
3. **Near misses are the lagging-signal multiplier.** Real incidents are rare; near misses (the leaked key that wasn't used, the phishing report 40 minutes before the campaign hit everyone) are 10× more plentiful and carry the same causal information. A near-miss register is the cheapest way to get statistical power for your ground truth.
4. **Review the *set* twice a year:** retire leading metrics that have sat at target for 3+ quarters (they've become attestations — move them to an annual check and free the dashboard slot for the current risk frontier). A dashboard whose composition never changes is measuring last year's threat model.

## The maturity arc

Programs evolve through indicator stages, and skipping stages fails:

1. **Count what exists** (lagging, raw): incidents, findings. Honest but reactive.
2. **Instrument the causes** (leading): coverage, latency, privilege. The program can now be *managed*.
3. **Close the loop** (paired): each leading metric audited by a lagging one; metric definitions versioned; gaming pathways documented (the [KPI catalog](kpi-catalog.md) format).
4. **Risk-integrated:** metrics feed the risk register's likelihood scores, and metric movements reprioritize the roadmap automatically. Few programs truly reach this; the ones that do stop arguing about budget by anecdote.

Aim publicly for stage 3. Stage 4 is a direction, not a destination.
