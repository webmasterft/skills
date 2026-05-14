# Master Technical Remediation Report: SEIUMB Home Page
**Audit Date:** May 12, 2026
**Target URL:** [https://www.seiumb.com/](https://www.seiumb.com/)

---

## 🏛️ Component: Search & Header (Minor Issues First)

### Missing Landmark Label
- **Severity:** MINOR
- **Affected Impairments:** Visual (Screen Reader)
- **Issue:** The `<section>` container for the search results lacks an `aria-label` or `aria-labelledby`, preventing screen reader users from identifying the landmark.
- **Successful criteria:** [1.3.1 Info and Relationships](https://www.w3.org/TR/WCAG21/#info-and-relationships)
- **Suggested remediation:** Add `aria-label="Search results"` to the section tag.
- **DOM Evidence:**
  ```html
  <section class="search-container">...</section>
  ```

### Redundant Image Alt Text
- **Severity:** MINOR
- **Affected Impairments:** Visual (Screen Reader noise)
- **Issue:** The footer logo has alt text "Logo SEIU," which is redundant as the screen reader already announces the element as an image.
- **Successful criteria:** [1.1.1 Non-text Content](https://www.w3.org/TR/WCAG21/#non-text-content)
- **Suggested remediation:** Change alt text to "SEIU Member Benefits" or hide if decorative.
- **DOM Evidence:**
  ```html
  <img src="/footer-logo.png" alt="Logo SEIU">
  ```

---

## 🏛️ Component: Navigation & Links (Moderate)

### Ambiguous Link Purpose
- **Severity:** MODERATE
- **Affected Impairments:** Visual, Cognitive
- **Issue:** Multiple links labeled "Learn More" and "Explore" provide no context for screen reader users navigating by link lists.
- **Successful criteria:** [2.4.4 Link Purpose (In Context)](https://www.w3.org/TR/WCAG21/#link-purpose-in-context)
- **Suggested remediation:** Use `aria-label` to specify the destination (e.g., `aria-label="Learn more about Auto Insurance"`).
- **DOM Evidence:**
  ```html
  <a href="/auto" class="link">Learn More</a>
  ```

### Small Interactive Target (Touch Targets)
- **Severity:** MODERATE
- **Affected Impairments:** Motor
- **Issue:** Social media icons and the "Skip to Content" link measure below the mandatory 24x24px threshold.
- **Successful criteria:** [2.5.8 Target Size (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
- **Suggested remediation:** Increase hit area to at least 24x24px using padding.
- **DOM Evidence:**
  ```html
  <a class="social-fb" href="...">...</a> <!-- 11x11px -->
  ```

---

## 🏛️ Component: Main Content & Visuals (Serious)

### Fragmented Heading Hierarchy
- **Severity:** SERIOUS
- **Affected Impairments:** Visual (Screen Reader), Cognitive
- **Issue:** The page skips logical levels, starting with `H4` and `H5` before reaching the main `H1`.
- **Successful criteria:** [1.3.1 Info and Relationships](https://www.w3.org/TR/WCAG21/#info-and-relationships)
- **Suggested remediation:** Restructure to H1 -> H2 -> H3 order.
- **DOM Evidence:**
  ```html
  <h4 class="eyebrow">Welcome</h4>
  <h1 class="hero-title">SEIU Member Benefits</h1>
  ```

### Color Contrast Violation (Aquamarine)
- **Severity:** SERIOUS
- **Affected Impairments:** Visual
- **Issue:** Primary action buttons (`#0099B2`) have a contrast ratio of **3.33:1** against white text, failing the **4.5:1** requirement.
- **Successful criteria:** [1.4.3 Contrast (Minimum)](https://www.w3.org/TR/WCAG21/#contrast-minimum)
- **Suggested remediation:** Darken the color to `#007487` or use dark text on the light background.
- **DOM Evidence:**
  ```html
  <button class="btn-primary" style="background-color: #0099B2; color: #FFFFFF;">Get a Quote</button>
  ```

---

## 🏛️ Component: Mobile Navigation (Blocker)

### Missing "Escape" Key Support
- **Severity:** BLOCKER
- **Affected Impairments:** Motor, Cognitive
- **Issue:** The mobile menu overlay cannot be closed using the 'Escape' key, forcing keyboard users to tab through the entire menu to exit.
- **Successful criteria:** [2.1.1 Keyboard](https://www.w3.org/TR/WCAG21/#keyboard)
- **Suggested remediation:** Add a `keydown` listener to the document that triggers the close function when `event.key === 'Escape'`.
- **DOM Evidence:**
  ```javascript
  // Missing listener in navigation.js
  ```

### Focus Trap Failure (Mobile Menu)
- **Severity:** BLOCKER
- **Affected Impairments:** Visual (Screen Reader), Motor
- **Issue:** Focus is not trapped within the mobile menu. Tabbing past the last item moves focus to hidden background elements.
- **Successful criteria:** [2.4.3 Focus Order](https://www.w3.org/TR/WCAG21/#focus-order)
- **Suggested remediation:** Implement a focus trap utility to cycle focus between the first and last focusable elements of the menu.
- **DOM Evidence:**
  ```html
  <nav id="mobile-nav" class="open">...</nav>
  ```
