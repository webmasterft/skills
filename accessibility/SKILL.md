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
**Command:** `/iaap` (defined in [iaap-workflow.md](./iaap-workflow.md))

---

## 🏗️ Phase 0: Project Handshake & Evidence SOP

Every audit begins with a clean workspace to ensure artifacts are modular and developer-ready.

### 1. Identify Workspace
The agent will confirm the absolute path for the audit (e.g., `C:/oshyn/seiumb`).

### 2. Scaffold Directories
The agent will create the following folders:
- `/a11y-audits/evidence/`: For NVDA logs, console errors, and screenshots.
- `/a11y-audits/reports/`: For the Master report, VPAT, and page-specific findings.

### 3. Setup NVDA Speech Logger (Verbatim Evidence)
To provide "unassailable evidence" in the remediation report, follow this one-time setup per project:
1.  **Open NVDA Settings**: `NVDA + N` -> Preferences -> Settings.
2.  **Select Speech Logger**: Find the "Speech Logger" category in the left sidebar.
3.  **Set Output Path**: Paste the project-specific path provided by the agent:
    `[PROJECT_PATH]\a11y-audits\evidence\nvda-speech.log`
4.  **Logging Trigger**: Toggle logging **ON** with `NVDA + Alt + L` right before you start your tab-sequence audit.
5.  **Finish & Submit**: Toggle logging **OFF** once finished. The agent will then read this `.log` file to extract verbatim speech announcements for the final report.

---

## 🛠️ Professional Audit Methodology (5-Layer SOP)

Every accessibility audit MUST follow this structured sequence to ensure 100% WCAG 2.1/2.2 AA coverage. The specific checks (like "Virtual NVDA" and "Heuristic Red Flags") are integrated directly into this workflow to ensure nothing is missed.

### 1. Executive Summary & Scope

Before technical testing, define the boundaries:

- **The Scope**: List all URLs and critical user flows (e.g., "Registration", "Search Experience").
- **Environment**: Document specific versions of browsers (Chrome/Firefox) and Assistive Technology (NVDA/JAWS/Virtual NVDA).
- **Conformance Target**: State the version (e.g., WCAG 2.2 Level AA).

### 2. Automated Scanning (The Baseline)

Run baseline scans using the right tool for the specific context:

| Tool              | Primary Use Case                | Key Strength                                      |
| :---------------- | :------------------------------ | :------------------------------------------------ |
| **Axe-Core**      | In-browser dev/debugging.       | Zero false-positive policy.                       |
| **Lighthouse**    | Quick page-level sanity checks. | Integrated A11y + SEO performance metrics.        |
| **Pa11y**         | Automated CLI scripts & CI/CD.  | Fast headless auditing with JSON exports.         |
| **A11y Insights** | **Mandatory** for full audits.  | Guided "Assessment" tests for non-automatable SC. |

- **Catch Low-Hanging Fruit**: Missing IDs, basic contrast, and empty alt attributes.
- **Reporting Disclaimer**: Explicitly state that automated tools only catch ~30% of potential barriers and serve only as a starting point.

### 3. Manual Technical Audit (The Core)

Apply expert frontend knowledge to check:

- **Keyboard Operability**: Verify every interactive element is reachable. Confirm "Skip to Content" presence and absence of Keyboard Traps.
- **Focus Management**: Ensure `:focus-visible` contrast is clear. Verify Focus Trapping in all modals and overlays.
- **Focus Visible & Tab Sequence Analysis**: The AI executes live DOM scripts via MCP to mathematically map `tabindex` flows and verify the presence of CSS `:focus-visible` properties across all interactive elements.

### 3. Visual & Layout Adaptability (Color & Contrast)
*Testing the "Perceivable" principle under different user constraints.*

