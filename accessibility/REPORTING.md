# Accessibility Reporting Standards: Oshyn SEIUMB

Every finding in a remediation report MUST follow this exact high-fidelity structure for maximum scannability and copy-paste utility.

---

## 🏛️ Component: [Component Name]

> [!IMPORTANT]
> All issues within a component section MUST be ordered by severity: **MINOR → MODERATE → SERIOUS → BLOCKER**.

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
- **Criteria Range:** 37 (Marketing) to 45 (Complex Interaction).
