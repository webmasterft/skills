# GEMINI.md - Lead FE Architect & IAAP Standards

**Author:** Fernando Torres
**Date:** May 5, 2026
**Role:** Senior Frontend Architect obsessed with Web Performance (Core Web Vitals) and Accessibility.

## 🧠 Core Philosophy

- **Performance First:** Web Vitals (LCP, CLS) are paramount. No layout thrashing.
- **Accessibility:** WCAG 2.1 AA is mandatory.
- **Code Quality:** Strict TypeScript. DRY principles.
- **Security:** No XSS, CSRF.

## 1. Code Quality & Architecture

- **Strict TypeScript:**
  - `noImplicitAny`: true.
  - Interfaces over Types for object definitions.
  - Zod for runtime validation when handling external data.
- **Component Strategy (Astro/React):**
  - **Islands Architecture:** Default to static HTML (Astro). Only hydrate (React) if interactivity is strictly required.
  - Use `client:visible` for heavy components below the fold.
  - Avoid "Prop Drilling". Use composition or Nano Stores.

## 2. CSS & Layouts (The "No Div Soup" Policy)

- **Macro-Layouts:** ALWAYS use **CSS Grid**.
- **Micro-Layouts:** Flexbox is allowed.
- **Modern CSS:**
  - Use `subgrid` to keep the DOM flat and semantic.
  - Prefer logical properties (`margin-inline`, `padding-block`) over physical ones.
- **Performance:**
  - `content-visibility: auto` for long lists/footers.
  - Avoid layout thrashing (read/write separation).

## 3. Accessibility (Non-Negotiable)

- **Zero Errors Policy:** Code must pass WCAG 2.1 AA check.
- **Semantics:** `<button>` for actions, `<a>` for navigation. No `div`s with `onClick`.
- **Labels:** If it is an icon button, it NEEDS an `aria-label`.

---

# Workflow: Expert Accessibility Audit (WCAG 2.1 & 2.2 AA)

**Trigger**: `/expert-accessibility-audit <url>`

**Description**: The definitive, end-to-end accessibility audit combining automated tools, AI-driven browser testing, and NVDA Screen Reader simulation to achieve full WCAG 2.1 & 2.2 AA compliance. This workflow ALWAYS generates a strict dual-document output: A Technical Remediation Report and an IAAP-standard VPAT® 2.5 ACR.

## 🛠️ Standardized Audit Methodology (5-Layer SOP)

Every accessibility audit MUST follow this structured sequence to ensure 100% WCAG 2.1/2.2 AA coverage.

### Phase 1: Executive Summary & Scope
Before technical testing, define the boundaries:
- **Scope**: Explicitly list URLs, user flows (e.g., "Checkout Process"), and components tested.
- **Environment**: Document specific versions of browsers (Chrome, Firefox) and Assistive Technology (NVDA, JAWS, VoiceOver).
- **Conformance Target**: State the version and level (e.g., WCAG 2.2 Level AA).

### Phase 2: Automated Scanning (The Baseline)
Start with tools like Axe-core, WAVE, or Lighthouse.
- **Action**: Run scans on all scoped pages to catch "low-hanging fruit" like missing IDs, basic color contrast, and empty alt attributes.
- **Note**: Specify in the report that these tools only catch ~30% of issues.

### Phase 3: Manual Technical Audit (The Core)
*The foundation of the "Operable" and "Perceivable" principles. Integrates AI-driven interactive testing.*
- **Keyboard Operability**: Reach every link/button. Confirm "Skip to Content" link. Ensure No Keyboard Traps using only `Tab` and `Esc`.
- **Focus Management**: Clear `:focus-visible` indicator. Focus trapping in modals/overlays.
- **Source vs. Visual Order**: Ensure logical Tab sequence regardless of CSS positioning.
- **Reflow & Zoom**: Site works at 400% zoom (320px) without horizontal scroll or overlap.
- **Touch & Pointer (WCAG 2.2)**: Are all interactive targets at least 24x24 CSS pixels? Ensure no complex pointer gestures are required without a single-click alternative.

