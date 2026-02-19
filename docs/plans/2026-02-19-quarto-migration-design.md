# Quarto Migration Design

**Date:** 2026-02-19
**Author:** Rizqy Amelia Zein
**Status:** Approved

## Overview

Convert the lvm-cfa workshop website from `rmarkdown`/`xaringan` (2019/2020 stack) to Quarto. Slides will use the `quarto-unair-theme` (`unair-revealjs` format). The site continues to publish from `docs/` to GitHub Pages without reconfiguration.

## Approach

In-place conversion (Option A): replace `.Rmd` files with `.qmd` equivalents, replace `_site.yml` with `_quarto.yml`, delete old source files. Git history preserves rollback safety.

## Project Structure

```
lvm-cfa/
├── _quarto.yml              # replaces _site.yml
├── index.qmd                # replaces index.Rmd
├── slides/
│   ├── materi-lvm-1.qmd    # replaces materi-lvm-1.Rmd
│   ├── materi-lvm-2.qmd    # replaces materi-lvm-2.Rmd
│   ├── materi-lvm-3.qmd    # replaces materi-lvm-3.Rmd
│   └── materi-lvm-4.qmd    # replaces materi-lvm-4.Rmd
└── _extensions/unair/       # installed via: quarto add rameliaz/quarto-unair-theme
```

**Output directory:** `docs/` (unchanged, GitHub Pages continues to work)

**Files deleted:** `_site.yml`, `index.Rmd`, `slides/*.Rmd`, `docs/slides/*.Rmd`

## Configuration

### `_quarto.yml`
- Project type: `website`, `output-dir: docs`
- Website theme: `cosmo` (Bootswatch)
- Navbar: same structure as current `_site.yml` — left (author link, GitHub icon), right (Salindia HTML, Salindia PDF, Dataset, Survei menus)

### Slides YAML
```yaml
format: unair-revealjs
```
Installed via `quarto add rameliaz/quarto-unair-theme`.

## Conversion Mapping

| xaringan / rmarkdown | Quarto revealjs |
|---|---|
| `output: xaringan::moon_reader` | `format: unair-revealjs` |
| `chakra: libs/remark-latest.min.js` | removed |
| `css: ["default", "rladies", "rladies-fonts"]` | removed (theme handles styling) |
| `seal: false` | `title-slide-attributes:` in YAML |
| `class: inverse, middle` on slide | `{background-color="#14497F"}` on `##` heading |
| `class: center, middle` | `::: {.center}` div or slide attribute |
| `` `r fa("icon-name")` `` | `{{< fa icon-name >}}` shortcode |
| `---` slide separator | kept as-is |
| `r emo::ji("...")` | direct Unicode emoji |
| `libs/` local images | kept in `slides/libs/`, paths unchanged |

## PDF Slides

Both HTML and PDF navbar links are retained. PDF export uses:
```bash
quarto render slides/materi-lvm-1.qmd --to pdf
```
PDF files output to `docs/slides/materi-lvm-{1,2,3,4}.pdf`.

## Build Workflow

```bash
# One-time setup
quarto add rameliaz/quarto-unair-theme

# Build entire site
quarto render

# Live preview
quarto preview

# Single slide deck
quarto render slides/materi-lvm-1.qmd
```

## R Packages

Still required: `lavaan`, `simsem`, `tidyverse`, `fontawesome` (for any remaining inline R use).
No longer required: `xaringan`, `emo` (emoji now inline Unicode).

## Out of Scope

- Content updates (dates, JASP version references, references list)
- `dataset-simulasi.R` hardcoded path fix
- Migrating `tugas/` folder (not part of current site build)
