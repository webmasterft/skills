---
description: iaap
---

# GEMINI.md - Lead FE Architect & IAAP Standards

**Author:** Fernando Torres
**Role:** Senior Frontend Architect obsessed with Accessibility & Clean Code.

## 🧠 Core Philosophy

- **Accessibility First:** WCAG 2.1 & 2.2 AA compliance is mandatory for all projects.
- **Code Quality:** Strict TypeScript. DRY principles.
- **No Div Soup**: Use semantic HTML5 elements by default.
- **Performance**: High-performance, accessible components with zero layout thrashing.

## 1. Code Quality & Architecture

- **Strict TypeScript:** `noImplicitAny: true`, Interfaces over Types, and Zod for validation.
- **Component Strategy (Astro/React):** Islands Architecture by default. Only hydrate (React) if interactivity is strictly required.

## 2. CSS & Layouts (The "No Div Soup" Policy)

- **Macro-Layouts:** ALWAYS use **CSS Grid**.
- **Micro-Layouts:** Flexbox is allowed.
- **Modern CSS:** Use `subgrid` to keep the DOM flat and semantic. Prefer logical properties over physical ones.

## 3. Accessibility (Non-Negotiable)

- **Zero Errors Policy:** Every component must pass WCAG 2.1 & 2.2 AA standards.
- **Semantics:** `<button>` for actions, `<a>` for navigation. No `div`s with `onClick`.
- **Labels:** Icon buttons REQUIRE `aria-label`.

---

# Workflow Trigger: Expert Accessibility Audit

**Command:** `/iaap <url>`

## Phase 0: Project Initialization (Mandatory)

Before the audit begins, the agent MUST:
1.  **Identify Project Path:** Ask the user for the client project root (e.g., `C:/oshyn/seiumb`).
2.  **Scaffold Workspace:** Execute the following directory structure if it doesn't exist:
    - `[PROJECT_PATH]/a11y-audits/evidence/`
    - `[PROJECT_PATH]/a11y-audits/reports/`
3.  **Establish Evidence Pipeline:** Instruct the user to set their **NVDA Speech Logger** to:
    `[PROJECT_PATH]\a11y-audits\evidence\nvda-speech.log`
4.  **Confirm Readiness:** Wait for the user to confirm that the environment is set up.

## Phase 1: Execution

Once initialized, the agent executes the **5-Layer Audit SOP** defined in the **[Accessibility Skill (SKILL.md)](./SKILL.md)** for each URL provided.

The audit will result in a modular output:
1. **Master Technical Remediation Report** (Located in `reports/master-report.md`)
2. **Page-Specific Finding Artifacts** (Located in `reports/url-slug.md`)
3. **VPAT® 2.5 ACR** (Located in `reports/vpat.md`)

Follow the templates and sorting logic defined in **[REPORTING.md](./REPORTING.md)**.
