# 🎨 Fritzing-Parts: MT6701 Magnetic Encoder Guide

A comprehensive, step-by-step workflow for creating high-quality custom components in Fritzing, specifically addressing the common SVG rendering and XML font bugs.

---

<table width="100%">
  <tr>
    <td width="50%" align="left" valign="middle">
      <h2>🚀 The Backstory</h2>
    </td>
    <td width="50%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/1c865b8d-d03e-4994-b2b1-2320f37c6ebe" alt="MT6701 Fritzing Part Preview" width="150" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>
        Creating new parts in Fritzing is rarely straightforward. Most online tutorials use outdated versions of Inkscape or overlook the strict XML requirements Fritzing demands. When I needed a clean, accurate part for the <b>MT6701 Magnetic Encoder</b>, I spent a full day troubleshooting why fonts looked wrong and colors wouldn't render.
      </p>
      <p>
        This repository serves as a "Hard-Knocks" guide, documenting the exact settings and XML edits required to make a part look professional and function correctly in both Breadboard and PCB views.
      </p>
      <blockquote>
        <b>Pro-Tip:</b> A <code>.fzpz</code> file is actually just a renamed <code>.zip</code> archive. If you need to fix or study an existing part, rename the extension to <code>.zip</code>, extract it, and you can access the XML and SVG source files directly.
      </blockquote>
    </td>
  </tr>
</table>

---

## 🛠️ Quick-Fix Troubleshooting
If your part looks "broken" in Fritzing, check this table first:

| Symptom | Likely Cause | Fix |
| :--- | :--- | :--- |
| **Giant/Tiny Text** | Inkscape `px` units | Delete "px" from `font-size` in XML Editor |
| **Black Text Only** | Hardcoded `fill` value | Remove the specific `fill` line in the XML tree |
| **Single-Sided PCB** | Incorrect Layering | Nest `copper1` group inside the `copper0` group |
| **Invisible Part** | Missing Layer ID | Ensure the top-level group ID matches the `.fzp` (e.g., `breadboard`) |

---

## ✨ Key Technical Solutions

* **The "PX" Font Fix:** Solves the issue where text appears at the wrong size due to Inkscape’s default pixel units. Fritzing's engine expects unit-less values.
* **Color Rendering Fix:** Identifies and removes hard-coded XML fill values that force text to appear black in Fritzing.
* **Vector Optimization:** Techniques for saving SVGs in the specific format Fritzing prefers for its rendering engine (Plain SVG or Optimized SVG).
* **Transparency Handling:** A workflow for using PNG-to-Bitmap tracing to maintain transparency in custom part shapes without adding heavy path data.

---

## 📐 The 4-Stage Workflow

The full process is detailed in the included `Fritzing New Parts.doc`, but the core stages are:

### Stage 1: Template Selection
Start with a generic IC template within Fritzing. This provides the foundational metadata structure before you begin visual customization. It is much easier to modify an existing `.fzp` than to write one from scratch.

### Stage 2: XML & Metadata Editing
Rename your files and manually edit the `.fzp` (Fritzing Part) XML file to define the connections and pin mapping. 

**Note:** If your part has multiple pins that share the same net (like multiple GND pins), you can define a **Bus** in the `.fzp` file to link them internally.

<table width="100%">
  <tr>
    <td width="50%" align="left" valign="middle">
      <h3>Stage 3: Breadboard SVG Design</h3>
    </td>
    <td width="50%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/0a2c6a35-7743-4e2b-aba9-47cb5250f7af" alt="Breadboard SVG Editing" width="150" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>Designing the visual look of the component. This is where most font issues occur. Ensure you group your elements and set the Layer ID to <code>breadboard</code> in the Inkscape object properties.</p>
    </td>
  </tr>
  <tr><td colspan="2"><hr></td></tr>
  <tr>
    <td width="50%" align="left" valign="middle">
      <h3>Stage 4: PCB SVG Design</h3>
    </td>
    <td width="50%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/0a2c6a35-7743-4e2b-aba9-47cb5250f7af" alt="PCB SVG Layout" width="150" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>Creating the footprint for manufacturing. This requires precise pad spacing (usually 0.1 inch for headers).</p>
      <p><b>Critical Requirement:</b> To ensure dual-side connectivity, you must follow a specific nesting structure in your layers: The <code>copper1</code> group (top layer) must physically contain the <code>copper0</code> group (bottom layer) within the SVG XML tree.</p>
    </td>
  </tr>
</table>

---

## 📐 Solving the Inkscape Bug

Fritzing's rendering engine often struggles with modern Inkscape outputs. If your part looks strange, follow these XML Editor fixes:



<table width="100%">
  <tr>
    <td width="50%" align="left" valign="middle">
      <h3>1. The Font-Size Bug</h3>
    </td>
    <td width="50%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/8f07b2f2-e7df-45d7-867e-32d66262723b" alt="Inkscape XML Editor Font Fix" width="150" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>If your fonts appear massive or tiny, open the <b>XML Editor (Edit -> XML Editor)</b> in Inkscape. Find any <code>font-size</code> attribute ending in <code>px</code> and delete it. Fritzing requires unit-less values for correct scaling.</p>
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td width="50%" align="left" valign="middle">
      <h3>2. The Black Text Bug</h3>
    </td>
    <td width="50%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/8f07b2f2-e7df-45d7-867e-32d66262723b" alt="Inkscape XML Color Fix" width="150" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>If your text appears black regardless of the color you set, find the <code>fill</code> value in the XML tree. Deleting the fixed value line allows Fritzing to use the intended color profile.</p>
    </td>
  </tr>
</table>

---

## 📜 Resources & Tools

* **FritzingCheckApp:** Highly recommended to run your SVG files through this tool to clean up common metadata errors before importing.
* **Inkscape:** Use "Optimized SVG" or "Plain SVG" settings during export to minimize compatibility issues.

---

<footer align="center">
  <p>© 2026 MatsRobot | Part of the Open Source Robotics Initiative</p>
  <p><small>Copyright (c) 2026 | Licensed under the <a href="https://github.com/MatsRobot/matsrobot.github.io/blob/main/LICENSE" style="color: #6a737d;">MIT License</a></small></p>
</footer>