#### A. Color Contrast Standards (WCAG 1.4.3 / 1.4.11)
- **Normal Text**: Minimum **4.5:1** ratio.
- **Large Text (18pt+ or 14pt bold)**: Minimum **3:1** ratio.
- **UI Components & Graphics**: Non-text contrast (icons, borders, focus indicators) must be at least **3:1**.
- **The "Color-Only" Failure**: Information MUST NOT be conveyed by color alone. (e.g., Required fields must use an asterisk or label, not just a red border).

#### B. Visual Disability Simulation Checklist
Perform audits using color-blindness simulators (like Chrome DevTools or specialized extensions) to verify visibility for:
- **Protanopia & Deuteranopia** (Red-Green blindness): Ensure critical buttons (Success/Error) remain distinguishable by shape or icon.
- **Tritanopia** (Blue-Yellow blindness): Check that link colors remain visible against backgrounds.
- **Achromatopsia** (Total color blindness): The UI must remain functional in grayscale.
- **Low Vision & Cataracts**: Verify that borders and text remain legible under a "blur" filter or when contrast is slightly reduced.

#### C. Reflow & Zoom (WCAG 1.4.10)
- **Reflow (400% Zoom):** At 400% zoom on a 1280px wide screen, does the content flow vertically without a horizontal scrollbar?
- **Text Spacing:** Increase line height (to 1.5) and paragraph spacing (to 2). Does text overlap or get cut off in fixed-height containers?
- **Motion & Animations (WCAG 2.3.3)**: Verify that `prefers-reduced-motion` media queries are respected. Parallax, hero background videos, and heavy transitions MUST halt or simplify when this preference is set.

### 4. Screen Reader Validation (The User Experience)

> [!IMPORTANT]
> **Mandatory Evidence Protocol:** No Screen Reader findings are considered "confirmed" without a corresponding log entry captured via the **[NVDA-SOP.md](./NVDA-SOP.md)**.

_Utilizing the AI-Driven "Virtual NVDA" Simulation Rule:_

- **Virtual NVDA Simulation**: Perform a simulated NVDA read based on the accessibility tree (linear reading order, semantics, ARIA live regions) to expose "Invisible" barriers. The AI can generate a simulated NVDA transcript by linearly traversing the accessibility tree, predicting exactly what a screen reader user would hear.
- **Snapshot Extraction**: Take a verbose snapshot of the Accessibility Tree.
- **Linear Announcement Logic**: Walk the tree from top-to-bottom. Announce landmarks, headings, links, and buttons with their state. Flag "No Text" or redundant announcements.
- **Semantics & Landmarks**: Verify H1-H6 hierarchy and proper use of `<nav>`, `<main>`, and `<footer>`.
- **Name, Role, Value**: Ensure every interactive element has a clear accessible name. (e.g., "Submit, button").
- **ARIA Usage**: Validate that ARIA is used only when native HTML is insufficient. Ensure `aria-live` is used for dynamic updates.
- **Link Purpose in Context (2.4.4)**: Audit for "Read More" or "Learn More" link soup. Every link must either have descriptive text or an `aria-label` providing context.
- **Real-World Verification (Speech Logger)**: Use the **Speech Logger** add-on to capture a verbatim transcript of the audit. This serves as the "Gold Standard" evidence for technical remediation.

### 5. Visual, Cognitive & Heuristic Checking

- **Color Contrast**: Manually verify text contrast (4.5:1) and non-text contrast (3:1 for icons/borders).
- **Seizure Safety**: Ensure no content flashes >3 times per second.
- **Error Handling**: Verify error messages are clear and provide suggestions for correction.

#### 🧠 Critical Heuristic Red Flags (Lessons Learned)

Always manually verify these high-impact patterns during Phase 3 and 4:

