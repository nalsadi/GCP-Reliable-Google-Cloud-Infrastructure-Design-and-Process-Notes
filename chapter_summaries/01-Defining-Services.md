# 01 Defining Services

## Overview
This chapter defines how to scope and design services around business value. It emphasizes starting from business requirements, translating them into measurable KPIs, and using user-centered techniques (roles, personas, and user stories) to drive design. It then introduces service quality constructs (SLIs, SLOs, SLAs) and practical guidance for crafting realistic, testable requirements and reliable service levels.

## Key Concepts
- Business vs. technical requirements: focus on business value and measurable impact.
- KPIs and SMART criteria: metrics that quantify progress toward business goals; KPIs should be Specific, Measurable, Achievable, Relevant, Time-bound.
- SLOs, SLIs, SLAs: SLIs are indicators, SLOs are targets for those indicators, and SLAs are binding contracts with consequences.
- Qualitative vs. quantitative requirements: Who/What/Why/When/How questions shape user needs; KPIs quantify outcomes.
- Roles and personas: roles describe objectives; personas are stories that represent those roles to guide design.
- User stories and INVEST: clear, testable features from a user perspective; INVEST ensures stories are Independent, Negotiable, Valuable, Estimatable, Small, and Testable.
- Measurement practices: use time-bound metrics and appropriate aggregation (prefer percentiles over averages to reveal tail latency).

## Practical Guidance
1) Start with business outcomes: articulate the value the service delivers.
2) Gather requirements: separate functional, non-functional, and business value needs; define qualitative drivers and quantitative targets.
3) Define KPIs using SMART criteria; tie KPIs to business goals.
4) Model user perspective: define roles, translate to personas, and consolidate overlaps.
5) Write user stories: include a clear title and concise description; use Given/When/Then if helpful.
6) Apply INVEST to each story for better planning and feedback.
7) Specify service quality: establish SLIs, set realistic SLOs, and determine SLAs where appropriate.
8) Choose right metrics: for user-facing systems, prioritize availability, latency, and throughput; for data-heavy systems, emphasize latency and durability.
9) Set measurement windows and methods: ensure consistency across SLI/SLO/SLA definitions; use time-bounded evaluations.
10) Plan for capacity: maintain spare capacity to meet targets and absorb variability.
11) Engage real users when possible; otherwise, rely on imaginative personas for practice in coursework or scenarios.
12) Iterate: refine roles, personas, and user stories as you learn from measurements and feedback.
13) Keep targets realistic: avoid 100% availability; start with achievable SLOs and tighten as you mature.

## Services/Tools Mentioned
- KPI, SLI, SLO, SLA concepts (measurement and contractual framework)
- SMART criteria for KPIs
- Roles and Personas (e.g., fictional representations to guide requirements)
- User Stories (incl. Given/When/Then variant)
- INVEST criteria for evaluating stories
- Upptime checks (example mechanism for uptime/availability monitoring)
- Example domains: MegaCorp Bank, online travel portal, ClickTravel (illustrative contexts)
- Latency, throughput, availability, durability as core metrics

## Quick Revision Notes
- Begin with business value; KPIs must reflect business goals, not just technical targets.
- Distinguish qualitative requirements (who/what/why) from quantitative ones (metrics).
- Use roles and personas to capture diverse user perspectives; write user stories that are independent, negotiable, valuable, estimatable, small, and testable.
- Define SLIs/SLOs first; only then consider SLAs; ensure SLIs/SLOs are measurable and time-bound.
- Keep SLOs realistic and user-focused; prefer multiple targeted SLOs over a single, unrealistic goal.
- Use percentiles rather than averages to assess latency and tail performance.
- Align software metrics with business objectives; plan capacity to meet SLAs and maintain reliability.
