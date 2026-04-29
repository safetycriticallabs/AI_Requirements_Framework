# AI Requirements Framework for Safety-Critical Systems

> Requirements and Verification Standards for Artificial Intelligence in Safety-Critical Applications

**Issuing Authority:** Safety Critical Labs | AI Certification Authority
**Version:** 2.1.2 | April 2026
**Status:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19024421.svg)](https://doi.org/10.5281/zenodo.19024421)

> The DOI above points to the most recent deposited version on Zenodo. Each Zenodo release receives its own version DOI; the Concept DOI above always resolves to the latest version.

---

## Overview

This framework establishes the AI-specific requirements and verifications against which Safety Critical Labs conducts certification assessments for systems incorporating artificial intelligence or machine learning capabilities in safety-critical applications.

Traditional software assurance assumes deterministic, logic-based systems with stable post-deployment behavior. AI and ML systems challenge this paradigm through probabilistic outputs, emergent behavior from training data, and potential performance degradation over time. This framework defines requirements and verification methods designed specifically for data-driven systems.

The framework is domain-agnostic and algorithm-agnostic. It applies across aerospace, aviation, automotive, medical, and other safety-critical domains without prescribing specific implementation approaches.

---

## What's New in v2.1.1

- **AI-1 scope expansion.** The former "Data Partitioning" requirement set is now **AI-1: Operational and Data Foundations**, incorporating the Operational Design Domain (ODD) concept introduced in v2.1 (Section 1.2.3) alongside the original data-partitioning and provenance requirements.
- **AI-10: Privacy and Data Protection.** A new requirement set covering personal-data identification and minimization, lawful basis and consent, data-subject rights, privacy-enhancing techniques, cross-border transfer controls, privacy impact assessment, and privacy-compliance audit trail.
- **AI-8.5: Public Disclosure Support** (Gap 10). Optional, classification-dependent sub-requirement for external model cards, EU AI Act Article 13 user information, EO 14110 and OMB M-24-10 federal AI inventory entries, and EU AI Act Article 71 public database registration.
- **Gap 6 human factors expansion under AI-9.** Three new sub-requirements: AI-9.7 Operator Qualification, AI-9.8 Workload Management, AI-9.9 Training Program Requirements.
- **Classification rename.** "Mission Support" is now **Operational Support** throughout the framework to better describe systems that support operations without driving critical decisions.
- **Domain Standards Citation Convention (§1.3.1).** Each parent [R.AI-X] statement carries Applicable Domain Standards citations; sub-requirement-level citations are complete for AI-1.0 (ODD), AI-2.1, AI-7 (all six), AI-8.3, AI-8.5, AI-9.1, AI-9.7 through AI-9.9, and all of AI-10. Remaining sub-requirement citations are scheduled as a Phase 2 pass within v2.1.1.

---

## AI System Classification

Systems are classified based on their impact on safety and operations, which determines applicable requirements and tailoring authority:

| Classification | Description | Applicable Requirements |
|---|---|---|
| **Safety-Critical AI** | AI outputs directly affect human safety or system survivability | AI-1 through AI-10 (no tailoring without Safety Review Board approval) |
| **Mission-Critical AI** | AI outputs affect operational success but not human safety | AI-1 through AI-10 (tailoring permitted with documented rationale) |
| **Operational Support AI** | AI supports operations but does not drive critical decisions | AI-1 through AI-5 minimum; AI-6 through AI-10 as tailored |

---

## Requirement Sets

The framework defines ten AI-specific requirement sets, each addressing a gap between traditional software verification and AI and ML system behavior:

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

---

## Verification

Verification uses standard IEEE 1012 methods tailored for AI and ML systems:

| Method | AI Application |
|---|---|
| **Inspection** | Dataset documentation, provenance records, log schemas, disclosure artifacts |
| **Analysis** | Bias risk assessment, coverage analysis, distribution characterization, workload analysis |
| **Demonstration** | Operator comprehension, human-AI interaction evaluation |
| **Test** | Drift detection, OOD detection, hallucination detection, adversarial-input resilience |

Each requirement includes co-located verification criteria and success criteria. A verification matrix in Section 3.2 provides full traceability from each [R.AI-X.Y] to its verification method and evidence.

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
  1.4  Verb Application and Lexicon
  1.5  Threshold Category Definitions

Section 2: Requirements
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

Section 3: Verification
  3.1  Verification Methods
  3.2  Verification Matrix Summary
  3.3  Deployment Format Validation

Section 4: Implementation Guidance
  4.1  Threshold Selection Guidance
  4.2  Continuous Learning Requirements
  4.3  Multi-Model System Considerations
  4.4  Neural Network Considerations
  4.5  AI-Specific Hazard Analysis Integration

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
| ISO/IEC 23894:2023 | AI — Guidance on Risk Management |
| ISO/IEC 25059:2023 | SQuaRE — Quality Model for AI Systems |
| ISO/IEC 5338:2023 | AI System Lifecycle Processes |
| ISO/IEC 42001:2023 | AI Management System Requirements |
| ISO/IEC 27001:2022 / 27002:2022 | Information Security Management |
| NIST AI RMF 1.0 | AI Risk Management Framework |
| NIST SP 800-53 Rev. 5 | Security and Privacy Controls |
| IEEE 1012 | System, Software, and Hardware Verification and Validation |

Domain-specific:

| Domain | Document | Title |
|---|---|---|
| Aviation | RTCA DO-178C / DO-254 / DO-326A / DO-355 | Airborne software, hardware, and information security |
| Aviation | 14 CFR 25.1302; 14 CFR 121 Subpart Y | Flight crew interfaces; qualification and training |
| Automotive | ISO 26262; ISO 21448; ISO/SAE 21434 | Functional safety, SOTIF, cybersecurity |
| Automotive | SAE J3016; NHTSA AV 4.0 | Driving automation taxonomy; voluntary safety assessment |
| Medical | IEC 62304; ISO 14971; FDA CDS / GMLP / PCCP | Medical software lifecycle, risk management, AI guidance |
| Regulatory | EU AI Act (Reg. 2024/1689) | High-risk AI obligations (Articles 9, 10, 13, 14, 15, 26, 50, 71) |
| Regulatory | EO 14110; OMB M-24-10 | US federal AI governance and use-case inventory |

A full citation list with section-level references appears throughout the framework as **Applicable Domain Standards** blocks under each requirement.

---

## Getting Started

1. **Determine applicability** — Use the criteria in Section 1.2.1 and the checklist in Appendix B to identify whether your system incorporates AI or ML
2. **Classify your AI system** — Safety-Critical, Mission-Critical, or Operational Support (Section 1.2.2)
3. **Define your Operational Design Domain** — Document ODD per Section 1.2.3; this feeds AI-1.0 and sub-requirement scoping
4. **Identify applicable requirements** — Based on classification (Table 1-3)
5. **Apply tailoring if needed** — Document rationale per Section 1.2.6
6. **Define thresholds** — Use Section 4.1 guidance to establish project-specific values
7. **Execute verification** — Use the verification matrix (Section 3.2) and evidence templates in Appendix C

---

## Citation

If you use this framework in research, certification work, or derivative publications, please cite:

> Williams, K., & Safety Critical Labs AI Certification Authority. (2026). *AI Requirements Framework for Safety-Critical Systems* (Version 2.1.1) [Standard]. Zenodo. https://doi.org/10.5281/zenodo.19024421

---

## License

Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## Contact

kevin.williams@safetycriticallabs.com
[safetycriticallabs.com](https://safetycriticallabs.com)
