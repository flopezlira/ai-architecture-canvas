# 🧠 AI Architecture Canvas — Comprehensive Guide for AI Architects (v1.1 • draft)

**Author:** Francisco López-Lira  
**Contact:** flopezlira@gmail.com  
**Repository:** https://github.com/flopezlira/ai-architecture-canvas  
**Base:** *AI Architecture Canvas – Project Edition (v1.0)*  
**License:** CC BY-NC-SA 4.0 — Open Framework for Trustworthy AI Systems  

---

> This guide transforms the Canvas into a **practical handbook** for AI architects.  
> It includes checklists, expected deliverables, relevant standards, and anti-patterns for each block.  
> Designed for projects combining **classical ML**, **LLMs/GenAI**, and **edge/cloud** setups.

---

[← Back to Baseline](AI_Architecture_Canvas_v1.0.md)

---

## Table of Contents
1. Guiding principles  
2. Lifecycle flow and artifacts  
3. RACI summary by discipline  
4. Block 1 — Business value & problem definition  
5. Block 2 — Data strategy  
6. Block 3 — Model strategy  
7. Block 4 — Technical architecture & infrastructure  
8. Block 5 — Integration & decision loop  
9. Block 6 — MLOps & operations  
10. Block 7 — Monitoring & governance (technical)  
11. Block 8 — Ethics & responsibility (social)  
12. Block 9 — Efficiency & sustainability (FinOps/GreenOps)  
13. Gate reviews & quality checkouts  
14. Practical annexes (templates, glossary, references)

---

## 1) Guiding Principles

- **Business-first:** every technical requirement maps to a measurable outcome (KPI/OKR).  
- **Evidence-based:** decisions backed by data, A/B tests, or offline→online evaluation.  
- **Defense-in-depth:** security, privacy, and compliance by design.  
- **Lean & modular:** avoid unnecessary lock-in; use ports/adapters; versioned contracts.  
- **Total observability:** telemetry across data→model→serving→business.  
- **Shared responsibility:** product, data, science, platform, and legal teams aligned.

---

## 2) Lifecycle Flow & Artifacts

**Design → Build → Deploy → Operate → Govern → Improve**

1 → 2 ↔ 3 ↔ 4 → 5 → 6 → 7 → 8 → 9


**Key artifacts by phase**  
- **Design:** prioritized use cases, KPIs, stakeholder map, Data & Model Cards v0, logical architecture, risk assessment.  
- **Build:** data pipelines (DAGs), training/serving code, tests, data/API contracts, IaC.  
- **Deploy:** manifests (K8s/Run/Functions), feature flags, canary/blue-green, security checklist.  
- **Operate:** dashboards, alerts, retraining/rollback policies, runbooks.  
- **Govern:** audits, traceability, model inventory, DPIA/AI Act mapping, control agreements.  
- **Improve:** post-mortems, drift reviews, cost/energy optimization, next iteration plan.

---

## 3) RACI Summary by Discipline

| Discipline | R | A | C | I |
|---|---|---|---|---|
| Product | Prioritization, KPIs | Value approval | Legal, Sales | Leadership |
| AI Architecture | Overall design | Technical co-approval | Security, Data | Others |
| Data Science | Experiments | Model metrics | Product | MLOps |
| Data/Engineering | Ingestion, quality | Lineage | Security | Product |
| MLOps/Platform | CI/CD/CT, serving | SLOs | Architecture | Support |
| Legal/Ethics | Evaluations | Compliance | Product | Leadership |

---

## 4) Block 1 — Business Value & Problem Definition
**Goal:** Align AI work with verifiable business outcomes.

**Quick checklist**
- [ ] Problem framed in end-user language.  
- [ ] Impact KPIs (€, %, time, NPS, risk).  
- [ ] Bridge metrics model→business (precision@K → revenue).  
- [ ] Hypotheses and assumptions validated (data, adoption).  
- [ ] Stakeholder map and RACI.  
- [ ] Boundaries: what the system will **not** do.

**Deliverables:** 1-pager use case, KPI baseline, story map, success/exit criteria.  
**Anti-patterns:** tech-first thinking; accuracy-only KPIs; ignoring integration cost.  
**Templates:** *Business Case Canvas*, *Impact Map*.

---

## 5) Block 2 — Data Strategy
**Goal:** Ensure data is **useful, legal, and trustworthy**.

**Checklist**
- [ ] Source inventory (systems, owners, SLAs).  
- [ ] Quality: completeness, validity, timeliness, known bias.  
- [ ] Data lineage and schema contracts.  
- [ ] Governance: roles (steward), catalog/metadata, retention & deletion.  
- [ ] Privacy (GDPR): legal basis, minimization, anonymization/pseudonymization, DPIA if required.  
- [ ] Security: classification, encryption at rest/in transit, least-privilege access.  
- [ ] Feature Store (if applicable) and temporal train/val/test split.  
- [ ] Preliminary Data Cards.

