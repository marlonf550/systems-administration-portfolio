# Restore Test Runbook / Runbook de Teste de Restauração

| Step | Action | Expected result | Record |
| --- | --- | --- | --- |
| 1 | Choose approved test workload | Non-critical workload selected | Redacted workload ID |
| 2 | Check recovery point | Meets declared RPO | Timestamp |
| 3 | Restore in isolated location | Restore completes successfully | Duration and job result |
| 4 | Validate service/data | Service starts and checks pass | Test checklist |
| 5 | Close review | Deviations have owners and dates | Report reference |

**Safety / Segurança:** never restore into production or overwrite a live workload without explicit approval and a validated change plan.

