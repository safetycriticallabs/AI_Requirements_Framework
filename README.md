# AI Requirements Framework for Safety-Critical Systems

> Requirements and Verification Standards for Artificial Intelligence in Safety-Critical Applications

**Issuing Authority:** Safety Critical Labs | AI Certification Authority
**Version:** 3.0 | May 2026
**Status:** [![DOI]([https://zenodo.org/badge/DOI/10.5281/zenodo.19024421.svg)](https://doi.org/10.5281/zenodo.19024421](https://doi.org/10.5281/zenodo.20060591))

> The DOI above points to the most recent deposited version on Zenodo. Each Zenodo release receives its own version DOI; the Concept DOI above always resolves to the latest version. Update this badge when the v3.0 deposit is minted.

---

## Overview

This framework establishes the AI-specific requirements and verifications against which Safety Critical Labs conducts certification assessments for systems incorporating artificial intelligence or machine learning capabilities in safety-critical applications.

Traditional software assurance assumes deterministic, logic-based systems with stable post-deployment behavior. AI and ML systems challenge this paradigm through probabilistic outputs, emergent behavior from training data, and potential performance degradation over time. This framework defines requirements and verification methods designed specifically for data-driven systems.

The framework is organized into two tiers. Section 2 contains ten algorithm-agnostic requirement sets (AI-1 through AI-10) that apply across all AI/ML systems regardless of technique. Section 3 contains three architecture- and paradigm-specific requirement sets (AI-11 through AI-13) that apply when systems use multi-model architectures, neural networks, or continuous learning. The framework applies across aerospace, aviation, automotive, medical, and other safety-critical domains.

---

## What's New in v3.0

- **Major structural revision.** The framework has been reorganized into a two-tier requirement structure. Section 2 retains the ten algorithm-agnostic requirement sets. New Section 3 (**Architecture and Paradigm Requirements**) consolidates normative content for architecture- and paradigm-specific concerns, lifted from prior Section 4.2/4.3/4.4 implementation guidance.
- **AI-11: Multi-Model Systems Requirements.** New requirement set covering multi-model architecture documentation, cascading failure mitigation, ensemble coordination, combined-confidence representation, and multi-model audit trail for systems composed of two or more AI models.
- **AI-12: Neural Network Requirements.** New requirement set addressing neural-network-specific concerns: architecture documentation, confidence calibration, explainability methods, training integrity, OOD detection extensions, adversarial vulnerability mitigation, generative-model hallucination constraints, and deployment-format validation under transformations such as quantization and framework conversion.
- **AI-13: Continuous Learning and Adaptation Requirements.** New requirement set for systems that update parameters during operation: continuous learning permission criteria, runtime learning controls, learning data validation, catastrophic forgetting mitigation, learning validation, rollback procedures, ODD evolvability declaration, and continuous learning audit trail.
- **Section renumbering.** Prior Section 3 (Verification) is now Section 4. Prior Section 4 (Implementation Guidance) is now Section 5 (**Implementation Patterns**). The renumbering separates normative architecture/paradigm requirements from informative implementation guidance and resolves prior lexicon contradictions.
- **§1.3.3 Verification Status of Cited References.** New subsection records the verification disposition of cited references and explicitly identifies cited standards that were not available for clause-level verification at the time of release.
- **Domain Standards citations verified at clause level.** Domain Standards citations across all requirement sets have been verified at clause level against source documents where available. Wrong section references have been corrected; outdated dates updated; and held citations explicitly annotated.
- **Expanded standards traceability.** Glossary terms and citations now traceable to ISO/IEC 22989, 5338, 23053, 23894, 25059, 27001+AMD 1, 27701, 42001, ISO/IEC TR 24027, ISO/IEC TS 6254, NIST AI 100-1, NIST AI 100-2e2023, NIST AI 600-1, NIST SP 1270, NIST SP 800-53 Rev. 5, and NIST SP 800-218A, plus domain-specific standards listed below.

### Carried forward from v2.1

- **AI-1 scope expansion.** AI-1 is **Operational and Data Foundations**, incorporating the Operational Design Domain (ODD) concept introduced in v2.1 (Section 1.2.3) alongside the data-partitioning and provenance requirements.
- **AI-10: Privacy and Data Protection.** Personal-data identification and minimization, lawful basis and consent, data-subject rights, privacy-enhancing techniques, cross-border transfer controls, privacy impact assessment, and privacy-compliance audit trail.
- **AI-8.5: Public Disclosure Support.** External model cards, EU AI Act Article 13 user information, federal AI inventory entries, and EU AI Act Article 71 public database registration.
- **AI-9 human factors expansion.** AI-9.7 Operator Qualification, AI-9.8 Workload Management, AI-9.9 Training Program Requirements.
- **Classification rename.** "Mission Support" → **Operational Support**.
- **Domain Standards Citation Convention (§1.3.1).** Each parent [R.AI-X] statement carries Applicable Domain Standards citations.

---

## AI System Classification

Systems are classified based on their impact on safety and operations, which determines applicable requirements and tailoring authority:

| Classification | Description | Applicable Requirements |
|---|---|---|
| **Safety-Critical AI** | AI outputs directly affect human safety or system survivability | AI-1 through AI-10 (no tailoring without Safety Review Board approval); AI-11/12/13 apply when those architectures or paradigms are used |
| **Mission-Critical AI** | AI outputs affect operational success but not human safety | AI-1 through AI-10 (tailoring permitted with documented rationale); AI-11/12/13 apply when relevant |
| **Operational Support AI** | AI supports operations but does not drive critical decisions | AI-1 through AI-5 minimum; AI-6 through AI-10 as tailored; AI-11/12/13 applied when relevant |

---

## Requirement Sets

The framework defines thirteen AI-specific requirement sets organized into two tiers.

### Section 2 — Algorithm-Agnostic Requirements

Apply to all AI/ML systems regardless of architecture or technique.

| Req Set | Title | Gap Addressed |
|---|---|---|
| **AI-1** | Operational and Data Foundations | Operational Design Domain definition; training data integrity, separation, and traceability |
| **AI-2** | Addressing AI Bias | Bias and fairness issues across training, monitoring, and response |
| **AI-3** | ML Test Coverage | No traditional test coverage equivalent for trained models |
| **AI-4** | Continuous Validation | Static-after-deployment assumptions; drift and performance degradation |
| **AI-5** | Hallucination Prevention | Unpredictable and fabricated outputs |
| **AI-6** | Out-of-Distribution Detection | Vulnerability to OOD inputs not represented in training |
| **AI-7** | Adversarial Robustness | Vulnerability to data poisoning, adversarial inputs, model extraction, and supply-chain attacks |
| **AI-8** | Explainability | Black-box decision-making; transparency for operators, regulators, and the public |
| **AI-9** | Human-AI Teaming | Operators cannot verify AI reasoning; qualification, workload, and training gaps |
| **AI-10** | Privacy and Data Protection | Personal-data handling, consent, subject rights, and cross-border transfer |

### Section 3 — Architecture and Paradigm Requirements

Apply when the corresponding architecture or paradigm is used.

| Req Set | Title | Applies When |
|---|---|---|
| **AI-11** | Multi-Model Systems Requirements | System composes two or more AI models (cascades, ensembles, retrieval-augmented generation, etc.) |
| **AI-12** | Neural Network Requirements | System uses neural-network architectures, including deep learning and generative models |
| **AI-13** | Continuous Learning and Adaptation Requirements | System updates model parameters during operation (incremental, continual, or lifelong learning) |

---

## Verification

Verification uses standard IEEE 1012 methods tailored for AI and ML systems:

| Method | AI Application |
|---|---|
| **Inspection** | Dataset documentation, provenance records, log schemas, disclosure artifacts |
| **Analysis** | Bias risk assessment, coverage analysis, distribution characterization, workload analysis |
| **Demonstration** | Operator comprehension, human-AI interaction evaluation |
| **Test** | Drift detection, OOD detection, hallucination detection, adversarial-input resilience |

Each requirement includes co-located verification criteria and success criteria. A verification matrix in Section 4.2 provides full traceability from each [R.AI-X.Y] to its verification method and evidence.

---

## Document Structure

```
Section 1: Introduction
  1.1  Purpose
  1.2  Scope and Applicability
       1.2.1  Defining AI
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
  2.1   AI-1: Operational and Data Foundations (incl. ODD)
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
  4.1  Verification Methods
  4.2  Verification Matrix Summary
  4.3  Deployment Format Validation Notes

Section 5: Implementation Patterns
  5.1  Threshold Selection Guidance
  5.2  AI-Specific Hazard Analysis Integration
  5.3  Human-AI Teaming Implementation Guidance
  5.4  Privacy and Data Protection Implementation Guidance

Appendix A: Glossary (aligned with ISO/IEC 22989:2022, ISO/IEC 5338:2023)
Appendix B: AI Classification Checklist
Appendix C: Verification Evidence Templates
Appendix D: Risk Score Methodology
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
| IEEE 1012 | System, Software, and Hardware Verification and Validation |

Domain-specific:

| Domain | Document | Title |
|---|---|---|
| Aviation | RTCA DO-178C / DO-326A / DO-330 / DO-355 / DO-356A | Airborne software, security process, tool qualification, information security |
| Aviation | EUROCAE ED-324 / SAE ARP6983 | AI/ML aviation development and certification (Q1 2026) |
| Aviation | FAA AI Safety Roadmap | FAA aviation AI safety vision |
| Aviation | 14 CFR 25.1302; 14 CFR 121 Subparts N, Y | Flight crew interfaces; qualification and training |
| Automotive | ISO 26262; ISO 21448 (SOTIF); ISO/SAE 21434 | Functional safety, safety of the intended function, cybersecurity |
| Automotive | ISO 34503 | Operational design domain taxonomy for automated driving |
| Automotive | SAE J3016; UNECE WP.29 R157; NHTSA AV 4.0 | Driving automation taxonomy; ALKS regulation; voluntary safety assessment |
| Medical | IEC 62304; ISO 14971 | Medical software lifecycle; risk management |
| Medical | FDA AI-Enabled Device Software Functions | Lifecycle management and marketing submission recommendations (Draft, 2025) |
| Medical | FDA Predetermined Change Control Plan (PCCP) | Marketing submission recommendations for AI-enabled device PCCP (2024) |
| Medical | FDA Clinical Decision Support Software | CDS guidance (2026 update) |
| Medical | FDA Premarket / Postmarket Cybersecurity | Cybersecurity in medical devices (2023 / 2016) |
| Medical | FDA Transparency for ML-Enabled Medical Devices | Joint FDA / Health Canada / MHRA Guiding Principles (2024) |
| Regulatory | EU AI Act (Reg. 2024/1689) | High-risk AI obligations (Articles 9, 10, 13, 14, 15, 17, 26, 50, 71, 72) |
| Regulatory | GDPR (Reg. 2016/679); HIPAA; CCPA/CPRA | Personal data protection regimes |

A full citation list with section-level references appears throughout the framework as **Applicable Domain Standards** blocks under each requirement. See §1.3.3 for the verification status of cited references.

---

## Getting Started

1. **Determine applicability** — Use the criteria in Section 1.2.1 and the checklist in Appendix B to identify whether your system incorporates AI or ML
2. **Classify your AI system** — Safety-Critical, Mission-Critical, or Operational Support (Section 1.2.2)
3. **Define your Operational Design Domain** — Document ODD per Section 1.2.3; this feeds AI-1.0 and sub-requirement scoping
4. **Identify applicable requirements** — Section 2 (AI-1 through AI-10) plus any Section 3 requirements (AI-11/12/13) that apply based on system architecture and paradigm
5. **Apply tailoring if needed** — Document rationale per Section 1.2.6
6. **Define thresholds** — Use Section 5.1 guidance to establish project-specific values
7. **Execute verification** — Use the verification matrix (Section 4.2) and evidence templates in Appendix C

---

## Citation

If you use this framework in research, certification work, or derivative publications, please cite:

> Williams, K., & Safety Critical Labs AI Certification Authority. (2026). *AI Requirements Framework for Safety-Critical Systems* (Version 3.0) [Standard]. Zenodo. https://doi.org/10.5281/zenodo.19024421

---

## License

Creative Commons Attribution-Share Alike 4.0 International (CC BY-SA 4.0)

---

## Contact

kevin.williams@safetycriticallabs.com
[safetycriticallabs.com](https://safetycriticallabs.com)
