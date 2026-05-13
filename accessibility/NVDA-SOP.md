# NVDA Speech Logger SOP: Verbatim Evidence for AI Audits

This document defines the standard procedure for using NVDA (NonVisual Desktop Access) to capture speech logs as technical evidence for accessibility remediation reports.

---

## 🛠️ 1. Initial Setup (One-time per Project)

To ensure the AI agent can read your findings, you must redirect the NVDA Speech Logger output to the project's evidence folder.

1.  **Open NVDA Settings:** Press `NVDA + N` -> **Preferences** -> **Settings**.
2.  **Locate Speech Logger:** In the left sidebar, scroll down and select **Speech Logger**.
3.  **Set Output Path:** Paste the project-specific path provided by the AI agent into the **Log File Path** field.
    - _Standard Format:_ `[PROJECT_PATH]\a11y-audits\evidence\nvda-speech.log`
4.  **Configuration:**
    - **Overwrite existing log:** Ensure this is **UNCHECKED** (so we can append multiple pages).
    - **Log speech only:** Checked.

---

## ⌨️ 2. Audit Execution Shortcuts

| Action                | Shortcut              | Description                                                                                                                              |
| :-------------------- | :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| **Toggle Logging**    | `NVDA + Alt + L`      | Starts or stops the speech capture. You should hear a beep.                                                                              |
| **Elements List**     | `NVDA + F7`           | Opens the list of Landmarks, Headings, and Links. Use this to audit the **logical order** and descriptive text of all links on the page. |
| **Link Navigation**   | `K` / `Shift + K`     | Jumps to the next or previous link. Essential for "Link Soup" audits.                                                                    |
| **Visited Link**      | `V` / `Shift + V`     | Jumps to the next or previous visited link.                                                                                              |
| **Read Current Line** | `NVDA + Up Arrow`     | Re-announces the current line to ensure it's logged clearly.                                                                             |
| **Tab Sequence**      | `Tab` / `Shift + Tab` | Move through interactive elements to capture "Focus Announcements".                                                                      |
| **Enter / Space**     | `Enter` / `Space`     | Activates buttons/links. Verify that NVDA announces the state change (e.g., "Expanded").                                                 |
| **Arrow Keys**        | `Arrows`              | Used for navigating custom widgets like Sliders, Tabs, and Carousels.                                                                    |
| **Escape Key**        | `Esc`                 | Must close modals and overlays. Focus MUST return to the triggering element.                                                             |

---

## 🏃 3. The "Standard Audit" Workflow

Follow this sequence for every URL in the project:

1.  **Preparation:** Open the target URL in Chrome/Firefox.
2.  **Start Capture:** Press `NVDA + Alt + L`.
3.  **Linear Sweep:**
    - Use `H` to skip through headings (Check hierarchy).
    - Use `D` to skip through landmarks (Check semantic structure).
    - Use `Tab` to verify all interactive controls.
4.  **Interaction Testing:**
    - Open modals/menus.
    - Submit forms with invalid data (Verify error announcements).
5.  **Stop Capture:** Press `NVDA + Alt + L`.

---

## 🤖 4. AI Handoff Protocol

Once you finish a page, communicate with the AI agent using the following "Handshake":

1.  **Path Confirmation:** Tell the agent: _"The log for [URL] is ready in the evidence folder."_
2.  **Manual Context:** Provide any nuances the logger missed (e.g., _"The focus indicator is missing on the 'Search' input, but NVDA announced it correctly."_)
3.  **Artifact Generation:** Ask the agent: _"Parse the log and generate the remediation findings for this page."_

---

## 💡 Troubleshooting

- **No log generated?** Ensure NVDA was started **after** the Speech Logger add-on was installed.
- **Log is empty?** Check that you toggled the logger **ON** (`NVDA + Alt + L`) before tabbing.
- **Path Error?** Ensure the folder path exists on your Windows filesystem before pasting it into NVDA.