1. **The "Dual-Purpose" Blocker**: Check if a link (e.g., "Sign In") redirects to a new URL on click while also attempting to act as a hover-dropdown trigger. This is a keyboard blocker.
2. **Keyboard Fatigue (The 10-Link Rule)**: If a navigation group contains >10 links without a "Skip to Content" link or arrow-key navigation, flag it as a Serious focus order violation.
3. **Triple-Redundant Link Trap**: Flag cases where an Image, a Heading, and a Button all point to the same URL in a single card. Recommend consolidating focus to the button only.
4. **The "Blank" Image Link**: Look for `alt="blank"` or `alt="image"` inside an anchor tag that has no other text. This effectively hides the link from screen readers.
5. **Missing Submit Buttons**: Verify every functional `<form>` has a physical `<button type="submit">`. Relying on JS-only submission breaks keyboard "Enter" support.
6. **"Escape" Key Support**: Always test the `Esc` key on search overlays, mobile menus, and modals. Lack of `Esc` support is a Serious Operability violation.
7. **Technical Alt Text Noise**: Scan for filenames (e.g., `alt="bg-circular.png"`) or technical descriptions in alt attributes. These must be hidden (`alt=""`).
8. **Placeholder-as-label**: Using `<input placeholder="Email">` without a visible `<label>`. This fails 1.3.5 and 3.3.2.
9. **Ghost Announcements (display:none vs aria-hidden)**: Ensure hidden content is removed from both CSS and the A11y tree. CSS `visibility:hidden` still leaves elements in the tree.
10. **SVG Decorative Leaks**: Decorative SVGs MUST have `aria-hidden="true"` and `focusable="false"` to prevent "graphic" announcements or tab stops.

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

---

## ⚙️ Technical Setup: NVDA Automation

To bridge the gap between AI simulation and real-world screen reader testing, follow this setup:

1.  **Install Speech Logger**: Use the add-on located at `C:\FTORRES\AI\accessibility\NVDA` (or the latest version from GitHub).
2.  **Log Destination**: In NVDA settings (**Preferences > Settings > Speech Logger**), set the output path to:
    `C:\FTORRES\AI\accessibility\logs\nvda-speech.log`
3.  **The Trigger**: Toggle logging with `NVDA + Alt + L` before starting the tab-sequence audit.
4.  **Evidence Collection**: After auditing, provide the `.log` file to the AI agent. This allows the agent to verify exactly what a human user hears, ensuring 100% accuracy in the remediation report.

---

---

### 📏 The 37 Core Web Criteria Baseline

To ensure scoring consistency across marketing pages, we evaluate a standardized baseline of **37 Success Criteria**. This list is derived from the full WCAG 2.2 AA specification (55 criteria) by excluding 18 "Not Applicable" (N/A) items.

**The 37 Evaluated Criteria:**

- **Perceivable:** 1.1.1, 1.2.1, 1.2.2, 1.2.3, 1.2.5, 1.3.1, 1.3.2, 1.3.3, 1.3.4, 1.3.5, 1.4.1, 1.4.3, 1.4.4, 1.4.5, 1.4.10, 1.4.11, 1.4.12, 1.4.13
- **Operable:** 2.1.1, 2.1.2, 2.1.4, 2.2.2, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.4.5, 2.4.6, 2.4.7, 2.4.11, 2.5.1, 2.5.3, 2.5.8
- **Understandable:** 3.2.1, 3.2.2
- **Robust:** 4.1.1 (Parsing), 4.1.2

**Scoring Methodology:**

- **Supports (1pt) / Partially (0.5pt) / Does Not Support (0pt)**.
- **Score Calculation:** `((Supports * 1) + (Partially Supports * 0.5)) / Denominator * 100` (Denominator is 37 by default).

#### 🔄 Conditional Re-inclusion Rules

| If the page contains... | Add these Success Criteria (SC)                                                          |
| :---------------------- | :--------------------------------------------------------------------------------------- |
| **Sticky UI**           | 2.4.11 (Focus Not Obscured - Min).                                                       |
| **Forms / Submissions** | 3.3.1 (Error ID), 3.3.3 (Error Suggestion), 3.3.4 (Prevention), 3.3.7 (Redundant Entry). |
| **Login / Auth**        | 3.3.8 (Accessible Authentication - Min).                                                 |
| **Drag & Drop**         | 2.5.7 (Dragging Movements).                                                              |

