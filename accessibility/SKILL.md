---
name: accessibility
description: "Accessibility (a11y) best practices for web development. Focuses on WCAG 2.1/2.2 AA compliance, semantic HTML, and ARIA labels. Integrates with Accessibility Insights for Web and NVDA screen reader audits. Replaces earlier fragmented a11y workflows."
---

# Accessibility (a11y) Standards

## 4-Layer Accessibility Audit Methodology

When performing an expert audit, execute these layers in order to ensure WCAG 2.1/2.2 AA compliance.

### Layer 1: Keyboard & Focus Control
*The foundation of the "Operable" principle. Do not use your mouse.*
- **Skip Link:** Does a "Skip to Content" link appear on the first Tab? Does it actually move focus to the `<main>` element?
- **Focus Visibility:** Is the `:focus-visible` state clearly visible (high contrast)? Never use `outline: none`.
- **Focus Order:** Does the tabbing follow a logical visual flow (top-to-bottom, left-to-right)? Check that CSS Flexbox order or Grid hasn't broken the DOM sequence.
- **Keyboard Traps:** Can you enter and exit modals, menus, and tooltips using only `Tab` and `Esc`?
- **Non-Interactive Elements:** Ensure `<div>` or `<span>` elements aren't in the tab order unless they are truly interactive.

### Layer 2: Screen Reader Usability
*Testing with NVDA (Windows) or VoiceOver (macOS). Focus on "Understandable".*
- **Semantic Landmarks:** Use the "Elements List" (`Insert + F7` in NVDA). Are there landmarks like `<header>`, `<nav>`, `<main>`, and `<footer>`?
- **Headings Hierarchy:** Is there exactly one `<h1>`? Do headings follow a strict nesting order (`h1 > h2 > h3`) without skipping levels for styling?
- **Images & Context:** Do `alt` attributes describe the purpose, not just the pixels? (e.g., "Search" instead of "Magnifying glass icon").
- **Form Labels:** When tabbing into an input, does the screen reader announce the label, current value, and state (e.g., "Required", "Invalid")?
- **Dynamic Content:** When an error appears or a cart updates, is it announced? (Check for `aria-live="polite"`).

### Layer 3: Visual & Layout Adaptability
*Testing the "Perceivable" principle under different user constraints.*
- **Reflow (400% Zoom):** At 400% zoom on a 1280px wide screen, does the content flow vertically without a horizontal scrollbar?
- **Text Spacing:** Increase line height (to 1.5) and paragraph spacing (to 2). Does text overlap or get cut off in fixed-height containers?
- **Color Contrast:** Use a tool to verify text against backgrounds (AA requires 4.5:1).
- **Color as Meaning:** Ensure information isn't conveyed only by color (e.g., an error shouldn't just be a red border; it needs an icon or text label).

### Layer 4: Touch & Pointer (WCAG 2.2 focus)
*Critical for mobile and motor-impaired users.*
- **Target Size:** Are all interactive targets (buttons, links) at least 24x24 CSS pixels?
- **Pointer Gestures:** If a feature requires a complex gesture (like swiping or dragging), is there a single-click alternative (like "Up" and "Down" buttons)?
- **Orientation:** Does the site function perfectly in both Portrait and Landscape modes without losing data or functionality?

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

### 4-Layer Manual Testing Protocol

All audits must include manual verification across these four critical layers:

#### 1. Keyboard-Only Testing (The "No Mouse" Rule)
*   **Skip Links**: Ensure a "Skip to Main Content" link appears on the first tab and correctly moves focus to the `<main>` element.
*   **Focus Visibility**: Verify that all interactive elements have a clear, high-contrast focus indicator (never use `outline: none`).
*   **Focus Order**: Tab sequence must follow the logical visual flow.
*   **Keyboard Traps**: Ensure users can enter and exit all modals, dropdowns, and overlays using only the keyboard (Esc must close overlays).
*   **Target Size (WCAG 2.2)**: Verify that all interactive targets are at least **24x24 CSS pixels**.

