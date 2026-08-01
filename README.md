# Security Metrics That Survive Contact with Reality

A metrics kit for security leaders: a KPI catalog with formulas, targets, and — the part usually missing — an honest note on how each metric gets gamed; guidance on board reporting; a quarterly report template; and a primer on leading vs lagging indicators.

The stance throughout: a security metric exists to drive a decision or verify a control. A metric that can't change anyone's behavior is decoration, and a metric whose gaming pathway you haven't named will eventually measure the gaming, not the security.

Reference material distilled from practice building security reporting in cloud-native engineering organizations.

**Author:** Danylo Kochetov — Senior DevOps/SRE, security architecture track.

## Structure

```
security-metrics/
├── README.md
├── LICENSE
├── docs/
│   ├── kpi-catalog.md         # 16 metrics: formula, target, gaming-risk note
│   ├── board-reporting.md     # What belongs on a board slide (and what doesn't)
│   └── leading-vs-lagging.md  # Building a balanced indicator set
└── templates/
    └── quarterly-report.md    # Quarterly security report skeleton
```

## Usage

1. Start with [docs/kpi-catalog.md](docs/kpi-catalog.md) and pick **6–8 metrics, not 16**. Selection criteria are in the catalog header. Every metric you adopt needs a named data source you can query, an owner, and a target with a date.
2. Read the gaming-risk note for each metric you adopt and decide the countermeasure *before* publishing the metric — incentives move the moment a number appears on a dashboard.
3. Build the quarterly report from [templates/quarterly-report.md](templates/quarterly-report.md); derive board content from it using [docs/board-reporting.md](docs/board-reporting.md), never the reverse.
4. Re-balance the set twice a year with [docs/leading-vs-lagging.md](docs/leading-vs-lagging.md) — retired metrics are a sign of health, not failure.

## Three rules this repo keeps repeating

- **Trend beats snapshot.** Almost every number here is meaningless as a point value and useful as a 4-quarter trend.
- **Denominators are where metrics lie.** "95% MFA coverage" means nothing until you know whether the denominator includes contractors, service accounts, and the legacy tenant.
- **Pair every speed metric with a quality metric** (patch latency with recurrence, MTTR with reopen rate) — otherwise you are purchasing speed with silent corner-cutting.

## License

MIT — see [LICENSE](LICENSE).