---

### 📄 Mandatory Reporting
Upon completion of the audit, generate the dual-document output defined in **[REPORTING.md](./REPORTING.md)**. 

Every issue found across all phases MUST be documented in both the **Master Technical Remediation Report** (sorted Minor to Blocker) and the **VPAT® 2.5 ACR**.

---

### Standardized Issue Library

Use these standardized titles and remediation strategies for recurring patterns to ensure consistency.

| Standard Title            | Recurring Issue Description                                                   | WCAG SC | Severity | Affected Impairments         |
| :------------------------ | :---------------------------------------------------------------------------- | :------ | :------- | :--------------------------- |
| **Landmark Label**        | The `<section>` tag lacks an `aria-label` or `aria-labelledby`.               | 1.3.1   | MINOR    | Visual (Screen Reader)       |
| **Span Soup**             | Body content wrapped in `<span>` with inline styles instead of `<p>`.         | 1.3.1   | MINOR    | Visual, Cognitive            |
| **Invalid HTML Nesting**  | Block-level elements (like `<p>`) nested inside a heading tag (e.g. `<h5>`).  | 4.1.1   | SERIOUS  | Visual (Parsing error)       |
| **Empty Spacer Elements** | Empty `<p>&nbsp;</p>` or `<div>&nbsp;</div>` used for visual spacing.         | 1.3.1   | MINOR    | Visual (Screen Reader noise) |
| **Link as Toggle**        | An `<a>` tag with `href="#"` used for state toggles; missing `role="button"`. | 4.1.2   | SERIOUS  | Visual, Motor (Keyboard)     |
| **Redundant Alt**         | Alt text including redundant words like "logo" or "image".                    | 1.1.1   | MINOR    | Visual (Screen Reader noise) |
| **Eyebrow Text**          | A `<p>` tag section indicator directly above a heading.                       | 1.3.1   | MINOR    | Visual, Cognitive            |
| **List Semantics**        | Grouped cards/features marked as `div`s instead of `<ul>`.                    | 1.3.1   | MINOR    | Visual (Screen Reader)       |
| **H-Hierarchy**           | Skipped heading levels (e.g., H1 -> H5).                                      | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **Duplicate Announces**   | Concurrent mobile/desktop containers active in the a11y tree.                 | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **H-Announcement**        | Inline tags (like `<sup>`) causing screen readers to split a heading.         | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **Fake Button**           | Link used as button (`javascript:void(0)`) without keyboard support.          | 4.1.2   | SERIOUS  | Motor, Visual                |
| **Link Soup**             | "Read More" links without descriptive aria-labels for context.                | 2.4.4   | MODERATE | Visual (Screen Reader)       |
| **Motion Failure**        | Animations/Parallax failing to respect `prefers-reduced-motion`.              | 2.3.3   | MODERATE | Visual, Cognitive            |

---

## 📂 Multi-Page Auditing Strategy

When auditing a large site with multiple pages, follow this structure:

1.  **Shared Components First**: Audit global elements (Header, Footer, Navigation) once. Refer back to these in subsequent page reports to avoid redundancy.
2.  **Report Structure**:
    *   **Option A (Combined)**: One large Remediation Report with H2 sections for each Page/URL.
    *   **Option B (Modular)**: One directory per audit (e.g., `/audits/home-page/`, `/audits/contact-page/`) each with its own dual-document set.
3.  **Global VPAT**: Generate one **VPAT® 2.5 ACR** that represents the *entire project scope*. The score should be an average across all audited pages, or the lowest score found (to represent the "weakest link").
4.  **Issue Tracking**: Assign unique IDs to issues (e.g., `ISSUE-001`) if you are managing the remediation in a Jira/GitHub backlog.
