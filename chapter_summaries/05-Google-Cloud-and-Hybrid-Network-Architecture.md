# 05 Google Cloud and Hybrid Network Architecture

## Overview
This chapter guides designing a Google Cloud and hybrid network that balances cost, security, and performance. It covers global VPC concepts, subnet and IP planning, and centralized governance via Shared VPC. It explains load balancing strategies (global HTTP(S) vs regional TCP), the use of Cloud CDN to reduce latency and egress, and how to connect on-premises or other clouds through peering, VPN (Classic/HA), and Cloud Interconnect (Dedicated/Partner). The guidance emphasizes planning for global reach, fault tolerance, and scalable network management with Network Intelligence Center and Cloud Router/BGP for dynamic routing. A two-tier approach separates public front-ends from internal services, while security and policy controls keep operations compliant and maintainable.

## Key Concepts
- Global VPCs and subnets: VPCs are global; subnets are regional. Resources communicate via internal IPs; cross-region connectivity is seamless within a VPC.
- VPC modes and ownership: Auto mode vs custom mode; multiple VPCs per project; Shared VPC with a host and service projects for centralized governance.
- Subnet design: non-overlapping IP ranges; primary and secondary/alias ranges; subnets expandable without downtime.
- VM networking: up to 8 network interfaces per VM; interfaces connect to subnets in the VM’s region; interfaces defined at instance creation.
- Load Balancing: 
  - Application Load Balancer (Layer 7) for HTTP/HTTPS with features like SSL termination and content-based routing.
  - Network Load Balancer (Layer 4) for IP/port-based traffic (TCP/UDP) with low latency/high throughput.
  - Proxy passthrough and hybrid frontend options referenced.
- Cloud CDN: caches static content globally via edge locations (global external ALBs-backed).
- Connectivity options: VPC Peering, Cloud VPN (Classic/HA), Cloud Interconnect (Dedicated/Partner); use Cloud Router and BGP for dynamic routing.
- Global vs regional reach: global HTTP load balancers for internet-facing traffic; regional TCP load balancers for internal services.
- Security and certs: SSL/TLS best practices for public IPs; certificate management (Google-managed or self-managed).
- Observability: Network Intelligence Center for topology visualization and connectivity testing.
- On-prem integration: Private Google Access to reach Google services via private IPs from on-prem networks.
- Common terms: GFEs, Envoy proxy, *_MANAGED, non-overlapping subnets, IP aliasing, public vs internal endpoints.
- SLA and design cautions: HA VPN SLA depends on redundant tunnels/interfaces; MTU considerations; dynamic routing vs static routing; ECMP considerations with AWS.

## Practical Guidance
- Start with traffic characterization:
  - External internet-facing services: use Global HTTP(S) Load Balancer.
  - Internal services: use regional TCP Load Balancers.
  - Map services to appropriate load balancers first, then layer in Cloud CDN where beneficial.
- Design for global reach and fault tolerance:
  - Place subnets across regions to serve global users; designate a nearest region plus a backup region.
  - Use Shared VPC to centralize network policy and remove broad admin rights.
  - Enable Cloud CDN on global front-ends to reduce latency and egress costs.
- Subnet and IP planning:
  - Ensure non-overlapping IP ranges within a VPC; leverage primary and alias/secondary ranges for flexibility.
  - Plan subnet expansions to avoid downtime; document all ranges and peers.
- Security and policy:
  - Secure public IP endpoints with SSL; leverage ALB for HTTPs termination or proxy NLB as appropriate.
  - Enforce organizational policies via Shared VPC (disable default networks, restrict network admins).
- Connectivity choices and redundancy:
  - Peering for private VPC-to-VPC connectivity; VPN for on-prem/cloud connectivity; Interconnect for high-bandwidth needs.
  - For VPN, design HA VPN with two active tunnels and two external IPs per gateway to meet 99.99% SLA; use Cloud Router for dynamic routing (BGP).
  - When connecting to AWS, use two VPN connections for redundancy; consider Transit Gateway for ECMP with AWS.
  - MTU should be capped at 1460 bytes for VPN tunnels; prefer dynamic routing over static where possible.
- Observability and optimization:
  - Use Network Intelligence Center to validate topology and test connectivity during design and operations.
  - Regularly review latency, egress costs, and cross-region traffic patterns; adjust subnets, CDNs, and load balancer placements accordingly.
- On-prem and private access:
  - Use Private Google Access to let on-prem hosts reach Google services privately.
  - For analytics or reporting workflows, connect on-prem networks to cloud services via VPN or Interconnect as appropriate.
- Typical architectural pattern:
  - Global HTTP Load Balancer for public front-ends (Search/Web UI).
  - Regional TCP Load Balancers for internal/back-end services (Inventory/Orders).
  - VPN or Interconnect as the secure bridge to on-premises or other clouds.
  - Cloud CDN to accelerate content delivery for public services.

## Services/Tools Mentioned
- VPC networks, subnets, auto mode, custom mode, internal IPs, IP aliasing, secondary/alias ranges
- Cloud CDN
- Global and Regional Load Balancers; Application Load Balancer (Layer 7); Network Load Balancer (Layer 4); proxy/ passthrough variations
- Compute Engine; GKE; Cloud Storage; Shared VPC (Host Project, Service Project)
- Network Intelligence Center
- Peering; Cloud VPN (Classic VPN, HA VPN); Cloud Interconnect (Dedicated, Partner)
- Cloud Router; BGP; ECMP
- Regions; Points of Presence (PoPs); global private network
- SSL/TLS certificates (Google-managed or self-managed)
- Private Google Access
- GFEs (Google Front Ends); Envoy proxy
- Two-tier architecture (public HTTP LB + regional TCP LBs)
- AWS integration concepts (Transit Gateway, VGW) for VPN cross-cloud setups
- MTU considerations (VPN 1460-byte limit)

## Quick Revision Notes
- Global VPCs with regional subnets enable cross-region internal communication.
- Shared VPC centralizes networking and policy; enforce least privilege for admins.
- Use Global HTTP(S) LB for public traffic; regional TCP LBs for internal services.
- Enable Cloud CDN on global front-ends to lower latency and egress.
- Plan IPs carefully: non-overlapping subnets; use alias ranges; allow subnet expansion with no downtime.
- For high-availability VPNs, deploy two active tunnels and two external IPs; enable dynamic routing with Cloud Router (BGP).
- Prefer Dedicated Interconnect for high bandwidth; Partner Interconnect for flex and lower bandwidth needs.
- For on-prem access to Google services, enable Private Google Access.
- Use Network Intelligence Center to validate topology and test connectivity during design and operations.
- Ensure SSL is terminated or appropriately configured on public front-ends; manage certificates (Google-managed or self-managed).
