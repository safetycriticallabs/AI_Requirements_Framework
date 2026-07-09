# AI Requirements Framework for Safety-Critical Systems

> Requirements and Verification Standards for Artificial Intelligence in Safety-Critical Applications

**Issuing Authority:** Safety Critical Labs | AI Certification Authority
**Version:** 3.4 | July 2026
**Status:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19024420.svg)](https://doi.org/10.5281/zenodo.19024420)

> The DOI above is the Concept DOI and always resolves to the most recent deposited version on Zenodo. Each release receives its own version DOI; cite the Concept DOI unless you need to pin a specific version.

---

## Overview

This framework establishes the AI-specific requirements and verifications against which Safety Critical Labs conducts certification assessments for systems incorporating artificial intelligence or machine learning capabilities in safety-critical applications.

Traditional software assurance assumes deterministic, logic-based systems with stable post-deployment behavior. AI and ML systems challenge this paradigm through probabilistic outputs, emergent behavior from training data, and potential performance degradation over time. This framework defines requirements and verification methods designed specifically for data-driven systems.

The framework is organized into two tiers. Section 2 contains ten algorithm-agnostic requirement sets (AI-1 through AI-10) that apply across all AI/ML systems regardless of technique. Section 3 contains three architecture- and paradigm-specific requirement sets (AI-11 through AI-13) that apply when systems use multi-model architectures, neural networks, or continuous learning. Requirements are defined by the failures they prevent, carry co-located verifications with success criteria, and trace to a verification matrix with defined cadence and classification-scaled verifier independence. The framework applies across aerospace, aviation, automotive, medical, and other safety-critical domains.

---

## What's New in v3.4

- **Applicability gate redesigned (§1.2.1, Appendix B.1).** Learned behavior (behavior induced from data through training, fine-tuning, continuous learning, or retrieval augmentation) is now the anchor criterion and is necessary for applicability; probabilistic outputs and potential drift are supporting indicators that refine verification emphasis. Decision impact moved to classification (§1.2.2), where it does its proper work. New **Table 1-2b** gives negative criteria with worked examples of what is *not* AI for framework purposes (deterministic control laws, Kalman filters and classical estimators, fixed rule-based systems, statistical process control, lookup tables), and Appendix B.1 is now a decision sequence with self-contained question numbering.
- **AI-1.9: AI Hazard Analysis Integration.** New normative requirement: the hazard analysis the host standard already mandates (FMEA, FMECA, FTA, STPA, or PRA) must include the AI system, address the AI-specific failure mode categories in §5.2.2, and trace identified hazards to the requirements and thresholds that mitigate them. Hazard analysis outputs now inform classification and threshold selection.
- **AI-1.10: Retrieval Corpus Controls.** New normative requirement for retrieval-augmented systems: corpus provenance (per AI-1.3), content screening before admission (per AI-1.5), integrity protection and change control for corpus updates, and protection against corpus poisoning and indirect prompt injection (per AI-7.1/AI-7.2). Documented as Not Applicable where retrieval augmentation is not used.
- **§4.5: Verification Independence.** Verifier independence now scales with classification: Safety-Critical requires non-developer verification with organizational separation; Mission-Critical requires non-developer verification; Operational Support permits self-verification with independent Software Assurance review.
- **Classification hardened (§1.2.2).** Classification is anchored to the severity of the worst credible consequence of AI malfunction (drawing on AI-1.9); the more severe classification prevails on conflict, and the determination is approved at the same authority level as the ODD declaration (Table 1-4).
- **Threshold adequacy (§1.5).** Each threshold value must be documented with its derivation basis and justified against the declared ODD, classification, and hazard analysis; adequacy is adjudicated during certification assessment per the SCL assessment methodology.
- **Prompt injection coverage (AI-7.2).** Adversarial input protection now explicitly covers direct and indirect prompt injection for generative and retrieval-augmented systems, with OWASP LLM Top 10 and MITRE ATLAS citations.
- **Statistical ML coverage (AI-12.2, AI-12.4).** Confidence calibration and training integrity now additionally apply to non-neural statistical ML models (gradient-boosted trees, random forests, support vector machines), which exhibit the same miscalibration and overfitting failure modes.
- **Consistency and correctness pass.** Bias requirements reworded to what is actually verified (AI-2.1 Bias-Bounded Baseline Performance, AI-2.2 Bias-Managed Training Data); AI-2.3 scope corrected to include Safety-Critical decisions; defined-fallback response paths added to AI-2.11 and AI-5.3 for approved-autonomy and disconnected operations; the Demonstration method is now assigned in the verification matrix (AI-8.2, AI-9.3); logging and calibration verification cadences aligned; miswired cross-references corrected; Table 1-7 gains a Retirement lifecycle phase; UL 4600 added to references; AI-1.5 through AI-1.8 gain explicit Not Applicable provisions; ODD attribute coverage in AI-1.0 now scales with classification per Table 1-4.

### Earlier releases

v3.1 through v3.3 were editorial and consistency revisions (uniform verification format across AI-1 through AI-13, corrected verification-method definitions, IEEE 1012-2024 citation). v3.0 was the major structural revision that introduced the two-tier structure and the Section 3 Architecture and Paradigm Requirements (AI-11 Multi-Model Systems, AI-12 Neural Networks, AI-13 Continuous Learning and Adaptation), renumbered Verification to Section 4 and Implementation Patterns to Section 5, and added the §1.3.2 Source Traceability Typology and §1.3.3 Verification Status of Cited References. The full revision history appears at the end of the framework document.

---

## AI System Classification

Systems are classified based on their impact on safety and operations, which determines applicable requirements and tailoring authority. Classification is anchored to the severity of the worst credible consequence of AI system malfunction, informed by the hazard analysis (AI-1.9), and is approved at the authority level defined in Table 1-4.

| Classification | Description | Applicable Requirements |
|---|---|---|
| **Safety-Critical AI** | AI outputs directly affect human safety or system survivability | All AI-1 through AI-10 (no tailoring without Project Safety Review Board approval); plus AI-11 if multi-model, AI-12 if neural network, AI-13 if continuous learning |
| **Mission-Critical AI** | AI outputs affect operational success but not human safety | AI-1 through AI-6, AI-8, AI-9, AI-10 (tailoring permitted with Chief Engineer approval); AI-7 tailored; plus AI-11 / AI-12 / AI-13 conditionally per system design |
| **Operational Support AI** | AI supports operations but does not drive critical decisions | AI-1 through AI-6 and AI-10 minimum; AI-7, AI-8, AI-9 as tailored; plus AI-11 / AI-12 / AI-13 conditionally per system design |

> AI-12.2 (Confidence Calibration) and AI-12.4 (Training Integrity) additionally apply to systems built on non-neural statistical ML models.

---

## Requirement Sets

The framework defines thirteen AI-specific requirement sets organized into two tiers.

### Section 2 — Algorithm-Agnostic Requirements

Apply to all AI/ML systems regardless of architecture or technique.

| Req Set | Title | Gap Addressed |
|---|---|---|
| **AI-1** | Operational and Data Foundations | Operational Design Domain definition; training data integrity, separation, and traceability; hazard analysis integration; retrieval corpus controls |
| **AI-2** | Addressing AI Bias | Bias and fairness issues across training, monitoring, and response |
| **AI-3** | ML Test Coverage | No traditional test coverage equivalent for trained models |
| **AI-4** | Continuous Validation | Static-after-deployment assumptions; drift and performance degradation; operational validation without ground truth; deployment format validation |
| **AI-5** | Hallucination Prevention | Unpredictable and fabricated outputs |
| **AI-6** | Out-of-Distribution Detection | Vulnerability to OOD inputs not represented in training |
| **AI-7** | Adversarial Robustness | Vulnerability to data poisoning, adversarial inputs, prompt injection, model extraction, and supply-chain attacks |
| **AI-8** | Explainability | Black-box decision-making; transparency for operators, regulators, and the public |
| **AI-9** | Human-AI Teaming | Operators cannot verify AI reasoning; qualification, workload, and training gaps |
| **AI-10** | Privacy and Data Protection | Personal-data handling, consent, subject rights, and cross-border transfer |

### Section 3 — Architecture and Paradigm Requirements

Apply when the corresponding architecture or paradigm is used.

| Req Set | Title | Applies When |
|---|---|---|
| **AI-11** | Multi-Model Systems Requirements | System composes two or more AI models (cascades, ensembles, coordinated architectures) |
| **AI-12** | Neural Network Requirements | System uses neural-network architectures, including deep learning and generative models (AI-12.2 and AI-12.4 also apply to other statistical ML models) |
| **AI-13** | Continuous Learning and Adaptation Requirements | System updates model parameters during operation (incremental, continual, or lifelong learning) |

---

## Verification

Verification uses standard IEEE 1012 methods tailored for AI and ML systems:

| Method | AI Application |
|---|---|
| **Inspection** | Dataset documentation, provenance records, log schemas, disclosure artifacts |
| **Analysis** | Bias risk assessment, coverage analysis, distribution characterization, hazard traceability |
| **Demonstration** | Operator comprehension, human-AI interaction evaluation, trust calibration |
| **Test** | Drift detection, OOD detection, hallucination detection, adversarial-input resilience, deployment-format equivalence |

Each requirement includes co-located verification criteria and success criteria. The verification matrix in Section 4.2 provides full traceability from each [R.AI-X.Y] to its verification method, evidence artifact, and cadence (one-time, periodic, or continuous). Section 4.4 consolidates the continuous and periodic verification obligations for deployed systems, and Section 4.5 establishes verifier independence scaled by classification.

---

## Document Structure

```
Section 1: Introduction
  1.1  Purpose
  1.2  Scope and Applicability
       1.2.1  Defining AI (anchor criterion, supporting indicators, negative criteria)
       1.2.2  AI System Classification
       1.2.3  Operational Design Domain
       1.2.4  Relationship to Traditional Software Standards
              1.2.4.1  Gap Analysis
              1.2.4.2  Gap-to-Requirement Mapping
       1.2.5  Integration with Software Lifecycle
       1.2.6  Tailoring Guidance
  1.3  Normative References
       1.3.1  Domain Standards Citation Convention
       1.3.2  Source Traceability Typology
       1.3.3  Verification Status of Cited References
  1.4  Verb Application and Lexicon
  1.5  Threshold Category Definitions

Section 2: Requirements (Algorithm-Agnostic)
  2.1   AI-1: Operational and Data Foundations (incl. ODD, hazard analysis, retrieval corpora)
  2.2   AI-2: Addressing AI Bias
  2.3   AI-3: ML Test Coverage
  2.4   AI-4: Continuous Validation
  2.5   AI-5: Hallucination Prevention
  2.6   AI-6: Out-of-Distribution Detection
  2.7   AI-7: Adversarial Robustness
  2.8   AI-8: Explainability
  2.9   AI-9: Human-AI Teaming
  2.10  AI-10: Privacy and Data Protection

Section 3: Architecture and Paradigm Requirements
  3.1  AI-11: Multi-Model Systems Requirements
  3.2  AI-12: Neural Network Requirements
  3.3  AI-13: Continuous Learning and Adaptation Requirements

Section 4: Verification
  4.0  Overview
  4.1  Verification Methods
  4.2  Verification Matrix Summary
  4.3  Deployment Format Validation
  4.4  Continuous and Periodic Verification
  4.5  Verification Independence

Section 5: Implementation Patterns
  5.1  Threshold Selection Guidance
  5.2  AI-Specific Hazard Analysis Integration
  5.3  Human-AI Teaming Implementation Guidance
  5.4  Privacy and Data Protection Implementation Guidance

Appendix A: Glossary (aligned with ISO/IEC 22989:2022, ISO/IEC 5338:2023)
Appendix B: AI Classification Checklist
Appendix C: Verification Evidence Templates
Appendix D: Risk Score Methodology

Document Revision History
```

---

## Normative and Applicable Domain References

Cross-domain and general:

| Document | Title |
|---|---|
| ISO/IEC 22989:2022 | Artificial Intelligence — Concepts and Terminology |
| ISO/IEC 23053:2022 | Framework for AI Systems Using Machine Learning |
| ISO/IEC 23894:2023 | AI — Guidance on Risk Management |
| ISO/IEC 25059:2023 | SQuaRE — Quality Model for AI Systems |
| ISO/IEC 5338:2023 | AI System Lifecycle Processes |
| ISO/IEC 42001:2023 | AI Management System Requirements |
| ISO/IEC 27001:2022 + AMD 1 | Information Security Management |
| ISO/IEC 27701 | Privacy Information Management |
| ISO/IEC TR 24027:2021 | Bias in AI Systems and AI-Aided Decision Making |
| ISO/IEC TS 6254 | Objectives and Approaches for Explainability and Interpretability of ML Models and AI Systems |
| NIST AI RMF 1.0 (NIST AI 100-1) | AI Risk Management Framework |
| NIST AI 100-2e2023 | Adversarial Machine Learning Taxonomy |
| NIST AI 600-1 | AI RMF Generative AI Profile |
| NIST SP 1270 | Towards a Standard for Identifying and Managing Bias in AI |
| NIST SP 800-53 Rev. 5 | Security and Privacy Controls |
| NIST SP 800-218A | Secure Software Development Practices for Generative AI |
| IEEE 1012-2024 | System, Software, and Hardware Verification and Validation |

Domain-specific:

| Domain | Document | Title |
|---|---|---|
| Aviation | RTCA DO-178C / DO-326A / DO-330 / DO-355 / DO-356A | Airborne software, security process, tool qualification, information security |
| Aviation | EUROCAE ED-324 / SAE ARP6983 | AI/ML aviation development and certification (Q1 2026) |
| Aviation | SAE ARP4761 | Safety assessment process for civil airborne systems |
| Aviation | FAA AI Safety Roadmap | FAA aviation AI safety vision |
| Aviation | 14 CFR 25.1302; 14 CFR 121 Subparts N, Y | Flight crew interfaces; qualification and training |
| Automotive | ISO 26262; ISO 21448 (SOTIF); ISO/SAE 21434 | Functional safety, safety of the intended function, cybersecurity |
| Automotive | ISO 34503 | Operational design domain taxonomy for automated driving |
| Automotive | SAE J3016; UNECE WP.29 R157; NHTSA AV 4.0 | Driving automation taxonomy; ALKS regulation; voluntary safety assessment |
| Autonomy | UL 4600 | Standard for Safety for the Evaluation of Autonomous Products |
| Medical | IEC 62304; ISO 14971 | Medical software lifecycle; risk management |
| Medical | FDA AI-Enabled Device Software Functions | Lifecycle management and marketing submission recommendations (Draft, 2025) |
| Medical | FDA Predetermined Change Control Plan (PCCP) | Marketing submission recommendations for AI-enabled device PCCP (2024) |
| Medical | FDA Clinical Decision Support Software | CDS guidance (2026 update) |
| Medical | FDA Premarket / Postmarket Cybersecurity | Cybersecurity in medical devices (2023 / 2016) |
| Medical | FDA Transparency for ML-Enabled Medical Devices | Joint FDA / Health Canada / MHRA Guiding Principles (2024) |
| Defense / Aerospace | MIL-STD-882E; NASA-STD-8739.8 | System safety; software assurance and safety analysis |
| Regulatory | EU AI Act (Reg. 2024/1689) | High-risk AI obligations (Articles 9, 10, 13, 14, 15, 17, 26, 50, 71, 72) |
| Regulatory | GDPR (Reg. 2016/679); HIPAA; CCPA/CPRA | Personal data protection regimes |

A full citation list with section-level references appears throughout the framework as **Applicable Domain Standards** blocks under each requirement. See §1.3.3 for the verification status of cited references.

---

## Getting Started

1. **Determine applicability** — Apply the anchor criterion (learned behavior) and supporting indicators in Section 1.2.1, use Table 1-2b to rule out non-AI systems, and record the determination via Appendix B.1 and C.1
2. **Classify your AI system** — Safety-Critical, Mission-Critical, or Operational Support, anchored to worst-credible-consequence severity and approved per Table 1-4 (Section 1.2.2)
3. **Define your Operational Design Domain** — Document ODD per Section 1.2.3; this feeds AI-1.0 and sub-requirement scoping
4. **Integrate AI failure modes into your hazard analysis** — Per AI-1.9, using the Section 5.2 failure mode categories and guidance
5. **Identify applicable requirements** — Section 2 (AI-1 through AI-10) plus any Section 3 requirements (AI-11/12/13) that apply based on system architecture and paradigm
6. **Apply tailoring if needed** — Document rationale per Section 1.2.6
7. **Define thresholds** — Use Section 5.1 guidance to establish project-specific values, documented and justified per Section 1.5
8. **Execute verification** — Use the verification matrix (Section 4.2), the cadence obligations (Section 4.4), the independence requirements (Section 4.5), and the evidence templates in Appendix C

---

## Citation

If you use this framework in research, certification work, or derivative publications, please cite:

> Williams, K., & Safety Critical Labs AI Certification Authority. (2026). *AI Requirements Framework for Safety-Critical Systems* (Version 3.4) [Standard]. Zenodo. https://doi.org/10.5281/zenodo.19024420

---

## License

Creative Commons Attribution-Share Alike 4.0 International (CC BY-SA 4.0)

---

## Contact

kevin.williams@safetycriticallabs.com
[safetycriticallabs.com](https://safetycriticallabs.com)
