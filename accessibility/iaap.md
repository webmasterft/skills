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

**Instruction:** When this command is triggered, the agent MUST execute the **5-Layer Audit SOP** defined in the **[Accessibility Skill (SKILL.md)](./SKILL.md)**.

The audit will result in a dual-document output:
1. **Master Technical Remediation Report** (Sorted Minor to Blocker)
2. **VPAT® 2.5 ACR** (Based on the 37 Core Criteria Baseline)

Follow the templates defined in **[REPORTING.md]( ./REPORTING.md)**.