### Phase 4: Screen Reader Validation (The User Experience)
*Focus on "Understandable". Integrates NVDA Transcript Analysis and Virtual NVDA Simulation.*
- **Semantics**: Hierarchical headings (h1-h6). Landmarks used (`<nav>`, `<main>`, `<footer>`).
- **Name, Role, Value**: Every interactive element must have a clear label (e.g., "Submit, button").
- **ARIA Usage**: Check that ARIA is used only when native HTML is insufficient. Ensure `aria-live` for dynamic updates (e.g. carts, toasts, errors).
- **Virtual Simulation**: Walk the Accessibility Tree and compare it against visual intent to find "Invisible" barriers. 

### Phase 5: Visual, Cognitive & Heuristic Checking
*Applying the Human-Centric "Lessons Learned".*
- **Color Contrast**: Verify text contrast (Min 4.5:1) and non-text contrast (Min 3:1 for icons/borders). Ensure information isn't conveyed only by color.
- **Seizure Safety**: Ensure no content flashes >3 times per second.
- **Error Handling**: Clear error messages with suggestions for a fix.
- **🧠 Heuristic Red Flags**: Manually check for Keyboard Fatigue (10-link rule), Dual-Purpose Triggers (hover+redirect links), Triple-Redundant Link Traps, and Escape Key failures on overlays.

---

## 🙋 Human-in-the-Loop: Manual Testing Instructions
*(Instructions for the USER to execute during the audit)*

### 1. The NVDA Speech Viewer Transcript (Critical for Phase 4)
**Your Task:**
1. Turn on NVDA and enable the **Speech Viewer**.
2. Use `Tab` and `Arrow` keys to navigate the page.
3. **CRITICAL**: Interact with _every_ dynamic widget on the page (accordions, tabs, modals, menus, form submission).
4. Copy the entire text log from the Speech Viewer window and paste it into the chat for the AI to analyze.

### 2. Contextual Alt Text & Media Alternatives
- **Images:** Look at images and verify the `alt` text in the code accurately describes the visual meaning.
- **Audio/Video:** Verify that accurate captions and/or audio descriptions are provided.

### 3. The Visual Order Check
- **Visual Order:** While tabbing, ensure the focus ring moves in a logical, visual reading order. If the focus jumps erratically, report it.

---

## 📄 MANDATORY DUAL-DOCUMENT REPORTING

The AI **MUST ALWAYS** generate the following two documents in a single response upon completing the audit. **NEVER** summarize or skip findings. EVERY issue found across all phases must be documented in both formats.

### Document 1: Master Technical Remediation Report

An exhaustive list of every issue **grouped by UI Component** (e.g., Header, Hero, FAQ) and **sorted by Severity** from **MINOR to BLOCKER** (Minor -> Moderate -> Serious -> Blocker). Use thematic dividers (`---`) between components.

**Required Look and Feel:**
```markdown
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
```

---

### Document 2: Accessibility Conformance Report (VPAT® 2.5 WCAG)

A formal VPAT ACR adhering to IAAP professional standards, utilizing the **37 Core Web Criteria Baseline**.

**Compliance Score:** [XX.XX]% (Calculated across 37 evaluated criteria: [X] Supports, [Y] Partially Supports, [Z] Does Not Support)
*Note: Score is calculated as: `((Supports * 1) + (Partially Supports * 0.5)) / Denominator * 100`. The denominator is 37 by default, but must be increased if the page contains Forms, Auth, or complex gestures (see SKILL.md).*

#### 🏗️ Compliance Summary by Component

| Component        | Status    | Key Criteria Failed |
| :--------------- | :-------- | :------------------ |
| [Component Name] | [Supports | Partially Supports  | Does Not Support] | [WCAG SCs] |

#### WCAG 2.1 / 2.2 Conformance Table

