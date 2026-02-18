# Design: Migrate rmarkdown/xaringan → Quarto

**Date:** 2026-02-18
**Author:** Rizqy Amelia Zein
**Status:** Approved

---

## Goal

Migrate the LVM-CFA workshop website from `rmarkdown` (website) + `xaringan` (slides) to a unified Quarto project, using the `quarto-unair-theme` for reveal.js slides.

---

## Project Structure

```
lvm-cfa/
├── _quarto.yml              # replaces _site.yml
├── index.qmd                # replaces index.Rmd (homepage)
├── slides/
│   ├── materi-lvm-1.qmd     # replaces materi-lvm-1.Rmd
│   ├── materi-lvm-2.qmd
│   ├── materi-lvm-3.qmd
│   └── materi-lvm-4.qmd
├── _extensions/
│   └── unair/               # installed via: quarto add rameliaz/quarto-unair-theme
├── docs/                    # build output (GitHub Pages root, unchanged)
├── dataset-simulasi.R       # unchanged
└── [all data/asset files]   # unchanged
```

---

## `_quarto.yml` Config

- `project: type: website`, `output-dir: docs`
- Navbar mirrors existing `_site.yml` links (HTML slides × 4, datasets × 4, survey)
- PDF slide links **removed** from navbar — reveal.js slides support browser print-to-PDF
- Website theme: `flatly` (Bootstrap 5, same as before)
- All `.qmd` files (index + 4 slides) listed under `project: render:`

---

## Slide Conversion Map (xaringan → Quarto reveal.js)

| xaringan | Quarto reveal.js |
|---|---|
| `---` slide separator | `---` (unchanged) |
| `class: inverse` | `## Title {background-color="#14497F"}` |
| `class: center, middle` | `## {.center}` |
| `.pull-left[]` / `.pull-right[]` | `:::: {.columns}` / `::: {.column width="50%"}` |
| `--` incremental reveal | `::: {.incremental}` or `.fragment` |
| `` `r fa("arrow-circle-right")` `` | Unicode `→` or `{{< fa arrow-circle-right >}}` |
| `` `r emo::ji("wink")` `` | Literal emoji `😉` |
| `.footnote[]` | `^[text]` footnote or `::: {.footnote}` |
| `<center><img ...></center>` | `![](path){fig-align="center" width="X%"}` |
| R code chunks | Unchanged (knitr works in Quarto) |
| Hand-built title slide | Handled by unair theme YAML metadata |
| `library(fontawesome)`, `library(emo)` | Removed from setup chunk |
| Closing xaringan attribution | Updated to reference Quarto + unair theme |

---

## Files to Delete After Migration

- `_site.yml`
- `index.Rmd`
- `slides/materi-lvm-1.Rmd` through `materi-lvm-4.Rmd`
- xaringan-specific assets in `slides/libs/`: `remark-latest.min.js`, `remark-css/`, `animate.css`, `slides.css`, `slides.js`, and all other JS/CSS that came from xaringan (image assets in `slides/libs/` are **kept**)

---

## Approach

**Approach A (Flat / unified):** Single Quarto project at repo root. Website + slides share one `_quarto.yml`. The unair theme extension is installed once at the root via `quarto add`. `quarto render` builds everything to `docs/`.
