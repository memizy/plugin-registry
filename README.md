<div align="center">

# 🧩 Memizy Plugin Registry
**The Official Directory of OQSE Applications & Plugins**

![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

<br>

Welcome to the **Plugin Registry**, the central hub where developers publish their tools (players, editors, validators) for the [Memizy Ecosystem](https://github.com/memizy/memizy).

</div>

---

## ⚙️ How It Works (Capability-Based Matching)

The Memizy ecosystem is highly modular. Instead of building one massive application that understands every possible question type (Flashcards, Multiple Choice, 3D Anatomy models, Chess puzzles), Memizy relies on lightweight, sandboxed plugins.

This repository contains a single file: `index.json`. 
This file is an array of **Application Manifests**. Every time a user opens a study set (e.g., an Anki-style deck or a Math quiz), the Memizy app checks this registry to find a plugin whose declared **Capabilities** match the **Requirements** of the study set.

---

## 🚀 How to Publish Your Plugin

Have you built a cool new quiz player or a visual editor? Adding it to the Memizy ecosystem is simple:

1. Build your plugin using the [Memizy Plugin SDK](https://github.com/memizy/plugin-api).
2. Host your plugin's compiled `.html` or `.js` file somewhere accessible (e.g., GitHub Pages, Vercel, or raw via jsDelivr).
3. Fork this `plugin-registry` repository.
4. Add your **Application Manifest** object to the array in `index.json`.
5. Open a **Pull Request**.

Once merged, the Memizy host application will automatically discover your plugin and use it whenever a compatible study set is loaded!

---

## 🛠️ Data Structure (`index.json`)

The registry is a JSON array containing Manifest objects defined by the [OQSE Specification](https://github.com/memizy/oqse-specification). 

Here is an example of what your entry in the `index.json` array should look like. This example shows a plugin designed strictly for Multiple-Choice Questions (MCQ):

```json
[
  {
    "$schema": "[https://raw.githubusercontent.com/memizy/oqse-specification/main/schemas/manifest/v0.json](https://raw.githubusercontent.com/memizy/oqse-specification/main/schemas/manifest/v0.json)",
    "version": "1.0",
    "id": "[https://memizy.com/plugins/medical-drill-player](https://memizy.com/plugins/medical-drill-player)",
    "appName": "Memizy Medical Drill Player",
    "description": "Fast, distraction-free player optimized for MCQ exams.",
    "author": "Memizy Team",
    "studyMode": "drill",
    "capabilities": {
      "actions": ["render"],
      "types": ["mcq-single", "mcq-multi"],
      "assets": null,
      "features": ["markdown"],
      "itemProperties": ["explanation", "incorrectFeedback"]
    }
  }
]
