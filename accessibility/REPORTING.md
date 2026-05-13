# IAAP Accessibility Reporting Templates

This document contains the canonical, dual-document reporting templates for all accessibility audits. These templates are designed to meet IAAP professional standards and provide developer-ready remediation instructions.

---

## Document 1: Master Technical Remediation Report

Generate this report as the primary deliverable for developers. Findings must be grouped by UI Component and sorted strictly from **MINOR to BLOCKER**.

> [!IMPORTANT]
> **Audit Trail Mandate:** No finding related to Screen Reader validation or ARIA behavior is considered "confirmed" or "remediated" without a corresponding **NVDA Speech Log** entry attached as evidence.

````markdown
# Master Technical Remediation Report: [Product Name]

**Audit Date:** [Date]
**Target URL:** [URL]

---

## 🏛️ Component: [Component Name]

### [Issue Title]
- **Severity**: [MINOR | MODERATE | SERIOUS | BLOCKER]
- **Success Criteria**: [WCAG SC Link]
- **Affected Impairments**: [Visual | Motor | Cognitive | Hearing]
- **Observation**: [Detailed description of the finding found during the audit]
- **Suggested Remediation**: [Copy-pasteable technical fix and verification instructions]
- **DOM Evidence**:
  ```html
  [Exact snippet from the source code]
  ```

---
````

---

## Document 2: Accessibility Conformance Report (VPAT® 2.5)

A formal ACR adhering to IAAP professional standards, generated for **each audited URL**.

````markdown
# Accessibility Conformance Report (VPAT® 2.5): [Product Name]

**Audit Date:** [Date]
**Compliance Score:** [XX.XX]% (Calculated across 37 evaluated criteria: [X] Supports, [Y] Partially Supports, [Z] Does Not Support)

---

## 🏗️ Compliance Summary by Component

| Component | Status | Key Criteria Failed |
| :--- | :--- | :--- |
| [Component Name] | [Supports | Partially Supports | Does Not Support] | [WCAG SCs] |

---

## WCAG 2.1 & 2.2 Conformance Table

*Evaluated against the 37 Core Web Criteria Baseline.*

| Criteria | Conformance Level | Remarks and Explanations |
| :--- | :--- | :--- |
| [SC Number] | [Supports | Does Not Support] | [Finding + User Impact] |
````

---

### 📏 Scoring Rules
- **Denominator**: 37 by default.
- **Adjustment**: Increase to 42 if the page contains Forms, Auth, or complex interactions (as defined in SKILL.md).
- **Formula**: `((Supports * 1) + (Partially Supports * 0.5)) / Denominator * 100`
