---
name: accessibility
description: "Accessibility (a11y) best practices for web development. Focuses on WCAG 2.1/2.2 AA compliance, semantic HTML, and ARIA labels. Integrates with Accessibility Insights for Web and NVDA screen reader audits. Replaces earlier fragmented a11y workflows."
---

# Accessibility (a11y) Standards

Mandatory accessibility guidelines to ensure WCAG 2.1 and 2.2 AA compliance across all web applications.

## When to Apply

- Building any UI component or page
- Implementing interactive elements (buttons, links, forms)
- Reviewing or auditing existing interfaces
- Integrating icons or media

## Core Requirements (Oshyn FE Lead Standards)

### 1. Semantic HTML & Structure
- **Zero-Div Soup Policy**: Use semantic elements over `<div>` whenever possible.
- **Actions vs. Navigation**: Use `<button>` for functional actions (e.g., "Submit") and `<a>` for navigation. NEVER attach `onClick` to a `div`.
- **Form Controls**: Use proper `<label>` elements for all inputs.
- **Ordering of Findings**: ALWAYS order accessibility findings within a report from **MINOR** to **BLOCKER** (Minor -> Moderate -> Serious -> Blocker). This allows developers to see the lower-hanging fruit first before addressing structural blockers.

### 2. Labels & ARIA
- **Icon Buttons**: Every icon-only button MUST have an `aria-label`.
- **Contextual ARIA**: Use `aria-expanded`, `aria-haspopup`, and `aria-controls` for dropdowns and modals to assist screen readers.

### 3. Keyboard Navigation
- All interaction points must be focusable and respond to `Enter` or `Space`.
- Ensure a visible focus indicator (never set `outline: none` without a clear alternative).

### 4. Hierarchy & Structure
- Extract and verify all headings. The sequence must be logical (e.g., H1 -> H2 -> H3). NEVER skip heading levels.
- Provide a single `<h1>` per page that accurately summarizes the content.

### 5. Media Alternatives
- **Alt Text**: All images must have an `alt` attribute. Avoid placeholder text like "Responsive Image".
- **Captions/Labels**: Ensure technical diagrams and complex media have text descriptions.

To perform a comprehensive accessibility audit, trigger the expert workflow:
**Command:** `/expert-accessibility-audit`

This workflow utilizes the **Accessibility Insights for Web** Chrome extension and **NVDA Screen Reader** to perform both automated FastPass checks and manual Assessment tests, covering 95%+ of WCAG 2.1 & 2.2 AA criteria.

---

## 🛠️ Professional Audit Methodology (5-Layer SOP)

Every accessibility audit MUST follow this structured sequence to ensure 100% WCAG 2.1/2.2 AA coverage. The specific checks (like "Virtual NVDA" and "Heuristic Red Flags") are integrated directly into this workflow to ensure nothing is missed.

### 1. Executive Summary & Scope
Before technical testing, define the boundaries:
*   **The Scope**: List all URLs and critical user flows (e.g., "Registration", "Search Experience").
*   **Environment**: Document specific versions of browsers (Chrome/Firefox) and Assistive Technology (NVDA/JAWS/Virtual NVDA).
*   **Conformance Target**: State the version (e.g., WCAG 2.2 Level AA).

### 2. Automated Scanning (The Baseline)
Run baseline scans using `axe-core`, `pa11y`, or `lighthouse`.
*   **Catch Low-Hanging Fruit**: Missing IDs, basic contrast, and empty alt attributes.
*   **Reporting Disclaimer**: Explicitly state that automated tools only catch ~30% of potential barriers and serve only as a starting point.

