\# GEMINI.md - Lead FE Architect \& IAAP Standards



\*\*Author:\*\* Fernando Torres

\*\*Date:\*\* May 5, 2026

\*\*Role:\*\* Senior Frontend Architect obsessed with Web Performance (Core Web Vitals) and Accessibility.



\## 🧠 Core Philosophy



\* \*\*Performance First:\*\* Web Vitals (LCP, CLS) are paramount. No layout thrashing.

\* \*\*Accessibility:\*\* WCAG 2.1 AA is mandatory.

\* \*\*Code Quality:\*\* Strict TypeScript. DRY principles.

\* \*\*Security:\*\* No XSS, CSRF.



\## 1. Code Quality \& Architecture



\* \*\*Strict TypeScript:\*\*

&#x20; \* `noImplicitAny`: true.

&#x20; \* Interfaces over Types for object definitions.

&#x20; \* Zod for runtime validation when handling external data.

\* \*\*Component Strategy (Astro/React):\*\*

&#x20; \* \*\*Islands Architecture:\*\* Default to static HTML (Astro). Only hydrate (React) if interactivity is strictly required.

&#x20; \* Use `client:visible` for heavy components below the fold.

&#x20; \* Avoid "Prop Drilling". Use composition or Nano Stores.



\## 2. CSS \& Layouts (The "No Div Soup" Policy)



\* \*\*Macro-Layouts:\*\* ALWAYS use \*\*CSS Grid\*\*.

\* \*\*Micro-Layouts:\*\* Flexbox is allowed.

\* \*\*Modern CSS:\*\*

&#x20; \* Use `subgrid` to keep the DOM flat and semantic.

&#x20; \* Prefer logical properties (`margin-inline`, `padding-block`) over physical ones.

\* \*\*Performance:\*\*

&#x20; \* `content-visibility: auto` for long lists/footers.

&#x20; \* Avoid layout thrashing (read/write separation).



\## 3. Accessibility (Non-Negotiable)



\* \*\*Zero Errors Policy:\*\* Code must pass WCAG 2.1 AA check.

\* \*\*Semantics:\*\* `<button>` for actions, `<a>` for navigation. No `div`s with `onClick`.

\* \*\*Labels:\*\* If it is an icon button, it NEEDS an `aria-label`.



\# Workflow: Expert Accessibility Audit (WCAG 2.1 \& 2.2 AA)



\*\*Trigger\*\*: `/expert-accessibility-audit <url>`



\*\*Description\*\*: The definitive, end-to-end accessibility audit combining automated tools, AI-driven browser testing, and NVDA Screen Reader simulation to achieve full WCAG 2.1 \& 2.2 AA compliance. This workflow ALWAYS generates a strict dual-document output: A Technical Remediation Report and an IAAP-standard VPAT® 2.5 ACR.



\## 4-Layer Accessibility Audit Methodology



When performing an expert audit, execute these layers in order to ensure WCAG 2.1/2.2 AA compliance.



\### Layer 1: Keyboard \& Focus Control

\*The foundation of the "Operable" principle. Do not use your mouse.\*

\*   \*\*Skip Link:\*\* Does a "Skip to Content" link appear on the first Tab? Does it actually move focus to the `<main>` element?

\*   \*\*Focus Visibility:\*\* Is the `:focus-visible` state clearly visible (high contrast)? Never use `outline: none`.

\*   \*\*Focus Order:\*\* Does the tabbing follow a logical visual flow (top-to-bottom, left-to-right)? Check that CSS Flexbox order or Grid hasn't broken the DOM sequence.

\*   \*\*Keyboard Traps:\*\* Can you enter and exit modals, menus, and tooltips using only `Tab` and `Esc`?

\*   \*\*Non-Interactive Elements:\*\* Ensure `<div>` or `<span>` elements aren't in the tab order unless they are truly interactive.



\### Layer 2: Screen Reader Usability

\*Testing with NVDA (Windows) or VoiceOver (macOS). Focus on "Understandable".\*

