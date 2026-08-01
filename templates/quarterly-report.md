# Quarterly Security Report — Template

The internal quarterly security report: written for the exec team, source document for the board slide (see [board-reporting.md](../docs/board-reporting.md)). Target length 3–5 pages. Fill every section or delete it — an empty "Nothing this quarter" is better than a padded one, and a padded one is worse than no report.

---

# Security Quarterly Report — {{Qn YYYY}}

**Prepared by:** {{SECURITY_OWNER}} · **Date:** {{DATE}} · **Distribution:** {{EXEC_TEAM / AUDIT_COMMITTEE}}
**Data sources & queries:** {{LINK — every number below must be reproducible from here}}

## 1. Executive summary (5 bullets max)

- Overall risk direction this quarter: {{improved / stable / degraded}} — because {{one clause}}.
- The one thing that most reduced risk: {{…}}
- The one thing that most concerns me going into next quarter: {{…}}
- Decisions needed from this group: {{… / none}}
- Commitments from last quarter: {{kept N of M — details in §6}}

*Write this section last, keep it honest first. If the summary and the details ever diverge, readers will stop trusting both.*

## 2. Top risks (from the risk register — top 5 by residual score)

| Risk | Residual (prev → now) | Movement driver | Treatment status | Owner |
|---|---|---|---|---|
| {{R-01 …}} | 10 → 8 | {{control shipped / new information / re-scored}} | {{on track / late / blocked}} | |

Narrative (2–3 sentences per moved risk): what changed in the world or in our controls. Risks that haven't moved in 3+ quarters get a one-line challenge: is the treatment stalled, or is the score wrong?

## 3. KPI dashboard (the fixed set — same metrics every quarter)

| Metric | Target | {{Q-3}} | {{Q-2}} | {{Q-1}} | {{This Q}} | Notes |
|---|---|---|---|---|---|---|
| MFA coverage (denominator: {{def}}) | 100% | | | | | |
| Offboarding SLA compliance | 100% | | | | | |
| Critical patch latency p50/p90 (days) | ≤7 | | | | | |
| Scan coverage by class | ≥95% | | | | | |
| New secrets in code / time-to-rotate | ↓ / ≤4h | | | | | |
| Externally-detected incident fraction | → 0 | | | | | |
| Incident action-item completion | ≥90% | | | | | |
| Risks past treatment due date | 0 | | | | | |

**Definition changes this quarter:** {{none / list — a metric whose definition changed gets a visible break in its trend line, never a silent rebase}}.

## 4. Incidents and near misses

**Summary:** {{N}} incidents ({{n1}} Sev-1, {{n2}} Sev-2, {{n3}} Sev-3/4), {{M}} recorded near misses.

Per Sev-1/2 incident (one block each):
- **{{INC-ID short name}}** — What happened (2 sentences, no euphemisms). Customer/data impact: {{…}}. Detected by: {{internal monitoring / employee / customer / external}} in {{time}}. Contained in {{time}}. What structurally changed as a result: {{…}}. Review link: {{…}}.

Near-miss highlight (pick one instructive case): {{what almost happened and which control caught it — this is where detection investment shows its value}}.

## 5. Program delivery

What shipped this quarter against the roadmap (security-led and engineering-led both — credit the platform teams explicitly; it's their controls):

| Initiative | Risk(s) addressed | Status | Note |
|---|---|---|---|

What slipped, and the honest reason (dependency, capacity, misestimate). Slips without reasons are how reports become fiction.

## 6. Commitments tracking

Every promise made in previous reports, with status. This section is the report's integrity mechanism — it is deliberately impossible to quietly drop a commitment.

| Committed | In report | Due | Status |
|---|---|---|---|

## 7. Compliance & assurance calendar

- Audit/certification status: {{SOC 2 window / ISO surveillance / pentest}} — next milestone {{date}}.
- Findings/exceptions open: {{count, oldest, owner}}.
- Vendor risk: {{Tier-1 reviews done/due, conditions overdue}}.
- Exceptions & risk acceptances expiring next quarter: {{list — these need decisions before they lapse into silent renewal}}.

## 8. Asks

Specific, priced, ranked: {{budget / headcount / decision / risk acceptance}}. For each: what risk it changes and what happens if deferred. If there are no asks, say so — manufactured asks train readers to discount real ones.

## 9. Next quarter preview

Top 3 planned outcomes (outcomes, not activities: "eliminate remaining static cloud keys," not "continue IAM work"). These become §6 rows next quarter — write them expecting to be graded on them.

---

*Appendix (links, not inlined): full incident list, KPI query definitions, risk register export, audit evidence index.*