**Deliverables:** data dictionary, access policies, data/API contracts, DAGs, quality metrics, Data Card v1.  
**Anti-patterns:** silent schema drift; scraping without legal basis; one-off datasets.  
**Templates:** DPIA checklist, quality matrix, *data contracts*, basic catalog.

---

## 6) Block 3 — Model Strategy
**Goal:** Select, train, and evaluate the right approach (ML/GenAI/RL) with explainability and robustness.

**Checklist**
- [ ] Simple baseline and “champion/challenger.”  
- [ ] Metrics by class/segment; cost-sensitive evaluation.  
- [ ] Robust validation (temporal, stratified, leakage control).  
- [ ] Explainability (SHAP/LIME/counterfactuals) and *Model Card*.  
- [ ] Robustness: adversarial tests, out-of-distribution.  
- [ ] For **LLMs/GenAI**: *API vs open-weights*, RAG (sources, chunking, evaluators), *guardrails* (regex/LLM-as-judge), *prompt/versioning*, automatic & human evaluation, data policies (no-train).  
- [ ] For **RL/online**: *safe exploration*, simulators, boundaries.  
- [ ] Licensing & IP rights.

**Deliverables:** reproducible notebooks, versioned datasets, evaluation report, *Model Card*, model risk matrix.  
**Anti-patterns:** overfitting to offline AUC; unmanaged *prompt rot*; hidden prompts.  
**Templates:** *Model Card*, *Prompt Registry*, RAG evaluation guide.

---

## 7) Block 4 — Technical Architecture & Infrastructure
**Goal:** Define compute, storage, network, and security topology for scalable serving.

**Checklist**
- [ ] Logical & deployment diagrams (cloud/edge/hybrid).  
- [ ] Serving strategy: batch, streaming, online (REST/gRPC), WebHooks.  
- [ ] Autoscaling & rate-limits; circuit breakers; exponential backoff.  
- [ ] Multitenancy & isolation (namespaces, projects, VPCs).  
- [ ] Security: IAM, managed secrets, image scanning, SBOM, WAF/API-GW, artifact signing, policy-as-code.  
- [ ] Observability: logs, metrics, traces (OpenTelemetry), SLO/SLA.  
- [ ] IaC (Terraform/Ansible), environment separation (dev/stage/prod).  
- [ ] Costing & capacity planning (GPU/CPU/RAM/IO).  
- [ ] Edge strategy (sync, caching, offline tolerance).

**Deliverables:** ADRs, C4 diagrams, manifests (K8s/Cloud Run), IaC modules, security policies.  
**Anti-patterns:** snowflake servers; secrets in repos; tight coupling to proprietary services.  
**Templates:** ADR, threat model (STRIDE/LINDDUN).

---

## 8) Block 5 — Integration & Decision Loop
**Goal:** Land business value into real workflows — with measurable feedback.

**Checklist**
- [ ] API contracts (OpenAPI), idempotency, versioning.  
- [ ] Integration points (events vs APIs), sagas & compensations.  
- [ ] Decision UX (recommendation, explanation, human overrides).  
- [ ] Telemetry of usage & feedback loops (labeling, human-in-the-loop).  
- [ ] Online measurement: experimentation/A-B, guardrails, kill-switch.  
- [ ] Feature flag management.

**Deliverables:** OpenAPI contract, BPMN/sequence diagrams, effectiveness dashboards, support playbooks.  
**Anti-patterns:** unused models; opaque UX; no decision lift measurement.  
**Templates:** *Decision Loop Map*, *UX explainability patterns*.

---

## 9) Block 6 — MLOps & Operations
**Goal:** Automate and secure the full lifecycle.

**Checklist**
- [ ] CI/CD/CT: data & model lint/tests, reproducible builds, registry push, canary deploy.  
- [ ] Model Registry & Feature Store; full lineage.  
- [ ] Retraining triggers (drift, schedule, business).  
- [ ] Rollback/post-deploy verification policies.  
- [ ] Runbooks + SRE on-call + error budgets.  
- [ ] Seed management, determinism & reproducibility.

**Deliverables:** pipelines (DAGs-as-code), retraining policies, model release notes, runbooks.  
**Anti-patterns:** jupyter-only; mutable infra; no staging.  
**Templates:** pipeline YAML, release checklist, incident template.

---

## 10) Block 7 — Monitoring & Governance (technical)
**Goal:** Maintain reliability, security, and traceability over time.