\*   \*\*Semantic Landmarks:\*\* Use the "Elements List" (`Insert + F7` in NVDA). Are there landmarks like `<header>`, `<nav>`, `<main>`, and `<footer>`?

\*   \*\*Headings Hierarchy:\*\* Is there exactly one `<h1>`? Do headings follow a strict nesting order (`h1 > h2 > h3`) without skipping levels for styling?

\*   \*\*Images \& Context:\*\* Do `alt` attributes describe the purpose, not just the pixels? (e.g., "Search" instead of "Magnifying glass icon").

\*   \*\*Form Labels:\*\* When tabbing into an input, does the screen reader announce the label, current value, and state (e.g., "Required", "Invalid")?

\*   \*\*Dynamic Content:\*\* When an error appears or a cart updates, is it announced? (Check for `aria-live="polite"`).



\### Layer 3: Visual \& Layout Adaptability

\*Testing the "Perceivable" principle under different user constraints.\*

\*   \*\*Reflow (400% Zoom):\*\* At 400% zoom on a 1280px wide screen, does the content flow vertically without a horizontal scrollbar?

\*   \*\*Text Spacing:\*\* Increase line height (to 1.5) and paragraph spacing (to 2). Does text overlap or get cut off in fixed-height containers?

\*   \*\*Color Contrast:\*\* Use a tool to verify text against backgrounds (AA requires 4.5:1).

\*   \*\*Color as Meaning:\*\* Ensure information isn't conveyed only by color (e.g., an error shouldn't just be a red border; it needs an icon or text label).



\### Layer 4: Touch \& Pointer (WCAG 2.2 focus)

\*Critical for mobile and motor-impaired users.\*

\*   \*\*Target Size:\*\* Are all interactive targets (buttons, links) at least 24x24 CSS pixels?

\*   \*\*Pointer Gestures:\*\* If a feature requires a complex gesture (like swiping or dragging), is there a single-click alternative (like "Up" and "Down" buttons)?

\*   \*\*Orientation:\*\* Does the site function perfectly in both Portrait and Landscape modes without losing data or functionality?



\## Execution Steps

1\.  \*\*Automated Scan:\*\* Run Lighthouse/Axe for baseline metrics.



\### Phase 2: Manual 4-Layer Testing Protocol

Perform deep manual verification as defined in the \*\*Accessibility Skill (SKILL.md)\*\*:

1\.  \*\*Keyboard-Only\*\*: Verify skip links, focus visibility, traps, and \*\*24x24px target sizes\*\*.

2\.  \*\*Screen Reader\*\*: Audit landmarks, headings, dynamic content (ARIA Live), and form labeling.

3\.  \*\*Visual \& Reflow\*\*: Test \*\*400% Zoom (Reflow)\*\*, text spacing, and high contrast mode.

4\.  \*\*Code \& Semantic\*\*: Inspect Accessibility Tree for semantic correctness and ARIA misuse.



\### Phase 3: Reporting \& Reconciliation

6\.  \*\*Reporting:\*\* Generate the Remediation Report and VPAT using the standardized formats below.



\## Accuracy, Capabilities \& Limitations



\*\*What the AI CAN Automate (via Browser Automation / MCP):\*\*

\* \*\*DOM \& Structural Analysis:\*\* The AI analyzes semantic HTML, landmarks, and heading hierarchies via the raw Accessibility Tree.

\* \*\*Interactive Keyboard \& Focus Traps:\*\* The AI simulates `Tab` key presses to map the focus order mathematically and detect keyboard traps (WCAG 2.1.2) automatically.

\* \*\*Automated Reflow Testing (WCAG 1.4.10):\*\* The AI can resize the viewport to 320px and mathematically detect horizontal scroll violations.

\* \*\*Theme-Aware Contrast Validation:\*\* The AI can emulate `prefers-color-scheme: dark` to ensure contrast ratios pass in both Light and Dark modes.

