# Alert Catalog / Catálogo de Alertas

| Alert | Severity | Trigger | First response | Status |
| --- | --- | --- | --- | --- |
| Host unavailable | High | Health check fails | Check connectivity and hypervisor state | Template |
| Disk capacity | Medium | Free space below threshold (`TBD`) | Confirm growth and cleanup/expansion options | Template |
| Backup failure | High | Latest expected job fails | Review job log; protect recovery point | Template |
| Service unavailable | High | Service check fails | Confirm scope, dependency, and recent changes | Template |

Tune thresholds after collecting baseline data. Avoid routing credentials or sensitive topology through alerts.