**Checklist**
- [ ] Technical (latency, error rate, throughput) & business metrics (revenue, conversion).  
- [ ] Drift: data, concept, performance decay; alarms & thresholds.  
- [ ] Audit: who-did-what-when; versions of data/model/code.  
- [ ] Runtime security: abuse detection, prompt injection & model abuse (for GenAI).  
- [ ] Data retention & right-to-be-forgotten.  
- [ ] Periodic stakeholder reports.

**Deliverables:** dashboards, SLIs/SLOs, drift reports, audit logs.  
**Anti-patterns:** “no news is good news”; noisy alerts; missing post-mortems.  
**Templates:** SLO board, drift report, minimal audit trail.

---

## 11) Block 8 — Ethics & Responsibility (social)
**Goal:** Responsible design & deployment.

**Checklist**
- [ ] Identify risks (bias, exclusion, security).  
- [ ] Bias & stress testing by subgroup.  
- [ ] Explainability suited to context (user, auditor, regulator).  
- [ ] Governance: committees, AI red teaming, complaint channels.  
- [ ] Regulatory compliance (EU AI Act mapping), processing records.  
- [ ] Human-in-the-loop & automation limits.

**Deliverables:** *Ethics Review*, risk matrix, mitigation plan, user documentation.  
**Anti-patterns:** ethics-washing; paper-only reviews; ignoring indirect impact.  
**Templates:** *Risk & Harm Canvas*, *AI Red Team Plan*, *EU AI Act checklist*.

---

## 12) Block 9 — Efficiency & Sustainability (FinOps/GreenOps)
**Goal:** Maximize value per € / W / ms.

**Checklist**
- [ ] Budget per environment; cost tags.  
- [ ] Right-sizing (incl. GPUs), spot/committed use.  
- [ ] Inference optimization (quantization, batching, caching, distillation).  
- [ ] TCO/ROI and unit economics per use case.  
- [ ] Carbon footprint (estimation, tracking, reporting) & green design.  
- [ ] Technical debt: refactor & sunset plan.

**Deliverables:** TCO/ROI report, optimization plan, emissions dashboard.  
**Anti-patterns:** chronic overprovisioning, GPU hoarding, unnecessary latency.  
**Templates:** *Cost Review*, *Green Scorecard*.

---

## 13) Gate Reviews & Quality Checkouts

- **Gate 0 — Discovery:** problem, KPIs, main risks, go/no-go.  
- **Gate 1 — Design:** architecture, available data, evaluation plan, security baseline.  
- **Gate 2 — Build:** test coverage, offline results, readiness review.  
- **Gate 3 — Controlled launch:** canary/flag, SLOs, runbooks, rollback.  
- **Gate 4 — Stable operation:** drift under control, adoption, early ROI.  
- **Gate X — Retirement/redesign:** sunset criteria or new major version.

**Cross-cutting verification list (excerpt)**
- [ ] Updated ADRs  
- [ ] Published Model/Data Cards  
- [ ] Critical risks mitigated  
- [ ] Security/testing evidence  
- [ ] Communication/support plan

---

## 14) Practical Annexes

**A. Included Templates (summary)**  
- *Business Case Canvas*, *Impact Map*  
- *Data Contract* (JSON Schema/Avro), *Data Quality Matrix*  
- *Model Card* (ML/GenAI), *Prompt Registry*  
- *Threat Model* (STRIDE/LINDDUN)  
- *Decision Loop Map* (BPMN/Sequence)  
- *Pipeline YAML* (CI/CD/CT), *Release Checklist*  
- *Incident Post-mortem*  
- *EU AI Act Quick Map*  
- *Cost Review* & *Green Scorecard*

**B. Glossary (minimum)**  
- **RAG:** Retrieval-Augmented Generation.  
- **Concept Drift:** change in X→Y relationship.  
- **LLMOps:** operational practices for LLMs (prompts, evaluation, guardrails, cost).  
- **DPIA:** Data Protection Impact Assessment.

**C. Useful References (non-exhaustive)**  
- CRISP-ML(Q), ISO/IEC 42010 (architecture), 23894 (AI risk management), 27001/27018 (security/privacy), 5259 (data governance), NIST AI RMF, EU AI Act (risk mapping), MLOps/SRE best practices.

---

> **Note for next iteration:** for a concrete use case, we’ll instantiate these templates with real examples (KPIs, data contracts, prompt policies, SLOs) and attach corresponding C4 & IaC diagrams.

---

*Based on “AI Architecture Canvas – Project Edition (v1.0)” by Francisco López-Lira (flopezlira@gmail.com), licensed under CC BY-NC-SA 4.0.*