#### 2. Screen Reader Testing (The "Eyes Closed" Rule)
*   **Landmarks & Headings**: Verify structure using the Elements List (e.g., NVDA Insert + F7). Ensure a single `<h1>` and meaningful `<nav>`, `<main>`, and `<footer>` landmarks.
*   **Dynamic Content (ARIA Live)**: Confirm that toasts, errors, and live updates are announced (use `aria-live="polite"`).
*   **Image Context**: Alt texts must be descriptive; decorative images must be hidden (`alt=""` or `aria-hidden="true"`).
*   **Form Labels**: Inputs must announce their label, state (required/invalid), and any helper text via `aria-describedby`.

#### 3. Visual & Reflow Testing (The "User Preference" Rule)
*   **Zoom & Reflow (WCAG 1.4.10)**: Zoom to **400%**. Site must reflow to a single column with **no horizontal scrolling** or content overlap.
*   **Text Spacing (WCAG 1.4.12)**: Increase line height and letter spacing. Text must remain contained without truncation.
*   **Color Contrast**: Maintain **4.5:1** for regular text and **3:1** for large text/UI components.
*   **High Contrast Mode**: Verify visibility of icons and borders in Windows High Contrast Mode.

#### 4. Code & Semantic Inspection (The "Lead Dev" Rule)
*   **Semantic HTML**: Use `<button>` for actions and `<a>` for navigation. No `div` with `onClick`.
*   **ARIA Validation**: Follow the First Rule of ARIA: If a native HTML element exists, do not use ARIA.
*   **Form Errors**: Ensure `aria-describedby` links error messages to inputs.

---

### Standardized Reporting Templates
When documenting audit findings, always use these standardized titles and remediation strategies for recurring issues to ensure developer-ready consistency.

### Reporting Standards for Consistency:
1. **Group by Component:** Issues MUST be grouped by functional UI component (e.g., Header, Hero, FAQ).
2. **Sort by Severity (CRITICAL):** Within each component group, order issues strictly from **MINOR** to **BLOCKER** (Minor -> Moderate -> Serious -> Blocker).

> [!IMPORTANT]
> **CRITICAL RULE:** Failure to sort findings by severity (Minor to Blocker) within each section makes the report harder for developers to process. Always double-check that the "Severity" field follows this ascending order.

3. **Bulleted Details:** Use bullet points for all issue metadata (Severity, Impairments, etc.).
4. **Clear Divisors:** Use thematic dividers (e.g., `---`) between component groups.
4. **Dev-Friendly VPATs:** For Conformance Reports (VPATs), include a "Compliance by Component" summary in addition to the standard WCAG table.

#### Template: Master Technical Remediation Report
```markdown
# Master Technical Remediation Report: [Product Name]
**Audit Date:** [Date]
**Target URL:** [URL]

---

## 🏛️ Component: [Component Name]

### [Standardized Issue Title]

- **Severity:** [BLOCKER | SERIOUS | MODERATE | MINOR]
- **Affected Impairments:** [Visual | Motor | Cognitive | Hearing]
- **Issue:** [Clear description of the barrier]
- **Successful criteria:** [WCAG SC Link]
- **Suggested remediation:** [Copy-pasteable fix and verification instructions]
- **DOM Evidence:**
```html
[Exact DOM Snippet]
```

---
```

#### Template: Accessibility Conformance Report (VPAT®)
```markdown
# Accessibility Conformance Report (VPAT® 2.5): [Product Name]
**Audit Date:** [Date]
**Page Compliance Score:** [XX.XX]% (Calculated across 37 evaluated criteria: [X] Supports, [Y] Partially Supports, [Z] Does Not Support)

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
| **Fake Button (Anchor without Role)** | Link used as button (`javascript:void(0)`) without keyboard support. | 4.1.2 | SERIOUS | Motor, Visual |
