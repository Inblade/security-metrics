# Security KPI Catalog

16 metrics with formula, realistic target, cadence, and a **gaming-risk note** — the way each metric degrades into theater once people are measured on it. Adopt 6–8. Selection test for each candidate: *Who changes what decision when this number moves?* No answer, no adoption.

Targets below assume a cloud-native company of 50–500 people; calibrate to your baseline — the right first target is usually "meaningfully better than our current number," not an industry benchmark.

---

## Identity & access

### 1. MFA coverage
- **Formula:** identities with enforced MFA ÷ all active human identities in the IdP and any non-federated system. Report phishing-resistant coverage (FIDO2) as a separate line for admins.
- **Target:** 100% enforced (not "enrolled"); admins 100% phishing-resistant.
- **Cadence:** monthly until 100%, then quarterly attestation.
- **Gaming risk:** the denominator. Contractors, service accounts misclassified as human, the legacy tenant, and non-SSO SaaS quietly drop out, producing a proud 100% over a third of reality. Countermeasure: publish the denominator definition with the metric and reconcile it against the HR roster, not the IdP's own list.

### 2. Offboarding SLA compliance
- **Formula:** departures with all access revoked within SLA (e.g. 4 business hours) ÷ all departures. Measured by reconciling HR termination dates against IdP/system logs — not by checklist self-report.
- **Target:** 100%; any miss gets a mini-review.
- **Gaming risk:** measuring checklist completion instead of actual access state; the checklist says "done" while a non-SSO tool session lives on. Countermeasure: the metric's source must be the log reconciliation, never the ticket status.

### 3. Standing privileged access
- **Formula:** count of identities with permanent admin/production-data access (target direction: down, replaced by JIT elevation).
- **Target:** trend to a small named set; zero permanent cloud-org-admin humans.
- **Gaming risk:** access relabeled ("power user" roles with admin-equivalent permissions) or moved to shared service accounts. Countermeasure: define the metric by *effective permissions* (policy analysis), not role names.

### 4. Access review completion & yield
- **Formula:** reviews completed on schedule ÷ scheduled; plus **yield** = grants reduced or revoked ÷ grants reviewed.
- **Target:** 100% completion; yield reported without target.
- **Gaming risk:** rubber-stamping — 100% completion, 0% yield forever means nobody is looking. A persistent zero yield is itself the signal to investigate. Never target yield directly (that manufactures revocations); just make it visible.

## Vulnerability & patch

### 5. Patch/remediation latency by severity
- **Formula:** median (and p90) days from *fix available* to *fix deployed*, per severity band, for OS/base images, dependencies, and cloud findings separately.
- **Target:** critical ≤ 7 days (KEV-listed: ≤ 72h), high ≤ 30, medium ≤ 90. p90, not just median — the median hides the scary tail.
- **Gaming risk:** severity downgrading ("it's high, but not *our* kind of high") and clock-starting games (counting from triage, not from fix availability). Countermeasure: severity source is the scanner + KEV list, adjustable only via a recorded risk-acceptance; clock definition published with the metric.

### 6. Vulnerability debt (aging backlog)
- **Formula:** count of open findings past SLA, weighted by severity; trend line.
- **Target:** zero critical/high past SLA; total debt trending down or flat while scan coverage grows.
- **Gaming risk:** closing findings as "risk accepted" in bulk, or narrowing scan coverage so fewer findings exist. Countermeasure: pair with metric #7 and report risk-acceptance count alongside.

### 7. Scan coverage
- **Formula:** assets actually scanned ÷ assets in inventory, per class (repos with SCA, images scanned, cloud accounts with CSPM, endpoints with EDR).
- **Target:** ≥ 95% per class, inventory-derived denominator.
- **Gaming risk:** inventory shrinkage — coverage looks great because the inventory is stale. Countermeasure: denominator generated from the cloud/asset APIs, never hand-maintained.

## Secrets & code

### 8. Secrets in code
- **Formula:** two lines — (a) new verified secrets committed per month (target: 0–2, trending down), (b) median time-to-rotate once detected (target ≤ 4h; ≤ 1h if public).
- **Gaming risk:** suppressing detections as "false positive" to keep line (a) clean, and celebrating rotation speed while ignoring recurrence by the same team/pattern. Countermeasure: sample suppressed findings quarterly; report repeat-offender patterns to the owning team, not on the public dashboard (public blame drives suppression).

