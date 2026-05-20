# Application Security Dashboard

A Mermaid-style visual summary of the current application security program.

## Dashboard Overview

```mermaid
flowchart TB
    A[Applications Onboarded<br/><b>42</b>] --> B[Active Repositories<br/><b>58</b>]
    A --> C[Critical Findings Open<br/><b>3</b>]
    B --> D[High Findings Open<br/><b>19</b>]
    B --> E[Medium Findings Open<br/><b>74</b>]
    C --> F[Mean Time to Remediate High Findings<br/><b>8 days</b>]
    D --> G[PR Scan Coverage<br/><b>93%</b>]
    E --> H[Re-test Completion Rate<br/><b>96%</b>]

    style A fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#111827
    style B fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#111827
    style C fill:#fee2e2,stroke:#dc2626,stroke-width:2px,color:#111827
    style D fill:#fef3c7,stroke:#d97706,stroke-width:2px,color:#111827
    style E fill:#f3f4f6,stroke:#6b7280,stroke-width:2px,color:#111827
    style F fill:#e0f2fe,stroke:#0284c7,stroke-width:2px,color:#111827
    style G fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#111827
    style H fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#111827
```

## Metrics Table

| Metric | Value | Status |
|---|---:|---|
| Applications onboarded | 42 | Healthy |
| Active repositories | 58 | Healthy |
| Critical findings open | 3 | Needs attention |
| High findings open | 19 | Needs attention |
| Medium findings open | 74 | Monitor |
| Mean time to remediate high findings | 8 days | Good |
| PR scan coverage | 93% | Strong |
| Re-test completion rate | 96% | Strong |

## Severity View

```mermaid
xychart-beta
  title "Open Findings by Severity"
  x-axis ["Critical", "High", "Medium"]
  y-axis "Count" 0 --> 80
  bar [3, 19, 74]
```

## Delivery Health

```mermaid
pie title Security Delivery Health
  "PR scan coverage" : 93
  "Re-test completion rate" : 96
```

## Interpretation

```mermaid
flowchart LR
    S[Security Program] --> O[Onboarding Healthy]
    S --> R[Repository Coverage Strong]
    S --> C[Critical Findings Low]
    S --> H[High Findings Need Action]
    S --> M[Medium Findings Need Planning]
    S --> V[Validation Strong]

    style S fill:#1d4ed8,stroke:#1e3a8a,stroke-width:2px,color:#ffffff
    style O fill:#dcfce7,stroke:#16a34a,stroke-width:1.5px,color:#111827
    style R fill:#dcfce7,stroke:#16a34a,stroke-width:1.5px,color:#111827
    style C fill:#fee2e2,stroke:#dc2626,stroke-width:1.5px,color:#111827
    style H fill:#fef3c7,stroke:#d97706,stroke-width:1.5px,color:#111827
    style M fill:#f3f4f6,stroke:#6b7280,stroke-width:1.5px,color:#111827
    style V fill:#dcfce7,stroke:#16a34a,stroke-width:1.5px,color:#111827
```

## Key Observations

- **Onboarding is healthy** with 42 applications and 58 active repositories.
- **Critical exposure is low** at 3 open items, but it should remain a priority.
- **High findings need focused remediation** because 19 items are still open.
- **Medium findings form the largest backlog** and should be planned into the normal delivery cycle.
- **Validation is strong** with 96% re-test completion.
- **Preventive scanning is mature** at 93% PR scan coverage.

## Status Snapshot

| Area | Result |
|---|---|
| Onboarding | Healthy |
| Exposure | Attention required |
| Scanning | Strong |
| Verification | Strong |

## Notes

This README is GitHub-friendly and uses Mermaid blocks to give a dashboard-like view directly in the repository.