### 3. Manual Technical Audit (The Core)
Apply expert frontend knowledge to check:
*   **Keyboard Operability**: Verify every interactive element is reachable. Confirm "Skip to Content" presence and absence of Keyboard Traps.
*   **Focus Management**: Ensure `:focus-visible` contrast is clear. Verify Focus Trapping in all modals and overlays.
*   **Source vs. Visual Order**: Ensure the Tab sequence follows a logical reading order regardless of CSS positioning.
*   **Reflow & Zoom (WCAG 1.4.10)**: Verify the site works at 400% zoom (320px width) without horizontal scroll or content overlap.
*   **Touch & Target Size (WCAG 2.2)**: Verify that all interactive targets are at least **24x24 CSS pixels**. Ensure no complex pointer gestures are required without a single-click alternative.

### 4. Screen Reader Validation (The User Experience)
*Utilizing the AI-Driven "Virtual NVDA" Simulation Rule:*
*   **Snapshot Extraction**: Take a verbose snapshot of the Accessibility Tree.
*   **Linear Announcement Logic**: Walk the tree from top-to-bottom. Announce landmarks, headings, links, and buttons with their state. Flag "No Text" or redundant announcements.
*   **Semantics & Landmarks**: Verify H1-H6 hierarchy and proper use of `<nav>`, `<main>`, and `<footer>`.
*   **Name, Role, Value**: Ensure every interactive element has a clear accessible name. (e.g., "Submit, button").
*   **ARIA Usage**: Validate that ARIA is used only when native HTML is insufficient. Ensure `aria-live` is used for dynamic updates.

### 5. Visual, Cognitive & Heuristic Checking
*   **Color Contrast**: Manually verify text contrast (4.5:1) and non-text contrast (3:1 for icons/borders).
*   **Seizure Safety**: Ensure no content flashes >3 times per second.
*   **Error Handling**: Verify error messages are clear and provide suggestions for correction.

#### 🧠 Critical Heuristic Red Flags (Lessons Learned)
Always manually verify these high-impact patterns during Phase 3 and 4:
1. **The "Dual-Purpose" Blocker**: Check if a link (e.g., "Sign In") redirects to a new URL on click while also attempting to act as a hover-dropdown trigger. This is a keyboard blocker.
2. **Keyboard Fatigue (The 10-Link Rule)**: If a navigation group contains >10 links without a "Skip to Content" link or arrow-key navigation, flag it as a Serious focus order violation.
3. **Triple-Redundant Link Trap**: Flag cases where an Image, a Heading, and a Button all point to the same URL in a single card. Recommend consolidating focus to the button only.
4. **The "Blank" Image Link**: Look for `alt="blank"` or `alt="image"` inside an anchor tag that has no other text. This effectively hides the link from screen readers.
5. **Missing Submit Buttons**: Verify every functional `<form>` has a physical `<button type="submit">`. Relying on JS-only submission breaks keyboard "Enter" support.
6. **"Escape" Key Support**: Always test the `Esc` key on search overlays, mobile menus, and modals. Lack of `Esc` support is a Serious Operability violation.
7. **Technical Alt Text Noise**: Scan for filenames (e.g., `alt="bg-circular.png"`) or technical descriptions in alt attributes. These must be hidden (`alt=""`).

---

### Standardized Reporting Templates
When documenting audit findings, always use these standardized titles and remediation strategies for recurring issues to ensure developer-ready consistency.

### Reporting Standards for Consistency:
1. **Group by Component:** Issues MUST be grouped by functional UI component (e.g., Header, Hero, FAQ).
2. **Sort by Severity (CRITICAL):** Within each component group, order issues strictly from **MINOR** to **BLOCKER** (Minor -> Moderate -> Serious -> Blocker).

> [!IMPORTANT]
> **CRITICAL RULE:** Failure to sort findings by severity (Minor to Blocker) within each section makes the report harder for developers to process. Always double-check that the "Severity" field follows this ascending order.

3. **Clear Divisors:** Use thematic dividers (e.g., `---`) between component groups.
4. **Dev-Friendly VPATs:** For Conformance Reports (VPATs), include a "Compliance by Component" summary in addition to the standard WCAG table.

