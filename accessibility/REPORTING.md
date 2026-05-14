# Accessibility Reporting Standards: Oshyn SEIUMB

Every finding in a remediation report MUST follow this exact high-fidelity structure for maximum scannability and copy-paste utility.

---

## 🏗️ The Live Preview Mandate

**CRITICAL:** The agent MUST update the `remediation_report_preview.md` in parallel with every finding registration. No finding is complete until it is reflected in the high-fidelity preview.

---

## 🏗️ Severity Classification

| Severity | Definition | Examples |
| :--- | :--- | :--- |
| **BLOCKER** | Prevents use for a specific group. | Keyboard trap, missing `aria-label` on icon button, no keyboard support. |
| **SERIOUS** | Significant barrier, high frustration. | Missing form labels, **Missing accessible landmarks**, Ambiguous link context. |
| **MODERATE** | Moderate barrier, degrades experience. | Heading skips, non-semantic grouping. |
| **MINOR** | Subtle barrier or cosmetic failure. | Redundant alt text, layout shift below 0.1. |

---

## 🏛️ Component Template: [Component Name]

> [!IMPORTANT]
> **STRICT ORDERING MANDATE:** All issues within a component section MUST be ordered by severity: **MINOR → MODERATE → SERIOUS → BLOCKER**.
> **NO SEVERITY IN TITLES:** Do NOT include the severity in the H3 title.

### [Issue Title]

- **Severity:** [MINOR | MODERATE | SERIOUS | BLOCKER]
- **Affected Impairments:** [Visual | Motor | Cognitive | Hearing]
- **Issue:** [Detailed description of the barrier found]
- **Successful criteria:** [Link Name (e.g. 2.4.7 Focus Visible)](URL_TO_WCAG)
- **Suggested remediation:** Ensure all interactive elements have a high-contrast focus ring (e.g., `outline: 3px solid #005daa`).
- **DOM Evidence:**

```html
[Exact source code snippet or CSS rule]
```

---

## 🏛️ Scoring Logic (VPAT 2.5)

- **Formula:** `((Supports * 1) + (Partially Supports * 0.5)) / Denominator * 100`
- **Criteria Baseline:** 42 Criteria (Mandatory for Interactive/Login pages).
 
 ### VPAT Header Format (STRICT)
 ```markdown
 Report Date: [Current Date] 
 Status: [Emoji] [Status Text] (e.g., 🔴 FAIL (Blocker & Serious Violations))
 Compliance Score: [XX.XX]% (Calculated across 42 evaluated criteria: [S] Supports, [P] Partially Supports, [D] Does Not Support)
 ```
 
 > [!IMPORTANT]
 > **The VPAT must include all 42 criteria in the conformance table**, even if N/A (mark as Supports with remark "N/A").

