# 09 Maintenance and Monitoring

## Overview
A concise playbook for keeping cloud apps healthy, up-to-date, and cost-effective. Focuses on zero-downtime updates, robust monitoring, capacity planning as an ongoing practice, and cost optimization through sizing, caching, and locality. Emphasizes measurable reliability (SLOs/SLIs) and actionable governance (alerts, budgets, automation).

## Key Concepts
- Versioning and updates: maintain backward compatibility; include version in API URIs for breaking changes.
- Deployment strategies: rolling updates, blue/green deployments, canary releases; platform-specific implementations (Compute Engine, Kubernetes, App Engine).
- Observability: Cloud Monitoring, Logs, Traces, Profiler; Uptime Checks; dashboards; alerts; SLIs/SLOs.
- Cost visibility: pricing calculator, billing reports, exporting billing data to BigQuery, Looker Studio dashboards; budgets and alerts.
- Capacity planning: continuous forecast → monitor → allocate → deploy → reassess (iterative cycle).
- Resource optimization: right-size VMs, auto scaling, discounts (committed use, Spot VMs); storage performance matching I/O; memory/caching to reduce compute/storage needs.
- Network considerations: egress charges, locality (keep compute near data), zone/region nuances; DNS/Traffic routing nuances for traffic shifts.
- Storage and data choices: evaluate Firestore, Bigtable, Cloud Storage, Memorystore, and disk types (Standard vs SSD) for cost and capability tradeoffs.
- Decoupling and resilience: use caching, CDN, Pub/Sub to minimize persistent storage and improve resilience.

## Practical Guidance
- Versioning and updates
  - Include version in URIs; bump versions for breaking changes.
  - Test thoroughly; aim for zero-downtime deployments.
  - Be prepared for risks with non-backward-compatible updates.
- Deployment strategies
  - Rolling updates by default when API compatibility exists.
  - Use blue/green or canary for larger or risky changes; route traffic carefully; have rollback pathways.
  - Implement platform-specific traffic migration (DNS, traffic splitting, labels).
- Cost planning and optimization
  - Treat capacity planning as an ongoing cycle: forecast, monitor, allocate, deploy, and re-forecast.
  - Start small: use auto scaling; consider committed use discounts.
  - Use Spot VMs for fault-tolerant workloads; pair with managed instance groups to recover from preemption.
  - Rightsize VMs and match disk performance to I/O needs; avoid over-provisioning.
  - Optimize network: minimize cross-region egress; keep data locality; leverage Memorystore, CDN, and caching where appropriate.
  - Compare storage options before committing (cost and capability differences matter).
- Monitoring and SRE
  - Define and monitor SLOs/SKIs; set uptime checks and alerts for violations.
  - Use default and custom dashboards; deploy traces, profiler, and logs to trace latency and reliability issues.
  - Automate cost responses where feasible (budgets, alerts, small automation via Pub/Sub or Cloud Run).
- Data management and cost analysis
  - Export billing data to BigQuery for deep analysis; build Looker Studio dashboards for visibility.
  - Use pricing calculator for estimates and to compare compute/storage options.
  - Visualize daily/monthly/project-level spend; monitor regional distribution and networking spend.
- Deployment hygiene
  - Ensure changes do not break existing clients; validate backward compatibility.
  - Prepare rollback plans for any deployment strategy.

## Services/Tools Mentioned
- Google Cloud pricing calculator; Cloud Billing Reports; billing data exports
- Cloud Monitoring; Dashboards; Uptime Checks; Alerts
- App Engine; Kubernetes; Compute Engine
- Instance groups; Docker images; Pods; Labels; Load balancers
- Blue/Green deployments; Traffic Splitting; DNS
- Canary releases
- Spot VMs; Committed use discounts; Rightsizing recommendations
- Standard Persistent Disk vs SSD Persistent Disk
- Memorystore for Redis
- Cloud CDN
- Firestore; Bigtable; Cloud Storage; Cloud SQL
- BigQuery; Looker Studio
- Pub/Sub; Cloud Run
- SRE concepts; SLOs; SLIs; latency as a key signal
- Profiler; Traces; Logs

## Quick Revision Notes
- Aim for zero-downtime updates; prefer rolling updates, blue/green, or canary as appropriate; ensure backward compatibility.
- Treat capacity planning as a continuous loop; continuously compare forecasts with actuals.
- Start small, scale with auto scaling, and leverage discounts (Spot VMs, committed use).
- Minimize egress costs via locality; match storage type to I/O needs; avoid over-provisioning.
- Use caching/CDN (Memorystore, Cloud CDN) to reduce compute/storage requirements.
- Decouple services with Pub/Sub to lower persistent storage needs.
- Export billing data to BigQuery; build Looker Studio dashboards for spend visibility.
- Define and monitor SLOs/SLIs; set uptime checks and alerts to detect and respond to issues early.
- Use standard deployment hygiene: test thoroughly, validate versions, and have rollback plans.
