# Board Reporting on Security

Boards don't want to be impressed by security; they want to know whether the company's risk is understood, priced, and managed by someone competent. A board security slide has one job: enable the board to discharge its oversight duty in about ten minutes. Everything else is noise that erodes your credibility.

## What the board is actually deciding

When security appears on the agenda, the board is implicitly answering four questions:

1. **Do we understand our top security risks, and are they moving in the right direction?**
2. **Is investment proportionate** — are we funding the right things, and what risk are we explicitly accepting by not funding the rest?
3. **Are we ready for the bad day** — incident, disclosure, regulator?
4. **Is management being straight with us?** (The meta-question; it's answered by tone and consistency across quarters, not by any single number.)

Structure every board appearance to answer these four. Nothing else has to be there.

## The slide that works (one slide, four blocks)

**Block 1 — Top risks (3–5, in business language).** Each: one line, direction arrow vs last quarter, what's being done, what it costs. "Ransomware disrupting order processing — residual risk down (backup immutability shipped); remaining exposure: recovery time ~8h vs 4h target; closing Q3." Business consequence first, mechanism second.

**Block 2 — Posture trend.** 3–4 KPIs from the [catalog](kpi-catalog.md) shown as 4-quarter trends with targets. Pick ones a director can interrogate: MFA coverage, critical-patch latency, externally-detected incident fraction, action-item completion. Same metrics every quarter — rotating metrics reads as curation, and directors notice.

**Block 3 — Incidents & near misses.** Count by severity, one sentence on any Sev-1/2 (what happened, customer impact, what changed as a result). Include a near miss when instructive: it signals detection works and builds the candor account you will need to draw on during a real breach.

**Block 4 — Asks and acceptances.** What you need decided (budget, policy, risk acceptance) or explicitly nothing: "no asks this quarter." Every quarter must name the risks being consciously accepted — this is the board's actual legal function, and putting acceptances in writing quarterly is what protects both of you later.

## What a board slide should NOT contain

- **Raw operational counts** — "14M attacks blocked," alerts triaged, vulnerabilities scanned. These numbers are unfalsifiable, uninterpretable, and read as padding. The firewall counting packets is not risk information.
- **Vendor-tool dashboards or screenshots.** If the slide could have been produced by the tool's marketing team, it doesn't belong.
- **Security-rating letter grades as the headline.** Fine as one input; as a headline they outsource your judgment to a scanner.
- **Fear framing** ("threat landscape worse than ever") to justify budget. It works once, then permanently reprices your credibility.
- **Perfect dashboards.** All-green across quarters doesn't read as excellence; it reads as either trivial metrics or filtered reporting. A slide with an honest red item and a plan outperforms a green wall in every board dynamic that matters.
- **Unexplained metric changes** — a metric that improves because you changed its definition, presented as improvement. Disclose definition changes in a footnote; being caught silently rebasing once costs more than a year of red metrics.
- **Acronym soup.** CSPM, SCA, EDR — translate or delete. A director who has to decode your slide concludes you can't operate at their altitude.

## Handling the predictable questions

Prepare (in the appendix, not the slide) for the questions boards actually ask:

- *"Are we vulnerable to [the breach in this week's news]?"* — have a same-day mechanism to answer this before the meeting; it's the most common ambush and a gift when you're ready ("we checked on Tuesday; not exposed because X; here's the one adjacent thing we tightened anyway").
- *"How do we compare to peers?"* — have a calibrated answer (framework maturity level, audit posture, insurance underwriting feedback) rather than "it's hard to compare."
- *"What keeps you up at night?"* — answer with a real risk from Block 1, never "nothing." The director is testing candor, not looking for comfort.
- *"What would you do with 30% more budget?"* — a ranked list with risk deltas, instantly available. Not having this answer is declining money.

## Cadence and channel

- **Quarterly**: the one-slide update inside the broader business review (or audit/risk committee where one exists — deeper, more technical latitude there).
- **Annually**: a 30-minute deep dive — program strategy, posture vs framework, multi-year investment arc, tabletop-exercise findings.
- **Immediately**: material incidents, on the pre-agreed threshold. Negotiate that threshold with the board *before* an incident (e.g. confirmed Restricted-data breach, regulator contact, ransom demand). The mid-incident question "should the board know?" means the answer was needed yesterday.

## The relationship between the quarterly report and the board slide

Write the full internal report first ([templates/quarterly-report.md](../templates/quarterly-report.md)), then extract the board view. Never build the board narrative and back-fill the data — the seams show, and the exec team who saw the internal report will notice any divergence between the two stories. One truth, two zoom levels.
