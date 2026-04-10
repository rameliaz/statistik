# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Quarto-based workshop website** for a Confirmatory Factor Analysis (CFA) / Latent Variable Modeling (LVM) workshop held at Universitas Negeri Semarang (UNNES). It is a Quarto website outputting to the `docs/` folder for GitHub Pages hosting. Slides use the `unair-revealjs` theme from [quarto-unair-theme](https://github.com/rameliaz/quarto-unair-theme).

## Build Commands

All commands run from the terminal in the project root:

```bash
# Build the entire website (renders all .qmd files to docs/)
quarto render

# Live preview with hot reload
quarto preview

# Render a single slide deck
quarto render slides/materi-lvm-1.qmd
quarto render slides/materi-lvm-2.qmd
quarto render slides/materi-lvm-3.qmd
quarto render slides/materi-lvm-4.qmd

# Simulate workshop datasets (R)
source("dataset-simulasi.R")
```

## Architecture

```
lvm-cfa/
├── index.qmd              # Homepage with embedded YouTube iframes
├── _quarto.yml            # Site config: navbar, output_dir (docs/), cosmo theme
├── _extensions/           # Quarto extensions (committed to repo)
│   ├── rameliaz/unair/    # unair-revealjs slide theme
│   └── quarto-ext/fontawesome/  # {{< fa >}} shortcode support (CDN, no local assets)
├── docs/                  # Build output (GitHub Pages root); committed to repo
│   └── slides/            # Built slide HTML files live here
├── slides/                # Source Quarto slide decks (4 parts)
│   ├── materi-lvm-1.qmd   # Part 1: Introduction to LVM
│   ├── materi-lvm-2.qmd   # Part 2: Correlation
│   ├── materi-lvm-3.qmd   # Part 3: Path models & lavaan syntax
│   ├── materi-lvm-4.qmd   # Part 4: CFA
│   └── libs/              # Static assets (images) referenced by slides; also contains
│                          # unused images — do NOT delete, kept intentionally
├── materials/             # Workshop resource files (datasets, codebooks, etc.)
│                          # Navbar dataset links in _quarto.yml point here
└── dataset-simulasi.R     # Script to simulate workshop practice datasets using simsem/lavaan
```

## Key Conventions

- **Slide format**: All slides use `format: unair-revealjs` (UNAIR brand colors: blue `#14497F`, yellow `#FFCB05`). Two-column layouts use `:::: {.columns}` / `::: {.column width="50%"}` divs. Dark slides use `{background-color="#14497F"}` on `##` headings. FontAwesome icons use `{{< fa icon-name >}}` shortcodes.
- **FontAwesome**: Loaded via cdnjs CDN (FA 6.7.2) — `_extensions/quarto-ext/fontawesome/assets/` does not exist. The `fontawesome.lua` injects a `<link>` tag pointing to the CDN on first use. Do not add local FA asset files.
- **Dataset files**: Stored in `materials/`. Navbar links in `_quarto.yml` use `materials/` prefix (e.g. `materials/corr.jasp`). Do not place dataset files at the project root.
- **Site output**: `_quarto.yml` sets `output-dir: docs` and `project.render` to `*.qmd` and `slides/*.qmd` only. The `docs/` directory is the GitHub Pages root.
- **Encoding**: UTF-8 throughout. Slide content mixes Indonesian and English.
- **R packages used**: `lavaan`, `simsem` (for dataset simulation only). Slides do not execute R code during render — all code blocks in slides are display-only (`#| eval: false`).
- **Dataset simulation**: `dataset-simulasi.R` uses `lavaan` + `simsem` to generate synthetic CFA datasets. The write path at the bottom of that script is hardcoded to a local `D:/Drive/...` path and must be updated before running.
- **No automated tests** — this is a teaching material repository.

## Content Language

Primary content language is **Indonesian (Bahasa Indonesia)**. R code and technical terms remain in English.
