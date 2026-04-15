# 08 Security

## Overview
Chapter 08 reinforces a security-first mindset as the foundation for safe innovation. It emphasizes a true shared responsibility model between Google Cloud and customers, a defense-in-depth approach, and clear governance. Practical guidance covers identity and access management, network security, edge protection, encryption, data loss prevention, and auditing. The goal is to design for least privilege, strong governance, private networking, and proactive threat mitigation, while keeping compliant with standards and maintaining visibility through comprehensive logging.

## Key Concepts
- Security-first mindset and defense in depth: layered security from hardware to applications; monitor and audit with configurable tools.
- Shared responsibility model: Google protects underlying platform and services; customers configure and operate their workloads correctly.
- Governance and organization: use Organization policies and folders to simplify policy inheritance and enforcement.
- Identity and access management: IAM roles, Identity-Aware Proxy (IAP), Identity Platform; manage machine identities with service accounts; grant roles to groups; prefer least privilege.
- Network security: private IPs, firewall rules, and Google Cloud private access; minimize public exposure.
- DDoS protection: leverage Cloud DNS, Google Cloud Armor, edge protections.
- Observability and compliance: Security Command Center; regular auditing of admin/data/VPC/firewall/system logs; be aware that cloud certs do not certify your app.
- Access boundaries and boundary controls: bastion/IAP SSH, Cloud NAT, Private Google Access; restrict external access and terminate at security boundaries.
- Data and encryption: DEKs and KEKs with Cloud KMS; CMEK for customer-managed encryption; CSEK for customer-supplied keys.
- Data protection tooling: DLP API for detection, redaction, masking, and tokenization; TLS/HTTPS for all endpoints; API management with Cloud Endpoints.
- Edge and API security: Cloud Armor at the edge; Layer 7 WAF rules; TLS everywhere; private access for internal services.
- Compliance awareness: standards such as ISO/IEC 27001, HIPAA, SOC 1; certification does not imply app-level compliance.

## Practical Guidance
- Enforce identity and access controls:
  - Use IAP to require login and grant access without VPNs where possible.
  - Deploy Identity Platform for CIAM needs; choose providers/protocols (SAML, OpenID, Email/Password, etc.).
  - Grant roles to groups; apply least privilege; avoid owner/editor roles for routine access.
  - Restrict who can create VMs with service accounts; use ServiceAccountUser where appropriate.
- Harden networks and access:
  - Remove external IPs where feasible; use bastion/IAP SSH or Cloud NAT; enable Private Google Access for internal-only resources.
  - Implement default-deny ingress; craft precise firewall rules by IP/port/protocol.
  - Place Cloud Armor in front of a global external load balancer; apply Layer 7 WAF rules for common attacks.
- Protect and manage keys and encryption:
  - Prefer CMEK in Cloud KMS for storage resources; rotate keys (rotation default ~90 days); enable automatic rotation where possible.
  - If using user-provided keys, understand CSEK behavior (keys are supplied per API call and only cached in RAM).
  - Control key creation permissions; avoid broad access to keys.
- API and data protection:
  - Use Cloud Endpoints to secure APIs; guard with JWTs and API keys; integrate with Identity Platform.
  - Ensure TLS/HTTPS for all endpoints and secure load balancer frontends.
  - Use DLP to detect and redact sensitive data in storage and databases.
- Observability and governance:
  - Regularly review Security Command Center findings and fix vulnerabilities.
  - Audit admin, data access, VPC flow, firewall, and system logs; act on detections and anomalous activity.
  - Design architectures with clear policy inheritance (org → folders → projects → resources) and multi-project separation to reduce risk.

## Services/Tools Mentioned
- Security Command Center
- Organization policies
- Folders
- IAM (Identity and Access Management)
- Identity-Aware Proxy (IAP) / Cloud IAP
- Identity Platform
- Service accounts
- ServiceAccountUser role
- Private Google Access
- Bastion host / IAP SSH / Cloud NAT
- Firewalls
- Google Cloud private access
- Cloud DNS
- Google Cloud Armor
- Audit logs (Admin, Data access, VPC Flow, Firewall, System)
- Google Cloud Console
- Groups
- Roles
- Projects
- Organizations
- ISO/IEC 27001, HIPAA, SOC 1 compliance
- Cloud Endpoints
- TLS / HTTPS
- Global Load Balancing
- Cloud Load Balancing
- Cloud CDN
- API Gateway
- Data Encryption Key (DEK)
- Key Encryption Key (KEK)
- Cloud KMS
- Customer Managed Encryption Keys (CMEK)
- Customer Supplied Encryption Keys (CSEK)
- Cloud Storage
- Compute Engine
- Data Loss Prevention (DLP) API
- BigQuery
- Firestore
- App Engine
- gcloud

## Quick Revision Notes
- Security first: design for least privilege, separation of duties, and regular audits.
- Guard at the edge: use Google Cloud Armor with a global external load balancer; default-deny ingress.
- Authenticate and authorize: rely on IAP and Identity Platform; assign roles to groups.
- Minimize exposure: reduce external IPs; use Private Google Access, Bastion/IAP SSH, and Cloud NAT.
- Encrypt everywhere: use DEK/KEK with CMEK; consider CSEK only when necessary; rotate keys regularly.
- Protect APIs: secure via Cloud Endpoints; require TLS/HTTPS; manage keys and JWTs.
- Data protection: use DLP for sensitive data discovery/redaction.
- Visibility: use Security Command Center and comprehensive logs to detect and respond to threats.
- Governance: enforce policies via org/folder inheritance; use multiple projects to separate duties.
- Compliance reminder: cloud certs do not certify your app; ensure your app meets applicable standards.
