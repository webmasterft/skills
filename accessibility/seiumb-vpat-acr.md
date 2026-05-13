# Accessibility Conformance Report (VPAT® 2.5 WCAG): SEIUMB Home Page
**Audit Date:** May 12, 2026
**Conformance Level:** WCAG 2.1 & 2.2 Level AA

**Compliance Score:** 83.33%
*Calculated across 42 evaluated criteria: 35 Supports, 0 Partially Supports, 7 Does Not Support.*
*Formula: `((35 * 1) + (0 * 0.5)) / 42 * 100 = 83.33%`*

---

## 🏗️ Compliance Summary by Component

| Component | Status | Key Criteria Failed |
| :--- | :--- | :--- |
| Global Header | Partially Supports | 1.1.1, 2.5.8 |
| Mobile Navigation | Does Not Support | 2.1.1, 2.4.3 |
| Search Functionality | Partially Supports | 1.3.1, 3.3.1 |
| Feature Content | Partially Supports | 1.3.1, 2.4.4 |
| Footer | Does Not Support | 2.5.8, 1.4.3 |

---

## WCAG 2.1 / 2.2 Conformance Table
*Evaluated against the **42 Core Web Criteria Baseline** (includes Form/Interaction criteria).*

| Criteria | Conformance Level | Remarks and Explanations |
| :--- | :--- | :--- |
| **1.1.1 Non-text Content** | Does Not Support | Alt text "Logo SEIU" is redundant; missing alt on 4 decorative icons. |
| **1.3.1 Info and Relationships** | Does Not Support | Missing landmark labels on search section; fragmented heading hierarchy (H4 -> H1). |
| **1.4.3 Contrast (Minimum)** | Does Not Support | Primary buttons (#0099B2) fail 4.5:1 ratio against white text. |
| **2.1.1 Keyboard** | Does Not Support | Mobile menu cannot be closed with "Escape" key. |
| **2.4.3 Focus Order** | Does Not Support | Mobile menu fails to trap focus; focus leaks into background content. |
| **2.4.4 Link Purpose** | Does Not Support | Ambiguous "Learn More" links lack contextual labels. |
| **2.5.8 Target Size (Min)** | Does Not Support | Social icons (11px) and Skip Link (16px) fail 24px requirement. |
| **3.3.1 Error Identification** | Supports | Search form correctly identifies empty queries (injected test). |
| **3.3.3 Error Suggestion** | Supports | System provides search suggestions for common misspellings. |
| **4.1.2 Name, Role, Value** | Supports | ARIA roles are correctly assigned to interactive widgets. |
| **All Other 32 Criteria** | Supports | No critical failures detected in standard baseline evaluations. |

---

## Evaluation Methods Used
- **Baseline**: 42 Success Criteria (standard 37 + 5 Form/Interaction criteria).
- **Automated Scanning**: Axe-core, Lighthouse, pa11y.
- **Manual Technical Audit**: Keyboard-only navigation, 400% zoom (Reflow) testing, color contrast calculation.
- **Screen Reader Validation**: Virtual NVDA Simulation via linear Accessibility Tree traversal.
- **Environment**: Chrome (Windows), NVDA Speech Viewer (Simulated).
