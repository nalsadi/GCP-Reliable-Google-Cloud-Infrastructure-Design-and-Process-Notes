# 06 Deploying Applications to Google Cloud

## Overview
This chapter guides deploying applications on Google Cloud by contrasting App Engine, GKE, Cloud Run, Cloud Run functions, and Compute Engine. It presents a decision framework based on OS/container requirements and event-driven needs, and translates design principles into practical patterns for traffic management, scalability, and multi-region deployments. The goal is to help you select the right platform for a given workload and to apply portable, best-practice deployment patterns across platforms.

## Key Concepts
- Deployment targets: App Engine (fully managed, serverless), Google Kubernetes Engine (GKE; customizable Kubernetes), Cloud Run (managed, stateless containers), Cloud Run functions (event-driven serverless microservices), Compute Engine (IaaS VMs).
- Platform characteristics:
  - App Engine: code-focused, automatic networking/load balancing/autoscaling; one App Engine app per project with services/versions/instances; supports traffic splitting.
  - GKE: flexible, multi-service deployments within clusters; choice between Autopilot (managed workload experience) and Standard (more control).
  - Cloud Run: managed, ephemeral containers; immutable revisions; deploy from Artifact Registry or source; simple scaling, including scale-to-zero.
  - Cloud Run functions: event-driven, pay-per-use, triggers from storage, Pub/Sub, or HTTP.
  - Compute Engine: full OS control, non-containerized apps, self-hosted services/databases, autoscaling, health checks, multi-zone HA.
- Networking and delivery: use managed backends (instance groups) with global load balancer; Cloud CDN for static content; SSL for external services; avoid exposing public IPs for internal services.
- Portability and design: 12-factor principles support portability across platforms; deploying same app across platforms aids platform selection.

## Practical Guidance
- Platform decision framework
  - Specific OS requirements: choose Compute Engine.
  - No OS constraints and using containers: choose between GKE (for Kubernetes control) and Cloud Run (for managed simplicity); pick GKE for customization and multi-service orchestration, Cloud Run for reduced ops overhead.
  - Non-container workloads: consider Cloud Run Functions for event-driven tasks; otherwise App Engine for serverless code-based apps.
- Compute Engine patterns
  - Start small: identify the smallest machine type that suffices; use autoscaling and health checks.
  - High availability: distribute instances across multiple zones; use instance groups with auto-healing.
  - Load balancing: front-end with a global load balancer; backends from instance groups; enable Cloud CDN for static content; apply SSL; avoid exposing public IPs for internal services.
- GKE considerations
  - Choose Autopilot for a workload-centric, managed experience; choose Standard mode for finer control over clusters, nodes, and hardware.
  - Deploy multiple services within a single cluster when appropriate; balance flexibility, portability, and cost.
- Cloud Run and Cloud Run functions
  - Cloud Run: container-based deployments; revisions are immutable; deploying from a tag resolves to a digest for stability; deploy via Cloud Console or gcloud.
  - Cloud Run functions: design event-driven, loosely coupled workflows; leverage triggers from storage, Pub/Sub, or HTTP to compose services; scale to zero to minimize costs.
- App Engine guidance
  - Leverage traffic splitting to implement canary or A/B testing and smooth version rollouts.
- Portability pattern
  - Apply 12-factor principles to maximize portability across cloud providers and deployment services.
  - Consider deploying the same app across multiple platforms to inform platform choice for future services.

## Services/Tools Mentioned
- Compute Engine
- Google Kubernetes Engine (GKE)
- Cloud Run
- App Engine
- Cloud Run functions
- Artifact Registry
- Container Registry
- Autopilot mode (GKE)
- Standard mode (GKE)
- Global load balancer
- Cloud CDN
- SSL
- Cloud Storage
- Cloud SQL
- Firestore
- Memcache
- Pub/Sub
- Vision API
- Cloud Translation API
- Docker
- Kubernetes
- 12-factor principles
- Cloud Build
- Docker/Kubernetes-backed CI/CD
- gcloud command line
- Google Cloud Console

## Quick Revision Notes
- Choose Compute Engine for specific OS or non-container workloads; use autoscaling, health checks, and multi-zone HA.
- Use instance groups as backends; a global load balancer with Cloud CDN and SSL supports multi-region and performance needs; avoid public IPs for internal services.
- GKE Autopilot favors managed workloads; Standard offers deeper control.
- Cloud Run offers managed, immutable revisions; deploy from Artifact Registry or source; supports scalable, pay-as-you-go operation.
- Cloud Run functions enable event-driven, serverless microservices with triggers from storage, Pub/Sub, or HTTP; scale to zero when idle.
- App Engine supports traffic splitting for canary/A/B testing and smooth version transitions.
- Applying 12-factor principles improves portability and informs deployment decisions across platforms.
- Deploying the same application across multiple platforms can illuminate platform tradeoffs and guide future choices.