#### Template: Master Technical Remediation Report
```markdown
# Master Technical Remediation Report: [Product Name]
**Audit Date:** [Date]
**Target URL:** [URL]

---

## 🏛️ Component: [Component Name]

### [Standardized Issue Title]
**Severity:** [BLOCKER | SERIOUS | MODERATE | MINOR]

**Affected Impairments:** [Visual | Motor | Cognitive | Hearing]

**Issue:** [Clear description of the barrier]

**Successful criteria:** [WCAG SC Link]

**Suggested remediation:** [Copy-pasteable fix and verification instructions]

**DOM Evidence:**
```html
[Exact DOM Snippet]
```

---
```

#### Template: Accessibility Conformance Report (VPAT®)
```markdown
# Accessibility Conformance Report (VPAT® 2.5): [Product Name]
**Audit Date:** [Date]
**Compliance Score:** [XX.XX]% (Calculated across 37 evaluated criteria: [X] Supports, [Y] Partially Supports, [Z] Does Not Support)

---

## 🏗️ Compliance Summary by Component
| Component | Status | Key Criteria Failed |
| :--- | :--- | :--- |
| [Component] | [Status] | [WCAG SCs] |

---

## WCAG 2.1 & 2.2 Conformance Table
*Evaluated against the 37 Core Web Criteria Baseline.*
| Criteria | Conformance Level | Remarks and Explanations |
| :--- | :--- | :--- |
| [SC] | [Supports | Does Not Support] | [Finding + User Impact] |
```

### 📏 The 37 Core Web Criteria Baseline
To ensure scoring consistency across marketing pages, we evaluate a standardized baseline of **37 Success Criteria**. This list is derived from the full WCAG 2.2 AA specification (55 criteria) by excluding 18 "Not Applicable" (N/A) items that govern functionality absent from standard marketing pages (e.g., Live Captions, Session Timeouts, Motion Sensors, or complex Legal/Financial data commits).

**The 37 Evaluated Criteria:**
- **Perceivable:** 1.1.1, 1.2.1, 1.2.2, 1.2.3, 1.2.5, 1.3.1, 1.3.2, 1.3.3, 1.3.4, 1.3.5, 1.4.1, 1.4.3, 1.4.4, 1.4.5, 1.4.10, 1.4.11, 1.4.12, 1.4.13
- **Operable:** 2.1.1, 2.1.2, 2.1.4, 2.2.2, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.4.5, 2.4.6, 2.4.7, 2.4.11, 2.5.1, 2.5.3, 2.5.8
- **Understandable:** 3.2.1, 3.2.2
- **Robust:** 4.1.1 (Parsing), 4.1.2

**Scoring Methodology:**
- **Supports (1pt):** Criterion passes or no violations were found during the audit.
- **Partially Supports (0.5pt):** Minor or localized failures that do not prevent completion of the task.
- **Does Not Support (0pt):** Systemic failures or Blockers that significantly impact the user experience.
- **Score Calculation:** `((Supports * 1) + (Partially Supports * 0.5)) / 37 * 100`

#### 🚫 Excluded Criteria (Not Applicable)
The following 18 criteria from the full WCAG 2.2 AA (55 total) are excluded from the baseline as they govern functionality absent from standard marketing pages:
1.  **1.2.4 Captions (Live)**: No live streaming video.
2.  **1.4.2 Audio Control**: No auto-playing background audio.
3.  **2.2.1 Timing Adjustable**: No session timeouts or time limits.
4.  **2.3.1 Three Flashes**: No flickering or flashing content.
5.  **2.5.2 Pointer Cancellation**: No custom touch-up event execution.
6.  **2.5.4 Motion Actuation**: No device-shaking functionality.
7.  **2.5.7 Dragging Movements**: No drag-and-drop UI components.
8.  **3.1.1 Language of Page**: Handled globally by CMS metadata.
9.  **3.1.2 Language of Parts**: No mixed-language text sections.
10. **3.2.3 Consistent Navigation**: Global site requirement (multi-page).
11. **3.2.4 Consistent Identification**: Global site requirement (multi-page).
12. **3.2.6 Consistent Help**: No body-embedded help/support modules.
13. **3.3.1 Error Identification**: No form validation on marketing pages.
14. **3.3.3 Error Suggestion**: No form error correction needed.
15. **3.3.4 Error Prevention (Legal)**: No legal transactions on-page.
16. **3.3.7 Redundant Entry**: No multi-step data entry processes.
17. **3.3.8 Accessible Authentication**: No login/password fields.
18. **4.1.1 Parsing (Deprecated)**: Now officially deprecated in WCAG 2.2 (though tracked for critical HTML bugs).

