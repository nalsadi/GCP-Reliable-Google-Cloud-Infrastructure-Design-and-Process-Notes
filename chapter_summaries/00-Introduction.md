# 00 Introduction

1) Key concepts
- Course focus: architecture, design, and process for reliable cloud infrastructure on Google Cloud.
- Role of cloud architect: determine which cloud services to use to implement applications effectively.
- Microservices: architectural style that decomposes applications into independent parts; affects agility, development speed, deployment, and monitoring.
- Requirements gathering: define what the software does, who users are, and why it matters; start from this phase.
- Design process: rough/structured design and iteration; weigh trade-offs to reach best solution given constraints.
- Service selection: choose storage (relational, NoSQL, data warehouse) and deployment (VMs, Kubernetes, App Engine) using objective criteria.
- Reliability considerations: availability, durability, cost, and disaster recovery; design to meet goals.
- Security: security is baked into the design; layered security; Google Cloud provides controls; security is a shared responsibility.
- Monitoring: use dashboards, logs, error reporting, and tracing to evaluate if service goals are met.
- Course structure: part of the Cloud Infrastructure learning path; includes lectures, design activities, hands-on labs; emphasis on design work.
- Prerequisites: course builds on Architecting with Google Compute Engine or Kubernetes Engine; not a first exposure to Google Cloud.
- Case study/workbook: design activities (with examples like online banking, ride-sharing, online shopping, ClickTravel).

2) Important design/process recommendations
- Start with well-defined requirements before architecture.
- Decompose applications into microservices to improve agility.
- Use objective criteria to select storage and deployment services tailored to each microservice.
- Design for reliability from the outset (consider availability, durability, disaster recovery, and costs).
- Incorporate security from the beginning; apply layered security and recognize shared responsibility.
- Plan for monitoring from the start; define requirements and use monitoring tools to measure success.
- Invest substantial time in design and architecture activities; there are often multiple viable solutions.
- Use the provided case-study workbook and design activities to practice; understand that feedback is provided via sample solutions.
- Recognize that the course emphasizes architecture/design/process rather than implementing specific cloud features.

3) Terms or services mentioned
- Microservices; API Gateway; Identity
- Storage options: relational database, NoSQL database, data warehouse
- Compute options: virtual machines, Kubernetes cluster, App Engine
- Google Cloud services (general reliability-related offerings)
- Google Compute Engine; Google Kubernetes Engine
- App Engine
- Monitoring components: dashboards, logs, error reporting, tracing
- Security concepts: layered security; security controls; physical hardware security
- Hybrid network architecture; cloud/hybrid deployments
- Case study examples: online banking portal, ride sharing application, online shopping site, ClickTravel (online travel portal)

4) Explicit best practices or cautions
- There is no single right answer; design involves weighing pros and cons given requirements and constraints.
- Microservices bring agility but require consideration of their own trade-offs; the course discusses advantages and disadvantages.
- Security is integral, not optional; design should bake security in and acknowledge shared responsibility between you and cloud controls.
- The course focuses on architecture/design/process rather than implementing specific cloud features.
- More effort in design activities yields greater learning and understanding.