### 9. Security review coverage of sensitive changes
- **Formula:** PRs touching sensitive paths (auth, IAM, crypto, payment — as defined in CODEOWNERS) that received the required security review ÷ all such PRs.
- **Target:** 100% (it's technically enforced; the metric verifies the enforcement didn't drift).
- **Gaming risk:** path definitions rot — new sensitive code lands outside the CODEOWNERS globs and is invisibly exempt. Countermeasure: quarterly review of the path definitions is part of the metric's runbook.

## Detection & response

### 10. MTTD-security (mean/median time to detect)
- **Formula:** median hours from first attacker/violation activity (established in the post-incident timeline) to internal detection, over confirmed Sev-1/2 security incidents.
- **Target:** trend down; report alongside the *detection source mix* (metric #11). With few incidents, report per-incident values, not a mean of three numbers.
- **Gaming risk:** timeline archaeology bias — "first activity" gets set where it flatters. Countermeasure: the timeline is fixed in the blameless review before anyone computes metrics from it.

### 11. Detection source mix
- **Formula:** % of incidents detected by internal monitoring vs employee report vs customer vs third-party/external notification.
- **Target:** externally-notified fraction trending to zero — being told by a customer or researcher is the worst detection outcome.
- **Gaming risk:** low — which is why it's a good companion to MTTD. Mostly resists gaming because the categories are hard to argue.

### 12. MTTR-security (contain / eradicate, separately)
- **Formula:** median time from detection to containment, and detection to full eradication, per severity.
- **Target:** Sev-1/2 containment ≤ 4h; eradication reported without hard target (rushing eradication produces re-compromise).
- **Gaming risk:** premature "contained" declarations and severity inflation avoidance (incidents logged as Sev-3 to escape the clock). Countermeasure: containment declared by the IC per defined criteria; severity distribution itself is reviewed quarterly for drift.

### 13. Incident action-item completion
- **Formula:** post-incident action items closed by due date ÷ all due. The single best predictor of repeat incidents.
- **Target:** ≥ 90%; overdue items listed by name in the quarterly report (sunlight is the enforcement mechanism).
- **Gaming risk:** action items written vaguely enough to close trivially, or due dates set generously. Countermeasure: ICs review action-item quality in the post-incident review; extensions require the sponsor's sign-off, and extension count is visible.

## Human layer

### 14. Phishing simulation failure rate — handle with care
- **Formula:** report **reporting rate** (reported ÷ delivered) as the headline, failure rate (credentials entered ÷ delivered) as secondary.
- **Target:** reporting rate rising toward ≥ 60%; failure trend down. Never set a failure-rate target per team or person.
- **Gaming risk:** the highest in this catalog. Difficulty tuning (easy lures → great numbers), teams warning each other, and punitive use driving *real* phishing non-reporting — the metric can directly damage the incident-reporting culture it depends on. Countermeasure: fixed-difficulty lure bank year-over-year, no individual consequences ever, and celebrate reporters publicly instead of shaming clickers.

### 15. Security training completion & timeliness
- **Formula:** completed within 30 days of assignment ÷ assigned.
- **Target:** ≥ 95%, escalation to managers at day 21.
- **Gaming risk:** click-through completion measures attendance, not awareness. Accept that; this is a compliance-floor metric, and pretending it measures culture is the gaming. Pair with #14's reporting rate for the actual behavior signal.

## Program level

### 16. Risk-treatment velocity
- **Formula:** High+ risks in the register past their treatment due date (count + oldest age); exceptions/risk-acceptances past expiry.
- **Target:** zero past-due without a recorded sponsor decision.
- **Gaming risk:** due-date inflation at creation time and serial re-acceptance of expired exceptions. Countermeasure: re-acceptance requires a fresh signature each cycle and the *count of re-acceptances* is part of the reported number.

---

## Composition guidance

A balanced starter set of eight: **1, 2, 5, 7, 8, 11, 13, 16** — it covers prevention, detection, response, and governance; mixes leading and lagging (see [leading-vs-lagging.md](leading-vs-lagging.md)); and every metric has a queryable source. Add #14 only when the no-blame footing is genuinely in place.