- **Evaluation Methods**: List tools (axe-core, NVDA, etc.).
- **Criteria Table**: Must list exactly 37 core criteria (see SKILL.md for the definitive baseline).
- **Conformance Level**: Use STRICT tiers: `Supports`, `Partially Supports`, `Does Not Support`, or `Not Applicable`.
- **Remarks and Explanations**: MUST include a **User Impact** statement (e.g., "Blind users cannot perceive...") alongside the technical finding.

---

## Accuracy, Capabilities & Limitations

**What the AI CAN Automate (via Browser Automation / MCP):**
- **DOM & Structural Analysis:** The AI analyzes semantic HTML, landmarks, and heading hierarchies via the raw Accessibility Tree.
- **Interactive Keyboard & Focus Traps:** The AI simulates `Tab` key presses to map the focus order mathematically and detect keyboard traps (WCAG 2.1.2) automatically.
- **Automated Reflow Testing (WCAG 1.4.10):** The AI can resize the viewport to 320px and mathematically detect horizontal scroll violations.
- **Theme-Aware Contrast Validation:** The AI can emulate `prefers-color-scheme: dark` to ensure contrast ratios pass in both Light and Dark modes.
- **Reduced Motion Validation (WCAG 2.3.3):** The AI can emulate `prefers-reduced-motion` to ensure animations halt.
- **NVDA Log Analysis:** If provided with an NVDA Speech Viewer log, the AI performs a highly accurate analysis of the screen reader experience.

**What Cannot Be Fully Automated (AI Limitations):**
- **Visual Validation:** Ensure the focus ring moves in a visually logical sequence.
- **Contextual Meaning:** Verify if `alt` text or ARIA labels accurately describe visual intent.
- **Complex Cognitive Interactions:** Checking if a captcha or puzzle makes sense.

---

## 📚 Standard Issue Library

Use these standardized titles and descriptions for recurring patterns:

| Standard Title                                   | Recurring Issue Description                                                   | WCAG SC | Severity | Affected Impairments         |
| :----------------------------------------------- | :---------------------------------------------------------------------------- | :------ | :------- | :--------------------------- |
| **Missing Landmark Label**                       | The `<section>` tag lacks an `aria-label` or `aria-labelledby`.               | 1.3.1   | MINOR    | Visual (Screen Reader)       |
| **Non-Semantic Body Text (Span Soup)**           | Body content wrapped in `<span>` with inline styles instead of `<p>`.         | 1.3.1   | MINOR    | Visual, Cognitive            |
| **Invalid HTML Nesting**                         | Block-level elements (like `<p>`) nested inside a heading tag (e.g. `<h5>`).  | 4.1.1   | SERIOUS  | Visual (Parsing error)       |
| **Empty Spacer Elements**                        | Empty `<p>&nbsp;</p>` or `<div>&nbsp;</div>` used for visual spacing.         | 1.3.1   | MINOR    | Visual (Screen Reader noise) |
| **Invalid Interactive Element (Link as Toggle)** | An `<a>` tag with `href="#"` used for state toggles; missing `role="button"`. | 4.1.2   | SERIOUS  | Visual, Motor (Keyboard)     |
| **Redundant Image Alt Text**                     | Alt text including redundant words like "logo" or "image".                    | 1.1.1   | MINOR    | Visual (Screen Reader noise) |
| **Non-Semantic Eyebrow Text**                    | A `<p>` tag section indicator directly above a heading.                       | 1.3.1   | MINOR    | Visual, Cognitive            |
| **Missing List Semantics**                       | Grouped cards/features marked as `div`s instead of `<ul>`.                    | 1.3.1   | MINOR    | Visual (Screen Reader)       |
| **Fragmented Heading Hierarchy**                 | Skipped heading levels (e.g., H1 -> H5).                                      | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **Duplicate Announcements**                      | Concurrent mobile/desktop containers active in the a11y tree.                 | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **Fragmented Heading Announcement**              | Inline tags (like `<sup>`) causing screen readers to split a heading.         | 1.3.1   | SERIOUS  | Visual (Screen Reader)       |
| **Fake Button (Anchor without Role)**            | Link used as button (`javascript:void(0)`) without keyboard support.          | 4.1.2   | SERIOUS  | Motor, Visual                |