#### 🔄 Conditional Re-inclusion Rules
While 37 is the baseline for static/informational marketing pages, if the audited page contains interactive workflows, the following criteria **MUST** be added back into the evaluation:

| If the page contains... | Add these Success Criteria (SC) |
| :--- | :--- |
| **Forms / Submissions** | 3.3.1 (Error Identification), 3.3.3 (Error Suggestion), 3.3.4 (Error Prevention), 3.3.7 (Redundant Entry), 2.5.2 (Pointer Cancellation). |
| **Login / Auth** | 3.3.8 (Accessible Authentication - Min). |
| **Drag & Drop UI** | 2.5.7 (Dragging Movements). |
| **Live Support/Help** | 3.2.6 (Consistent Help). |

**Note on Scoring:** If criteria are added back, the denominator of the Page Compliance Score must be adjusted accordingly (e.g., if 5 form criteria are added, the score is calculated out of 42).

---

### Standardized Issue Library
| :--- | :--- | :--- | :--- | :--- |
| **Missing Landmark Label** | The `<section>` tag lacks an `aria-label` or `aria-labelledby`. | 1.3.1 | MINOR | Visual (Screen Reader) |
| **Non-Semantic Body Text (Span Soup)** | Body content wrapped in `<span>` with inline styles instead of `<p>`. | 1.3.1 | MINOR | Visual, Cognitive |
| **Invalid HTML Nesting** | Block-level elements (like `<p>`) nested inside a heading tag (e.g. `<h5>`). | 4.1.1 | SERIOUS | Visual (Parsing error) |
| **Empty Spacer Elements** | Empty `<p>&nbsp;</p>` or `<div>&nbsp;</div>` used for visual spacing. | 1.3.1 | MINOR | Visual (Screen Reader noise) |
| **Invalid Interactive Element (Link as Toggle)** | An `<a>` tag with `href="#"` used for state toggles; missing `role="button"`. | 4.1.2 | SERIOUS | Visual, Motor (Keyboard) |
| **Redundant Image Alt Text** | Alt text including redundant words like "logo" or "image". | 1.1.1 | MINOR | Visual (Screen Reader noise) |
| **Non-Semantic Eyebrow Text** | A `<p>` tag section indicator directly above a heading. | 1.3.1 | MINOR | Visual, Cognitive |
| **Missing List Semantics** | Grouped cards/features marked as `div`s instead of `<ul>`. | 1.3.1 | MINOR | Visual (Screen Reader) |
| **Fragmented Heading Hierarchy** | Skipped heading levels (e.g., H1 -> H5). | 1.3.1 | SERIOUS | Visual (Screen Reader) |
| **Duplicate Announcements** | Concurrent mobile/desktop containers active in the a11y tree. | 1.3.1 | SERIOUS | Visual (Screen Reader) |
| **Fragmented Heading Announcement** | Inline tags (like `<sup>`) causing screen readers to split a heading. | 1.3.1 | SERIOUS | Visual (Screen Reader) |
| **Fragmented Heading Announcement** | Inline tags (like `<sup>`) causing screen readers to split a heading. | 1.3.1 | SERIOUS | Visual (Screen Reader) |
| **Fake Button (Anchor without Role)** | Link used as button (`javascript:void(0)`) without keyboard support. | 4.1.2 | SERIOUS | Motor, Visual |
