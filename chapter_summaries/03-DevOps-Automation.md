# 03 DevOps Automation

## Overview
Chapter 03, DevOps Automation, combines CI/CD with infrastructure as code (IaC) to enable fast, reliable, and repeatable software delivery. It emphasizes on-demand, cloud-based builds, centralized artifact management, and automated quality and security checks. Key pillars include microservices with independent repos, Terraform-driven provisioning, and deployment governance using Binary Authorization and attestations. It also covers deploying to multiple runtimes (GKE, Cloud Run, Compute Engine, App Engine) with secure, auditable workflows.

## Key Concepts
- DevOps automation as a driver of consistency, reliability, and deployment speed
- CI/CD pipelines with automated quality gates (linting, SonarQube, integration tests, test reports) and image scanning
- On-demand provisioning for automated pipelines and deployment environments
- Infrastructure as Code (IaC) as the core approach to provisioning, configuring, and deploying infrastructure
- Terraform as the primary IaC tool for Google Cloud resources; declarative, parallel deployment, template-driven
- Disposable, ephemeral infrastructure and environments; treat machines as replaceable
- Declarative infrastructure provisioning and modular templates for reuse and disaster recovery
- Microservices architecture with separate repositories per service
- Centralized artifact management via Artifact Registry; supports Docker/OCI images and deployment packages
- CI/CD integration with Google Cloud tools: Cloud Source Repositories, Cloud Build, Build Triggers
- Security and compliance: vulnerability scanning, Artifact Analysis, Pub/Sub signaling
- Deployment governance with Binary Authorization and Kritis attestations to gate production deployments
- Multi-runtime deployment: GKE, Cloud Run, Compute Engine, App Engine
- Cloud-native ecosystem on Google Cloud: Cloud Source Repositories, Cloud Build, Artifact Registry, Terraform, SonarQube, Pub/Sub

## Practical Guidance
- Organize per-service repos: each microservice should have its own repository to enable independent CI/CD.
- Enforce strong CI gates: fail the pipeline on unit test failures; include linting, quality analysis, integration tests, and test reporting; run image vulnerability scans.
- Centralize artifacts: store Docker/OCI images and deployment packages in Artifact Registry; enable vulnerability analysis and IAM-based access control.
- Use on-demand, cloud-based builds: prefer Cloud Build for scalable, managed builds with steps as containers.
- Automate builds with triggers: configure build triggers that start on code changes, with branch/tag/regex filtering.
- IAM and access controls: manage access to Cloud Source Repositories with IAM; integrate Pub/Sub for repository events and vulnerability scan results.
- Security gating: enable Binary Authorization on GKE and require attestations (via Kritis signer) before deployment; use attestations to verify trusted origins.
- Vulnerability-driven deployment: run container image scans during the deployment workflow; surface findings to operators.
- Multi-runtime deployment: design pipelines to deploy to GKE, Cloud Run, Compute Engine, and App Engine via Artifact Registry.
- IaC on the cloud: automate everything with Terraform; treat infrastructure as disposable and reproducible.
- Templates and modularization: use Terraform modules/templates to abstract resources and accelerate DR planning.
- Parallel provisioning: leverage Terraform’s parallel deployments to speed up infrastructure provisioning.
- Start with Google Cloud provider: define resources (compute, VPC, firewall, load balancing, VPN, router) and outputs to capture results.
- Integrate IaC into CI/CD: embed IaC provisioning into your deployment flow for rapid, repeatable releases.

## Services/Tools Mentioned
- DevOps Automation (concept)
- Cloud Source Repositories
- Cloud Build
- Build Triggers
- Artifact Registry
- Terraform
- HashiCorp Configuration Language (HCL)
- SonarQube
- Pub/Sub
- GitHub
- Bitbucket
- Google Kubernetes Engine (GKE)
- App Engine
- Compute Engine
- Docker / Docker images
- OCI container images
- Binary Authorization
- Kritis
- Attestor / attestation
- Artifact Analysis
- Vulnerability scanners
- Virtual machines, serverless, Kubernetes
- Cloud Shell
- Google Cloud IAM
- Clouds resources: VPC, Compute Engine, Firewalls, Load Balancers, VPN, Cloud Router

## Quick Revision Notes
- Use separate repos per microservice to enable independent CI/CD.
- Stop the CI pipeline on unit test failures; include linting, quality analysis, integration tests, and image scanning.
- Centralize artifacts in Artifact Registry; enable vulnerability analysis and IAM controls.
- Favor on-demand Cloud Build runs; automate with build triggers (branch/tag/regex).
- Gate deployments with Binary Authorization and attestations (Kritis signer) before deploying to GKE.
- Surface vulnerability findings via Pub/Sub for visibility and response.
- Gate deployments with container image attestations; rely on image scans during upload.
- Design for multi-runtime deployment (GKE, Cloud Run, Compute Engine, App Engine) via Artifact Registry.
- Treat all infrastructure as disposable; recreate rather than patch in place.
- Use IaC as the single source of truth; automate provisioning and testing with Terraform.
- Build modular, template-driven configurations to support DR and scalable environments.
