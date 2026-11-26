# INC-123 — Checkout errors after deployment

**Status** Resolved · **Date** 2026-11-26 · **Times** UTC

## Summary

Checkout returned HTTP 500 for up to 18% of requests over 13 minutes. The new release lowered the database connection pool limit from 40 to 5. Checkout requests timed out waiting for connections during peak traffic. Rolling back restored the previous limit and returned errors to baseline.

## Timeline

| Time | Event | Evidence |
| --- | --- | --- |
| 06:02 | The new checkout release rolled out. | E3 |
| 06:04 | Checkout errors began to rise. | E1 |
| 06:06 | The on-call engineer received an alert. | E1 |
| 06:09 | Application logs showed database connection acquisition timeouts. | E2 |
| 06:11 | The engineer confirmed the lower pool limit in the deployment diff. | E3 |
| 06:14 | The engineer completed the rollback. | E4 |
| 06:17 | Checkout errors returned to baseline. | E1 |

## Evidence in capture order

| ID | Captured at | Artifact | Source | Tag | Note |
| --- | --- | --- | --- | --- | --- |
| E2 | 06:10 | `checkout-errors.log` | Piped checkout logs | `symptom` | Includes the first connection timeout seen in the logs. |
| E3 | 06:12 | `checkout-deploy.diff` | Local file | `cause` | Compare the pool limit in the two releases. |
| E4 | 06:15 | `checkout-rollback.cast` | Terminal recording | `mitigation` | Includes rollout status for all checkout replicas. |
| E1 | 06:18 | `checkout-errors.png` | Grafana screenshot via clipboard | `impact` | Shows the full error spike and recovery. |

## Follow-up

- Add a release check for unexpected changes to the checkout pool limit.
- Alert on connection acquisition timeouts before they drive up checkout errors.