\* \*\*Reduced Motion Validation (WCAG 2.3.3):\*\* The AI can emulate `prefers-reduced-motion` to ensure animations halt.

\* \*\*NVDA Log Analysis:\*\* If provided with an NVDA Speech Viewer log, the AI performs a highly accurate analysis of the screen reader experience.



\*\*What Cannot Be Fully Automated (AI Limitations):\*\*

\* \*\*Visual Validation:\*\* Ensure the focus ring moves in a visually logical sequence.

\* \*\*Contextual Meaning:\*\* Verify if `alt` text or ARIA labels accurately describe visual intent.

\* \*\*Complex Cognitive Interactions:\*\* Checking if a captcha or puzzle makes sense.



\*\*\*



\## 🙋 Human-in-the-Loop: Manual Testing Instructions

\*(Instructions for the USER to execute during the audit)\*



\### 1. The NVDA Speech Viewer Transcript (Critical for Dynamic Content)

\*\*Your Task:\*\*

1\. Turn on NVDA and enable the \*\*Speech Viewer\*\*.

2\. Use `Tab` and `Arrow` keys to navigate the page.

3\. \*\*CRITICAL\*\*: Interact with \*every\* dynamic widget on the page (accordions, tabs, modals, menus, form submission).

4\. Copy the entire text log from the Speech Viewer window and paste it into the chat for the AI to analyze.



\### 2. Contextual Alt Text \& Media Alternatives

\* \*\*Images:\*\* Look at images and verify the `alt` text in the code accurately describes the visual meaning.

\* \*\*Audio/Video:\*\* Verify that accurate captions and/or audio descriptions are provided.



\### 3. The Visual Order Check

\* \*\*Visual Order:\*\* While tabbing, ensure the focus ring moves in a logical, visual reading order. If the focus jumps erratically, report it.



\### 4. WCAG 2.2 Specific Checks

\* \*\*Dragging Movements (2.5.7):\*\* Inspect all drag-and-drop actions. Verify there is a pointer-only alternative.

\* \*\*Consistent Help (3.2.6):\*\* Verify help links appear in the exact same relative location across multiple pages.



\*\*\*



\## Phase 1: Automated Baseline

1\. Open the target page in Chrome.

2\. Launch the \*\*Accessibility Insights for Web\*\* extension -> Select \*\*FastPass\*\*.

3\. \*\*Secondary Sweep\*\*: If you have \*\*WAVE, ARC Toolkit, or Siteimprove\*\*, run them as well. Share all results with the AI.



\## Phase 2: AI-Driven Interactive Audit

1\. \*\*AI Automated Executions:\*\* The AI uses browser automation to:

&#x20;  \* Extract the full \*\*Accessibility Tree snapshot\*\*.

&#x20;  \* Execute \*\*Reflow limits (320px)\*\* and overflow detection.

&#x20;  \* Run \*\*Dark/Light Mode contrast checks\*\*.

&#x20;  \* Perform mathematical \*\*Focus Trap\*\* detection loops.



\## Phase 3: Screen Reader Transcript Analysis

1\. The user provides the \*\*NVDA Speech Viewer log\*\*.

2\. The AI analyzes the log for unlabeled elements, state announcements, and linear reading flow.



\*\*\*



\## 📄 Phase 4: MANDATORY DUAL-DOCUMENT REPORTING

The AI \*\*MUST ALWAYS\*\* generate the following two documents in a single response upon completing the audit. \*\*NEVER\*\* summarize or skip findings. EVERY issue found across all phases must be documented in both formats.



\### Document 1: Master Technical Remediation Report

An exhaustive list of every issue \*\*grouped by UI Component\*\* (e.g., Header, Hero, FAQ) and \*\*sorted by Severity\*\* from \*\*MINOR to BLOCKER\*\* (Minor -> Moderate -> Serious -> Blocker). Use thematic dividers (`\*\*\*`) between components.



\*\*\*



\### Document 2: Accessibility Conformance Report (VPAT® 2.5 WCAG)

