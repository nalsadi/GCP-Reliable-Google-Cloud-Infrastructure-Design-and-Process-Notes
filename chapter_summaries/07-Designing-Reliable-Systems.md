# 07 Designing Reliable Systems

## Overview
Chapter 07, Designing Reliable Systems, consolidates reliability as a discipline across availability, durability, and scalability. It emphasizes fault-tolerant, decoupled architectures that operate across failure domains (zones/regions), plus observable systems and tested disaster recovery. Core patterns include health checks, readiness/liveliness probes, circuit breakers, intelligent retries with backoff and jitter, lazy deletion, and proactive data/HA strategies for databases and storage. The goal is to design for normal, degraded, and full failure modes while planning, testing, and documenting disaster recovery.

## Key Concepts
- Availability, Durability, Scalability: the reliability triad guiding design and metrics.
- Fault tolerance: remove single points of failure; use N+2 capacity; interchangeable, stateless deployment units.
- Failure domains: distribute components across zones/regions to prevent correlated failures; use microservices with loose coupling.
- Cascading failures: mitigate via health checks, fast-starting instances, stateless designs, load balancers.
- Overload protection: circuit breakers; intelligent retries with backoff and jitter.
- Resilient data storage: lazy deletion; multi-region replication; backups/restores.
- Observability: monitor latency, resource usage, error rates; actionable metrics and alerts; plan DR testing.
- Operational states: design for normal, degraded, and failure conditions; prepare and test disaster recovery.
- High availability patterns: regional/multi-zone deployments, auto-healing, regional databases, load balancing.
- Kubernetes/GKE considerations: readiness/liveness probes, regional clusters, Istio for circuit breakers.
- Disaster recovery planning: define RPO/RTO by service; practice recovery with documented runbooks.

## Practical Guidance
- Architect for Availability, Durability, Scalability: eliminate single points of failure; decouple services; keep components stateless and interchangeable; plan for N+2 capacity across zones/regions.
- Health and Readiness: implement health checks that verify service readiness and dependency health; rely on auto-healing to replace unhealthy instances.
- Overload and Retries: use intelligent retries with backoff (truncate exponential backoff; include jitter); cap retries and max backoff; avoid unbounded retry storms; consider Istio on GKE for automated circuit breakers.
- Circuit Breakers: protect degraded services from cascading failures; route traffic away when unhealthy; design for degraded operation rather than incessant retries.
- Lazy Deletion: implement multi-stage deletion (visible → soft-delete → hard-delete) with defined windows; allow recovery during soft-delete; ensure backups exist.
- Data and HA across Regions: replicate data across zones/regions; use multi-region storage backups; prefer managed HA data services (Firestore, Spanner) where possible; Cloud SQL with a failover replica in another zone.
- Kubernetes Resilience: use regional clusters or multi-zone node pools; distribute workloads across zones; enable auto-healing; leverage Istio for circuit breaking.
- Disaster Recovery Planning: define DR objectives (RPO/RTO) per service; create diagrams and runbooks; implement backups and failover strategies; test regularly (drills).
- DR Tactics by Service: tailor DR approach per service priority (e.g., orders with tight RPO/RTO; analytics may tolerate re-import/rebuild).
- Backup and Restore Procedures: establish automated backups, cross-region storage, and restoration scripts; document and validate recovery steps.
- Cost vs Availability: HA incurs cost; perform risk/cost analysis including downtime costs; balance requirements with budget.

- Diagram and Planning Artifacts: create deployment diagrams showing multi-region/zone layouts, backup locations, failover paths, and DR runbooks.

## Services/Tools Mentioned
- Circuit breaker; truncated exponential backoff; retries with jitter
- Lazy deletion
- Health checks; readiness and liveliness probes
- Kubernetes; GKE; Istio
- Compute Engine; Cloud Load Balancing
- Zones and Regions
- Autohealing; multi-region/regional deployments
- Microservices; failure domains
- Disaster recovery planning; DR scenarios; RPO/RTO
- Cloud Storage (multi-region/dual-region)
- Cloud SQL (failover replica, cross-zone)
- Firestore; Spanner (HA/multi-region)
- Regional managed instance groups
- Global load balancer
- BigQuery
- Snapshots; machine images; persistent disks
- Cloud Functions; Cloud Scheduler
- Regions/Zones examples (e.g., us-central1, us-east1, europe-west2)

## Quick Revision Notes
- Design around the reliability triad: availability, durability, scalability.
- Eliminate single points of failure; deploy across multiple zones/regions; keep services stateless and interchangeable.
- Use health checks and readiness/liveliness probes to enable auto-healing and safe traffic routing.
- Implement intelligent retries with backoff and jitter; apply circuit breakers to prevent cascading overloads.
- Plan for degraded states; do not flood a recovering service with retries.
- Apply lazy deletion for recoverable user data; allow restoration during soft-delete windows.
- Invest in HA data services and cross-region backups; evaluate Cloud SQL failover replicas; prefer Firestore/Spanner for higher HA.
- Use Kubernetes regional configurations and Istio to simplify circuit breakers and resilience.
- Define DR objectives (RPO/RTO) per service; build and test DR runbooks; conduct regular drills.
- Map deployments with diagrams for HA, DR, and backup recovery; document procedures and recovery scripts.
