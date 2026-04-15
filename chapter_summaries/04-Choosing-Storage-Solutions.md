# 04 Choosing Storage Solutions

## Overview
Choosing Storage Solutions guides you to map data characteristics to Google Cloud storage and database offerings, balancing data type, durability, availability, scalability, performance, and cost. It emphasizes per-service responsibilities, microservices data ownership, and practical transfer options (on-prem to cloud and SaaS data movement) to support durable, scalable architectures.

## Key Concepts
- Data-type mappings:
  - Object/Binary: Cloud Storage
  - Relational: Cloud SQL, Spanner, AlloyDB
  - NoSQL/Unstructured: Firestore, Bigtable
  - In-memory caching: Memorystore
  - File storage: Filestore
  - Block storage: Persistent Disk
  - Data analytics/warehouse: BigQuery
- Availability and durability:
  - SLAs depend on multi-region vs regional configurations; durability is a shared responsibility (include backups, versioning, snapshots, lifecycle policies).
  - Durability features: Cloud Storage versioning, backups/point-in-time recovery (Cloud SQL), automatic replication (Spanner/Firestore), exports to Cloud Storage.
- Scaling and consistency:
  - Scaling models: horizontal (Bigtable, Spanner), vertical (Cloud SQL, Memorystore), automatic/elastic (Cloud Storage, BigQuery, Firestore).
  - Consistency: strong vs eventual; many services offer strong consistency, some default to eventual (Bigtable, Memorystore replicas); plan according to needs.
- Cost considerations:
  - Per-GB and per-operation costs vary; consider small datasets (Bigtable/Spanner high cost), Firestore reads/writes, Cloud Storage cheap but not a database, BigQuery storage vs query costs.
- Data transfer and integration:
  - Data transfer options include Storage Transfer Service, Transfer Appliance, and Data Transfer Service for SaaS sources; on-prem transfers require specific prerequisites and security controls.

## Practical Guidance
- Characterize data first:
  - Use Cloud Storage for raw/binary data and large binary objects.
  - Use Cloud SQL or Spanner for structured relational data; AlloyDB for HTAP with PostgreSQL compatibility.
  - Use Firestore or Bigtable for NoSQL/unstructured workloads; Memorystore for caching; Filestore for shared file systems; BigQuery for analytics.
- Design for durability and backups:
  - Enable Cloud Storage versioning; implement lifecycle policies.
  - Schedule Cloud SQL backups; rely on Spanner/Firestore automatic replication.
  - Plan export/import data paths to Cloud Storage for durable custody.
- Plan for scale and consistency:
  - Decide horizontal vs vertical vs automatic scaling per workload.
  - Define required consistency per service early to guide selection (strong vs eventual).
- Conduct cost analysis:
  - Assess storage footprint and operation costs (reads/writes for Firestore, per-GB storage, query costs for BigQuery).
- Microservices data ownership:
  - Assign each service its own data store and document its data type, structure, consistency, volume, and access patterns.
- Data transfer strategies:
  - For large on-prem data: use Transfer Appliance with AES-256 encryption, tamper-evident procedures, and secure erasure per NIST-800-88.
  - For ongoing SaaS-to-big-data pipelines: use BigQuery Data Transfer Service with supported connectors (Ads, Campaign Manager, YouTube) and other sources (Teradata, Redshift, S3).
  - For ongoing or scheduled cloud-to-cloud or cross-provider transfers: use Cloud Storage Transfer Service; plan schedules, filters, and deletions.
- On-prem to cloud specifics:
  - Ensure Posix source compatibility, Docker-enabled Linux agent, outbound ports 80/443, bandwidth planning (e.g., minimum 300 Mbps), and monitor transfer timelines.
- Reference mapping and design guidance:
  - Use the Design and Process Workbook to map cases to storage choices; apply example mappings (e.g., raw data to Cloud Storage, relational data to Cloud SQL, analytics to BigQuery).
- Security and governance:
  - Encrypt data at capture (AES-256 when applicable); manage keys securely; ensure proper data erasure after transfers per standards.

## Services/Tools Mentioned
- Cloud Storage
- Cloud SQL
- Spanner
- AlloyDB
- Firestore
- Bigtable
- Memorystore
- BigQuery
- Filestore
- Persistent Disk
- Storage Transfer Service
- Transfer Appliance
- BigQuery Data Transfer Service
- Cloud Storage Transfer Service
- AWS S3 (as transfer source/destination references)
- Teradata
- Amazon Redshift
- Amazon S3
- HTAP (hybrid transactional/analytical processing)
- NIST-800-88 (data erasure standard)
- Design and Process Workbook, Activity 7 (workbook guidance)

## Quick Revision Notes
- Map data types to the right store: binary to Cloud Storage, relational to Cloud SQL/Spanner/AlloyDB, NoSQL to Firestore/Bigtable, analytics to BigQuery, caching to Memorystore.
- Plan for durability and backups from the start; enable versioning and lifecycle policies; use point-in-time recovery where applicable.
- Choose scaling model per workload; decide on strong vs eventual consistency early.
- Use per-service data ownership in microservices to guide storage decisions.
- Leverage Transfer Appliance for large on-prem transfers and Data Transfer Service for SaaS/cloud data transfers; use Transfer Service options to manage schedules and formats.
- Consider total cost per GB and per operation; Cloud Storage is cheap but not a database; BigQuery storage plus query costs require planning.
- Follow security best practices: encryption at capture, key management, and compliant data erasure after transfers.