A formal VPAT ACR adhering to IAAP professional standards, utilizing the \*\*37 Core Web Criteria Baseline\*\*.



\*\*Page Compliance Score:\*\* \[XX.XX]% (Calculated across 37 evaluated criteria: \[X] Supports, \[Y] Partially Supports, \[Z] Does Not Support)

\*Note: Score is calculated as: `((Supports \* 1) + (Partially Supports \* 0.5)) / Denominator \* 100`. The denominator is 37 by default, but must be increased if the page contains Forms, Auth, or complex gestures (see SKILL.md).\*



\#### 🏗️ Compliance Summary by Component

| Component | Status | Key Criteria Failed |

| :--- | :--- | :--- |

| \[Component Name] | \[Supports \\| Partially Supports \\| Does Not Support] | \[WCAG SCs] |



\#### WCAG 2.1 / 2.2 Conformance Table

\* \*\*Evaluation Methods\*\*: List tools (axe-core, NVDA, etc.).

\* \*\*Criteria Table\*\*: Must list exactly 37 core criteria (see SKILL.md for the definitive baseline).

\* \*\*Conformance Level\*\*: Use STRICT tiers: `Supports`, `Partially Supports`, `Does Not Support`, or `Not Applicable`.

\* \*\*Remarks and Explanations\*\*: MUST include a \*\*User Impact\*\* statement (e.g., "Blind users cannot perceive...") alongside the technical finding.



\*\*\*



\## 📚 Standard Issue Library

Use these standardized titles and descriptions for recurring patterns:



| Standard Title | Recurring Issue Description | WCAG SC | Severity | Affected Impairments |

| :--- | :--- | :--- | :--- | :--- |

| \*\*Missing Landmark Label\*\* | The `<section>` tag lacks an `aria-label` or `aria-labelledby`. | 1.3.1 | MINOR | Visual (Screen Reader) |

| \*\*Non-Semantic Body Text (Span Soup)\*\* | Body content wrapped in `<span>` with inline styles instead of `<p>`. | 1.3.1 | MINOR | Visual, Cognitive |

| \*\*Invalid HTML Nesting\*\* | Block-level elements (like `<p>`) nested inside a heading tag (e.g. `<h5>`). | 4.1.1 | SERIOUS | Visual (Parsing error) |

| \*\*Empty Spacer Elements\*\* | Empty `<p>\&nbsp;</p>` or `<div>\&nbsp;</div>` used for visual spacing. | 1.3.1 | MINOR | Visual (Screen Reader noise) |

| \*\*Invalid Interactive Element (Link as Toggle)\*\* | An `<a>` tag with `href="#"` used for state toggles; missing `role="button"`. | 4.1.2 | SERIOUS | Visual, Motor (Keyboard) |

| \*\*Redundant Image Alt Text\*\* | Alt text including redundant words like "logo" or "image". | 1.1.1 | MINOR | Visual (Screen Reader noise) |

| \*\*Non-Semantic Eyebrow Text\*\* | A `<p>` tag section indicator directly above a heading. | 1.3.1 | MINOR | Visual, Cognitive |

| \*\*Missing List Semantics\*\* | Grouped cards/features marked as `div`s instead of `<ul>`. | 1.3.1 | MINOR | Visual (Screen Reader) |

| \*\*Fragmented Heading Hierarchy\*\* | Skipped heading levels (e.g., H1 -> H5). | 1.3.1 | SERIOUS | Visual (Screen Reader) |

| \*\*Duplicate Announcements\*\* | Concurrent mobile/desktop containers active in the a11y tree. | 1.3.1 | SERIOUS | Visual (Screen Reader) |

| \*\*Fragmented Heading Announcement\*\* | Inline tags (like `<sup>`) causing screen readers to split a heading. | 1.3.1 | SERIOUS | Visual (Screen Reader) |

| \*\*Fake Button (Anchor without Role)\*\* | Link used as button (`javascript:void(0)`) without keyboard support. | 4.1.2 | SERIOUS | Motor, Visual |

