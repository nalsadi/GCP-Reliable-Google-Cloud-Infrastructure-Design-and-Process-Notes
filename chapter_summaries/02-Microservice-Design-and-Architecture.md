# 02 Microservice Design and Architecture

## Overview
This chapter blends core microservice design principles with practical patterns for scalable, cloud-native architectures. It covers service boundaries, state and data management, API design (REST and gRPC), contract versioning, and deployment considerations. The guidance emphasizes independent deployability, feature-oriented decomposition, and leveraging 12-factor practices to operate in dynamic cloud environments.

## Key Concepts
- Microservices vs monoliths: multiple codebases with independent data management versus a single codebase and datastore.
- Independent deployability and scalable architecture: deploy and scale services independently.
- Service boundaries and domain-driven design: define clear boundaries; organize by domain concepts (e.g., product, orders, accounts).
- Datastore independence: each microservice owns its datastore to avoid cross-service coupling.
- Stateful vs stateless services: prefer stateless services; stateful components require careful data management and caching.
- State management patterns: back backend storage and optional caching; avoid in-memory shared state.
- 12-factor app principles: design for cloud deployment, portability, and independent deployment/scaling.
- REST and API design: consistent, well-defined contracts; domain-oriented resources; loose coupling.
- REST vs gRPC: REST for external/public APIs; gRPC for internal high-performance/streaming scenarios.
- API contracts and versioning: maintain backward-compatible contracts; plan deprecation and rollback.
- External vs internal concerns: expose stable APIs; design internal APIs for performance and language support when needed.
- API guidelines and tooling: OpenAPI for REST; protocol buffers for gRPC; API management patterns.
- Cloud deployment patterns: utilize cloud compute options and managed services with appropriate granularity.

## Practical Guidance
- Decompose by feature: form mini-apps around features; isolate shared functionality (e.g., authentication) for separate deployment.
- Data ownership: give each service its own datastore; avoid datastore-level coupling; choose storage per service needs.
- State handling: recognize stateful components early; use backend storage (e.g., Firestore, Cloud SQL) and caching where appropriate.
- Stateless first: design services to be stateless; plan for stateful needs with dedicated stores or caches.
- Service contracts: define strong, versioned contracts; maintain backward compatibility; plan deprecation and rollback.
- API design discipline: design around domain concepts; use REST with consistent URIs, JSON/XML payloads; consider HATEOAS for navigable APIs.
- When to use gRPC: internal service communication requiring performance, streaming, or multi-language support; expose via HTTP/2/Envoy if needed.
- API contracts and tooling: adopt OpenAPI for REST; use protocol buffers for gRPC; generate client/server stubs from contracts.
- API management: consider Cloud Endpoints, Apigee, API Gateway for auth, monitoring, security, and consistent policy enforcement.
- Deployment and operations: apply 12-factor decoupling; use IaC (Terraform) and containers; ensure dev/prod parity; log to stdout and centralize logs.
- Observability and admin tasks: centralize logging, treat admin tasks as separate one-off processes (Cloud Tasks, Cloud Scheduler, cron jobs).
- Dev/prod parity: keep development, staging, and production aligned to reduce environment-related issues.
- Cloud platform alignment: map services to Google Cloud offerings (App Engine, Cloud Run, GKE, Compute Engine, Cloud SQL, Firestore, Memorystore) and use appropriate networking/load balancing.

## Services/Tools Mentioned
- Cloud platforms and services: Google Cloud (App Engine, Cloud Run, GKE, Compute Engine, Cloud SQL, Firestore, Memorystore for Redis, Cloud DNS, Cloud Tasks, Cloud Scheduler, Cloud Storage)
- Networking/load balancing: Network Load Balancer, Application Load Balancer
- API design and contracts: REST, gRPC, OpenAPI, protocol buffers, Swagger
- API management: Cloud Endpoints, Apigee, API Gateway
- Tooling and IaC: Terraform, Google Cloud Source Repositories, Artifact Registry
- Containerization and runtime: Docker, containers, environment variables
- Data and state: Firestore, Cloud SQL, Memorystore
- Miscellaneous: URL-based backing services, HATEOAS, JSON/XML, versioning, plural/singular resource URIs

## Quick Revision Notes
- Design with clear service boundaries and domain-driven grouping; own your datastore per service.
- Prefer stateless services; for stateful needs, use backend storage and caching; avoid in-memory shared state.
- Decompose by feature to minimize cross-service coupling and enable independent deployments.
- Expose stable RESTful APIs with domain-oriented contracts; use versioning and backward-compatible changes.
- Use gRPC for internal high-performance needs; consider HTTP/2 and Envoy for exposure in cloud environments.
- Maintain a strict build/release/run discipline with identifiable artifacts for easy rollbacks.
- Centralize logs (stdout) and ensure observability across dynamic, scalable deployments.
- Treat admin tasks as separate one-off processes (cron, Cloud Tasks, Cloud Scheduler).
- Strive for dev/prod parity using IaC and containers; keep environments similar and automatable.
- Follow Google API design patterns and OpenAPI for REST; use protocol buffers for gRPC; design with consistency and minimal surface area.
- Use API management tools to secure, monitor, and standardize APIs across services.
