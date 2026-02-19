# Quarto Migration Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Convert the lvm-cfa rmarkdown/xaringan workshop site to Quarto, using the `unair-revealjs` theme for slides and `cosmo` theme for the website, keeping `docs/` as the output directory.

**Architecture:** In-place conversion — `.Rmd` files replaced by `.qmd` equivalents, `_site.yml` replaced by `_quarto.yml`. Old files deleted after conversion. Git history provides rollback safety.

**Tech Stack:** Quarto, `unair-revealjs` (rameliaz/quarto-unair-theme), `fontawesome` Quarto extension, R (`lavaan`, `tidyverse`), GitHub Pages via `docs/`.

---

## Global Conversion Rules

Apply these rules in every slide file:

| Old (xaringan) | New (Quarto revealjs) |
|---|---|
| `` `r fa("icon-name")` `` | `{{< fa icon-name >}}` |
| `` `r emo::ji("wink")` `` | `😉` |
| `` `r emo::ji("speaker")` `` | `🔊` |
| `` `r emo::ji("exclamation")` `` | `❗` |
| `` `r emo::ji("loud")` `` | `📢` |
| `--` (incremental) | `. . .` |
| `class: inverse` | `{background-color="#14497F"}` on `##` heading |
| `class: inverse, center` | `{background-color="#14497F" .center}` |
| `class: inverse, middle` | `{background-color="#14497F"}` |
| `class: inverse, middle, center` | `{background-color="#14497F" .center}` |
| `class: center, middle` | `{.center}` |
| `class: middle` | (drop — no direct equivalent needed) |
| `class: middle, center` | `{.center}` |
| `.pull-left[...] .pull-right[...]` | `:::: {.columns}` / `::: {.column width="50%"}` divs (see template below) |
| `.footnote[...]` | `::: {.footnote}` ... `:::` div |
| `<center>...</center>` | `::: {style="text-align: center;"}` ... `:::` |

**Two-column layout template:**
```markdown
:::: {.columns}
::: {.column width="50%"}
LEFT CONTENT
:::
::: {.column width="50%"}
RIGHT CONTENT
:::
::::
```

**Slide without heading (xaringan `---` + `class:`):**
```markdown
## {background-color="#14497F"}

Content here
```

---

## Task 1: Install Quarto extensions

**Files:**
- Creates: `_extensions/unair/` (managed by quarto)
- Creates: `_extensions/quarto-ext/fontawesome/` (managed by quarto)

**Step 1: Install unair theme**

Run from the project root:
```bash
quarto add rameliaz/quarto-unair-theme --no-prompt
```
Expected: `_extensions/unair/` created with `_extension.yml`, `airlangga.scss`, `theme.html`.

**Step 2: Install fontawesome extension**

```bash
quarto add quarto-ext/fontawesome --no-prompt
```
Expected: `_extensions/quarto-ext/fontawesome/` created.

**Step 3: Commit**

```bash
git add _extensions/
git commit -m "feat: install quarto-unair-theme and fontawesome extensions"
```

---

## Task 2: Create `_quarto.yml`

**Files:**
- Create: `_quarto.yml`
- Delete (later): `_site.yml`

**Step 1: Create `_quarto.yml`**

Create `_quarto.yml` in the project root with this exact content:

```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Latent Variable Modeling Workshop"
  navbar:
    left:
      - text: "oleh Rizqy Amelia Zein"
        href: https://rameliaz.github.io/
      - icon: github
        href: https://github.com/rameliaz/mg-sem-workshop
    right:
      - text: "Salindia (HTML)"
        menu:
          - text: "Bagian 1"
            href: slides/materi-lvm-1.html
          - text: "Bagian 2"
            href: slides/materi-lvm-2.html
          - text: "Bagian 3"
            href: slides/materi-lvm-3.html
          - text: "Bagian 4"
            href: slides/materi-lvm-4.html
      - text: "Salindia (PDF)"
        menu:
          - text: "Bagian 1"
            href: slides/materi-lvm-1.pdf
          - text: "Bagian 2"
            href: slides/materi-lvm-2.pdf
          - text: "Bagian 3"
            href: slides/materi-lvm-3.pdf
          - text: "Bagian 4"
            href: slides/materi-lvm-4.pdf
      - text: "Dataset"
        menu:
          - text: "Dataset Contoh Korelasi"
            href: corr.jasp
          - text: "Dataset Contoh CFA (*.jasp)"
            href: contoh-cfa.jasp
          - text: "Dataset Contoh CFA (*.csv)"
            href: contoh-cfa.csv
          - text: "Dataset Latihan CFA (*.csv)"
            href: dataset-wave1.csv
      - text: "Survei"
        menu:
          - text: "Evaluasi Workshop"
            href: https://www.soscisurvey.de/invited-talk-feedback/

format:
  html:
    theme: cosmo
    toc: true
    toc-float: true
    toc-depth: 3
    df-print: paged
    highlight-style: tango
```

**Step 2: Commit**

```bash
git add _quarto.yml
git commit -m "feat: add _quarto.yml replacing _site.yml"
```

---

## Task 3: Create `index.qmd`

**Files:**
- Create: `index.qmd`
- Delete (later): `index.Rmd`

**Step 1: Create `index.qmd`**

The source `index.Rmd` has no YAML frontmatter — just raw Markdown. Add a minimal YAML header and keep all content unchanged. The full `index.qmd`:

```markdown
---
title: "Workshop Confirmatory Factor Analysis (LVM)"
---

## Deskripsi
Berikut adalah repositori yang digunakan untuk menyimpan semua materi untuk **Workshop *Confirmatory Factor Analysis*** yang diselenggarakan oleh Fakultas Psikologi, Universitas Negeri Semarang. Materi *workshop* ini merupakan bagian (yang dimodifikasi) dari *workshop* *Multigroup Structural Equation modeling* yang diadakan oleh Fakultas Psikologi Universitas Airlangga. Untuk mengakses materi dan rekaman dari *workshop* `MG-SEM`, silahkan [klik tautan ini](https://rameliaz.github.io/mg-sem-workshop/).

Materi berlisensi [*Creative Commons* BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Materi bebas digunakan kembali namun wajib mengatribusi sumber aslinya**.


## Waktu dan tempat
*Workshop* diselenggarakan pada hari **Kamis, 30 Januari 2020**, pukul 07.30-16.00 WIB di Gedung A1 Ruang 204 Fakultas Ilmu Pendidikan, Universitas Negeri Semarang.


## *Outline* materi

Berikut adalah *outline* materi *workshop*:

##### **Pengantar**
* Apa itu *latent variable modeling* (LVM)?
* Mengapa dan pada kondisi seperti apa LVM diperlukan?
* Beberapa pilihan perangkat lunak untuk mengeksekusi LVM
* Yang tidak dicakup dalam *workshop* serta keterbatasan JASP

##### **Korelasi**
* Jenis-jenis koefisien korelasi
* Faktor-faktor yang membuat koefisien korelasi bervariasi
* [Koreksi atenuasi](https://methods.sagepub.com/reference/encyc-of-research-design/n81.xml) dan *measurement error*
* *Variance-covariance* dan *correlation matrix*
* *WARNING! Covariance/correlation matrix is not positive definite*
* [*Heywood* dan *ultra-Heywood case*](https://journals.sagepub.com/doi/10.1177/0049124112442138)
* Bivariat, *part*, dan *partial correlation*
* Metrik variabel (*standardised* vs *unstandardised*)

##### **Model Jalur** (*Path Model*) dan Model Regresi
* Definisi *path model*
* Nama variabel dan koefisien jalur (*path coefficients*)
  * δ (delta), ε (epsilon), ξ (ksi), η (eta), λ (lambda), γ (gamma), β (beta), φ (phi), ζ (zeta)
* Representasi visual model jalur menggunakan diagram jalur (*path diagram*)
* Menggambarkan hubungan antar-variabel dengan menggunakan diagram jalur
* *Syntax* `lavaan` untuk spesifikasi model jalur
* Asumsi kausalitas (?) dan limitasi

##### **Confirmatory Factor Analysis (CFA)**
* Definisi *factor analysis*
* *Exploratory* vs *confirmatory factor analysis*
* Kapan menggunakan CFA?
* [*Constraining parameter* model](https://psycnet.apa.org/record/2008-06808-005)
* Model pengukuran (paralel, *tau equivalence*, dan *congeneric*)
* Variabel indikator (reflektif vs formatif)
* *Correlated error variances*
* Metode estimasi
* Jenis-jenis kriteria untuk menilai ketepatan model (*model fit*)
  * [*Model fit*](http://www.ejbrm.com/issue/download.html?idArticle=183)
  * *Model comparison*/*Incremental fit indices*
  * *Model parsimony*
  * *Parameter fit*
* Menuliskan hasil analisis CFA dalam laporan penelitian


## Referensi

* Baujean, A.A. (2014). *Latent Variable Modeling Using R: A step-by-step guide*. New York: Routledge.
* Schumacker, R.E. & Lomax, R.G. (2016). *A Beginner's Guide to Structural Equation Modeling (4th edition)*. New York: Routledge.
* Van De Schoot, R., Schmidt, P., De Beuckelaer, A., Lek, K., & Zondervan-Zwijnenburg, M. (2015). [Measurement invariance](https://www.frontiersin.org/articles/10.3389/fpsyg.2015.01064/full). Frontiers in psychology, 6, 1064.
* Putnick, D. L., & Bornstein, M. H. (2016). [Measurement invariance conventions and reporting: The state of the art and future directions for psychological research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5145197/). Developmental review, 41, 71-90.
* Cho, E. (2016). [Making Reliability Reliable: A Systematic approach to reliability coefficients](https://rameliaz.github.io/mg-sem-workshop/cho2016.pdf). Organizational Research Methods, 19(4), 651-682.


## Contoh penelitian dengan `CFA`

* Rodriguez, V. J., Radusky, P. D., Kumar, M., Nemeroff, C. B., & Jones, D. (2018). [Measurement invariance of the Childhood Trauma Questionnaire by gender, poverty level, and HIV status](https://www.sciencedirect.com/science/article/abs/pii/S2468171718300085). Personalized Medicine in Psychiatry, 11, 16-22.
* Liu, Y., Millsap, R. E., West, S. G., Tein, J. Y., Tanaka, R., & Grimm, K. J. (2017). [Testing measurement invariance in longitudinal data with ordered-categorical measures](https://psycnet.apa.org/record/2016-25480-001). Psychological methods, 22(3), 486.
* Bowden, S. C., Saklofske, D. H., Van de Vijver, F. J. R., Sudarshan, N. J., & Eysenck, S. B. G. (2016). [Cross-cultural measurement invariance of the Eysenck Personality Questionnaire across 33 countries](https://www.sciencedirect.com/science/article/abs/pii/S0191886916302835). Personality and Individual Differences, 103, 53-60.
* Bieda, A., Hirschfeld, G., Schönfeld, P., Brailovskaia, J., Zhang, X. C., & Margraf, J. (2017). [Universal happiness? Cross-cultural measurement invariance of scales assessing positive mental health](http://www.kli.psy.ruhr-uni-bochum.de/klipsy/public/margraf%20Journals%20with%20Peer-Review/Bieda%20et%20al%202016%20Universal%20happiness.pdf). Psychological assessment, 29(4), 408.


## Sumber belajar lainnya

* [Learning Statistics with JASP](https://learnstatswithjasp.com/)
* [Undergraduate Statistics with JASP](https://osf.io/t56kg/)
* [Materi workshop SEM: Sacha Epskamp](http://sachaepskamp.com/SEM2019)


## Sebelum mulai workshop

* Sebaiknya semua peserta sudah memasang [JASP versi 0.11.1](https://jasp-stats.org/download/) pada perangkatnya masing-masing, untuk menghindari terlalu banyaknya waktu untuk menyelesaikan *troubleshooting* instalasi ketika *workshop*.
* Peserta sangat disarankan untuk menonton video tutorial JASP di bawah ini sebelum *workshop* untuk belajar menavigasikan menu dan fitur yang ada dalam JASP (total durasi kurang lebih hanya 5 menit).

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/HxqB7CUA-XI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>


## Video rekaman

#### Sesi 1 (09.00-12.00)

<iframe width="560" height="315" src="https://www.youtube.com/embed/L38yXlxbO-Y" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


#### Sesi 2 (13.00-16.00)

<iframe width="560" height="315" src="https://www.youtube.com/embed/6AtXbwYrs0s" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Pembaruan dan koreksi


## Poster kegiatan

<center><img src="slides/libs/poster.jpg" style="width:70%;" class="fancyimage"/></center><br>


## Jawaban Latihan


### Latihan Mandiri (1):

[Klik disini untuk melihat jawaban]() saya atas latihan mandiri (1).


### Latihan Mandiri (2):

[Klik disini untuk melihat jawaban]() saya atas latihan mandiri (2).


### Latihan Mandiri (3):

[Klik disini untuk melihat jawaban]() saya atas latihan mandiri (3).
```

**Step 2: Commit**

```bash
git add index.qmd
git commit -m "feat: add index.qmd replacing index.Rmd"
```

---

## Task 4: Create `slides/materi-lvm-1.qmd`

**Files:**
- Create: `slides/materi-lvm-1.qmd`
- Source: `slides/materi-lvm-1.Rmd`

**Step 1: Create `slides/materi-lvm-1.qmd`**

Apply all global conversion rules. Full content:

```markdown
---
title: "Workshop Latent Variable Modeling (LVM)"
subtitle: "Menggunakan JASP: Bagian 1 - Pengantar"
author: "Rizqy Amelia Zein"
institute: "Fakultas Psikologi, Universitas Airlangga"
date: "2020-01-29"
format: unair-revealjs
---

```{r setup, include=FALSE}
library(tidyverse)
options(width = 120)
```

## {background-color="#14497F"}

<img src="libs/unair.png" style="width:15%;"/> <img src="libs/STUA.png" style="width:23%;"/> <img src="libs/ina-logo.jpg" style="width:7%;"/> <img src="libs/igdore.png" style="width:23%;"/>

### Rizqy Amelia Zein

* Dosen, [Fakultas Psikologi, Universitas Airlangga](https://psikologi.unair.ac.id)
* Anggota, [#SainsTerbuka Airlangga](https://sainsterbukaua.github.io/) {{< fa universal-access >}}
* Relawan, [INA-Rxiv](https://inarxiv.id)
* Researcher-in-training, [Institute for Globally Distributed Open Research and Education (IGDORE)](https://igdore.org/)

---

## {.center}

# Menghubungi saya?

{{< fa paper-plane >}} <a href="mailto:amelia.zein@psikologi.unair.ac.id">amelia.zein@psikologi.unair.ac.id</a>
{{< fa twitter >}} [@ameliazein](https://twitter.com/ameliazein)
{{< fa github >}} [@rameliaz](https://github.com/rameliaz)
{{< fa desktop >}} https://rameliaz.github.io

Materi dalam paparan ini berlisensi {{< fa creative-commons >}} 4.0 dan tersedia di laman web pribadi saya **(https://rameliaz.github.io/mlm-lme-workshop/)**.
Kode tersedia secara terbuka di [repositori](https://github.com/rameliaz/mlm-lme-workshop) {{< fa github >}} saya.

---

## *Outline* {background-color="#14497F"}

:::: {.columns}
::: {.column width="50%"}

## Sebelum istirahat (07.30-12.00)

**Pengantar**
* Apa itu *latent variable modeling* (LVM) dan *structural equation modeling* (SEM)?
* Mengapa dan pada kondisi seperti apa LVM-SEM diperlukan?
* Beberapa pilihan perangkat lunak untuk mengeksekusi LVM-SEM
* Yang tidak dicakup dalam *workshop* serta keterbatasan JASP

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/31lPv5L3aIvTi/giphy.gif)

:::
::::

---

## Sebelum istirahat (07.30-12.00)

:::: {.columns}
::: {.column width="50%"}

* Jenis-jenis koefisien korelasi
* Faktor-faktor yang membuat koefisien korelasi bervariasi
* [Koreksi atenuasi](https://methods.sagepub.com/reference/encyc-of-research-design/n81.xml) dan *measurement error*
* *Variance-covariance* dan *correlation matrix*
* *WARNING! Covariance/correlation matrix is not positive definite*
* [*Heywood* dan *ultra-Heywood case*](https://journals.sagepub.com/doi/10.1177/0049124112442138)
* Bivariat, *part*, dan *partial correlation*
* Metrik variabel (*standardised* vs *unstandardised*)

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/3ornjXIIShZ2MgyyHu/giphy.gif)

:::
::::

---

## Sesudah istirahat (13.00-16.00)

:::: {.columns}
::: {.column width="50%"}

* Definisi *path model*
* Nama variabel dan koefisien jalur (*path coefficients*)
  * δ (delta), ε (epsilon), ξ (ksi), η (eta), λ (lambda), γ (gamma), β (beta), φ (phi), ζ (zeta)
* Representasi visual model jalur menggunakan diagram jalur (*path diagram*)
* Menggambarkan hubungan antar-variabel dengan menggunakan diagram jalur
* *Syntax* `lavaan` untuk spesifikasi model jalur
* Asumsi kausalitas (?) dan limitasi

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/rVbAzUUSUC6dO/giphy.gif)

:::
::::

---

## Sesudah istirahat (13.00-16.00) {background-color="#14497F"}

:::: {.columns}
::: {.column width="50%"}

* Definisi *factor analysis*
* *Exploratory* vs *confirmatory factor analysis*
* Kapan menggunakan CFA?
* [*Constraining parameter* model](https://psycnet.apa.org/record/2008-06808-005)
* Model pengukuran (paralel, *tau equivalence*, dan *congeneric*)
* Variabel indikator (reflektif vs formatif)
* *Correlated error variances*
* Metode estimasi
* Jenis-jenis kriteria untuk menilai ketepatan model (*model fit*)
  * [*Model fit*](http://www.ejbrm.com/issue/download.html?idArticle=183)
  * *Model comparison*/*Incremental fit indices*
  * *Model parsimony*
  * *Parameter fit*
* Menuliskan hasil analisis CFA dalam laporan penelitian

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/WUq1cg9K7uzHa/giphy.gif)

:::
::::

---

## Apa itu *latent variable modeling*? {background-color="#14497F" .center}

:::: {.columns}
::: {.column width="50%"}

## Pernahkah bapak/ibu menggunakan *structural equation modeling* (SEM) sebelumnya?
## Untuk apa LVM-SEM digunakan?

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/fvwXjE0Hf70690czE5/giphy.gif)

:::
::::

---

## LVM adalah...

* Model yang memuat **hubungan** antara **observed** dan **latent variables** dalam berbagai bentuk model teoritis. LVM memungkinkan peneliti untuk melakukan **pengujian hipotesis** yang berkaitan dengan model tersebut.

* LVM mengasumsikan (hipotesis) bahwa seperangkat variabel (*observed*) mendefinisikan sebuah konstruk **laten**, dan menggambarkan bagaimana hubungan antara konstruk-konnstruk laten ini.

* Tujuan LVM adalah untuk mengetahui apakah model teoritik yang diuji peneliti **didukung oleh data**
  - Apabila data memberikan **bukti yang mendukung** bahwa hubungan antar konstruk/variabel terjadi, maka **mungkin** hubungan tersebut memang benar-benar ada di populasi.
  - Apabila data **tidak memberikan bukti yang mendukung** korelasi yang dihipotesiskan, maka peneliti dapat melakukan **re-spesifikasi model** dan menguji kembali model yang sudah dire-spesifikasi tersebut, atau **menyusun ulang model yang baru** untuk kemudian diuji kembali.

---

## Jenis-jenis variabel

:::: {.columns}
::: {.column width="50%"}

* Variabel *observed*
  - Variabel yang dapat diukur langsung dengan berbagai cara/strategi.
  - Dalam pengukuran Psikologi, *item* pernyataan (dalam skala Psikologi - bisa dalam bentuk skala *Likert* atau yang lain) adalah variabel *observed*.
  - Variabel *observed* dapat merefleksikan variabel *latent* atau bisa menjadi **kombinasi linear** atas variabel *observed* yang lain (*index*).

* Variabel *latent*
  - Konstruk/variabel yang **tidak dapat diukur secara langsung**.
  - Oleh karena itu, membutuhkan variabel *observed* untuk mengukurnya.
  - Variabel *latent* dapat berperan sebagai variabel *independent* atau *dependent*.

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/irClCpuJAWgRqtP73t/giphy.gif)

:::
::::

---

## Jenis-jenis variabel

:::: {.columns}
::: {.column width="50%"}

* Variabel Eksogen dan Endogen
  - Variabel eksogen {{< fa arrow-circle-right >}} variabel yang **hanya memberi** *direct effect* pada variabel lain di dalam model yang sama
  - Variabel endogen {{< fa arrow-circle-right >}} variabel yang **hanya menerima** *direct effect* pada variabel lain di dalam model yang sama

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/yBFOH8Ux7nHQA/giphy.gif)

:::
::::

---

## Contohnya...

:::: {.columns}
::: {.column width="50%"}

* Seorang peneliti ingin **mengukur kepribadian** seorang responden dengan menggunakan pendekatan *Five-Factor Model* (Big 5), maka aitem dalam skala tersebut adalah *observed variable*, sedangkan dimensi dari Big 5 (*neuroticism*, *agreeableness*, *conscientiousness*, dan *extraversion*) adalah *latent variable*.

* Seorang peneliti Psikologi Pendidikan ingin tahu apakah **kepercayaan orang tua bahwa anaknya dapat berkembang secara natural** (*trust in organismic development* - *independent latent variable*) berkorelasi dengan **tingkat kemandirian anak** (*dependent latent variable*).

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/d5fW0J4klfwnm/giphy.gif)

:::
::::

---

## Contohnya...

:::: {.columns}
::: {.column width="50%"}

* Dalam konteks Psikologi Klinis, seorang pakar *public mental health* ingin tahu apakah **status sosio-ekonomi** (*observed independent variable*) dapat berdampak pada **kondisi kesehatan mental** individu (*latent dependent variable*).

* Dalam sebuah penelitian Psikologi Sosial, peneliti ingin tahu apakah **kepribadian seseorang** (*independent latent variable*) dapat menjelaskan mengapa orang **merespon pelanggaran moral** secara berbeda (*dependent latent variable*).

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/DxneCO38aK4Fi/giphy.gif)

:::
::::

---

## Model SEM

:::: {.columns}
::: {.column width="50%"}

* Model regresi (linear/OLS)
  - Menguji hubungan antar variabel *observed*

* Model jalur (*path model*)
  - Menguji hubungan antara variabel *observed* dan *latent*

* Model pengukuran (*measurement model*/*confirmatory factor analysis*)
  - Menguji apakah aitem-aitem dari skala Psikologi (yang mengukur konstruk laten tertentu) memang betul-betul mengukur konstruk tersebut {{< fa arrow-circle-right >}} validitas konstruk.

* SEM (*full model*) biasanya mengandung setidaknya dua model, yaitu model pengukuran dan model struktural (regresi/jalur).

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/SRNbNpKgJ03mOiYceA/giphy.gif)

:::
::::

---

## Mengapa LVM dilakukan?

* Peneliti sudah memiliki kesadaran bahwa ia harus menyelidiki **beberapa variabel penelitian** secara bersamaan untuk menjawab pertanyaan penelitiannya.

* Ada kesadaran bahwa peneliti selama ini mengabaikan faktor *error* pengkuran. LVM membantu peneliti untuk **mengurangi efek *measurement error*** terhadap hasil analisis data. Untuk itu, peneliti dapat sekaligus menguji properti/kualitas psikometrik instrumen yang digunakan.

* Selama beberapa dekade kebelakang, LVM termasuk teknik analisis data yang sudah cukup **matang pengembangannya**, dan dapat mudah dilakukan dengan bantuan perangkat lunak.

* Perangkat lunak LVM sudah cukup *user-friendly*
  - `JASP` adalah perangkat lunak LVM yang hanya memerlukan *coding* yang sangat minimal.
  - Namun `JASP` fungsinya agak terbatas, karena tidak menyediakan opsi *power analysis* (digunakan untuk merencanakan jumlah sampel) dan simulasi.
  - Selain itu, peneliti dapat menggunakan `Onyx`, `LISREL`, `AMOS`, `EQX`, `Mplus`, `STATA`, dsb.

* LVM adalah teknik yang lebih *sophisticated* untuk menggambarkan **hubungan antar-variabel** karena membuang **error pengukuran** dari estimasi korelasi, dan mengurangi bias estimasi model karena konstruk laten diperlakukan sebagaimana mestinya, bukan **dianggap** seolah-olah *observed variable*.

---

## Yang tidak dicakup oleh *workshop* ini...

:::: {.columns}
::: {.column width="50%"}

* *Exploratory factor analysis* (EFA)
* *Full model* SEM
* *A priori power analysis*, Monte Carlo *simulation*, dan *accuracy in parameter estimation* (AIPE) {{< fa arrow-circle-right >}} merupakan teknik-teknik yang digunakan untuk mengestimasi jumlah sampel
* *Mixture model* (SEM untuk desain penelitian longitudinal) {{< fa arrow-circle-right >}} *latent growth curve*
* Model SEM dengan *missing data*, ada variabel moderator/mediator, atau *moderated mediation* atau *mediated moderation*, atau ketika variabel indikatornya *dichotomous*
* *Hierarchical latent variable model*
* *Second-order CFA*
* SEM dengan model pengukuran formatif dan *multiple indicators, multiple causes* (MIMIC)

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/LpQuxhwDhzLCEKVYFh/giphy.gif)

:::
::::

---

## Ketika menggunakan LVM-SEM, maka asumsinya... {background-color="#14497F"}

:::: {.columns}
::: {.column width="50%"}

### 🔊 Data berdistribusi normal (*multivariate normality*)
### 🔊 Korelasi antar variabel sifatnya linear

:::
::: {.column width="50%"}

![](https://media.giphy.com/media/l4pTfqyI6TCjUW4Yo/giphy.gif)

:::
::::

---

## Normalitas data

* Mengapa data **tidak berdistribusi normal?**
  - Bisa jadi **bentuk datanya ordinal/nominal**, sehingga kalau menggunakan skala *Likert*, maka kemungkinan besar distribusi data menjadi tidak normal.
  - Jumlah sampel **terlalu sedikit**.
  - Distribusi data yang tidak normal akan berdampak pada *variance-covariance matrix*.

* Apa yang harus dilakukan?
  - Untuk **mengkoreksi distribusi data** yang juling (*skewness*), [***probit transformation***](http://methods.sagepub.com/Reference/the-sage-encyclopedia-of-educational-research-measurement-and-evaluation/i16518.xml) merupakan strategi yang terbaik.
  - Untuk mengkoreksi *kurtosis* yang tidak sesuai, membutuhkan prosedur yang agak lebih rumit. Beberapa diantaranya adalah dengan menambah jumlah responden, melakukan estimasi *standard error* dengan metode *bootstrapping*, atau bisa juga dengan menggunakan **metode estimasi** yang khusus untuk data yang tidak berdistribusi normal (*weighted least squares*).

---

## Terima kasih banyak! 😉 {.center}

![](https://media.giphy.com/media/hrBSJ2So6iTo4/giphy.gif)

Paparan disusun dengan menggunakan {{< fa r-project >}} dan [**Quarto**](https://quarto.org) dengan tema [quarto-unair-theme](https://github.com/rameliaz/quarto-unair-theme).
```

**Step 2: Commit**

```bash
git add slides/materi-lvm-1.qmd
git commit -m "feat: convert materi-lvm-1 from xaringan to quarto unair-revealjs"
```

---

## Task 5: Create `slides/materi-lvm-2.qmd`

**Files:**
- Create: `slides/materi-lvm-2.qmd`
- Source: `slides/materi-lvm-2.Rmd`

**Step 1: Create `slides/materi-lvm-2.qmd`**

Apply all global conversion rules to `slides/materi-lvm-2.Rmd`. Key conversions specific to this file:

- YAML: same pattern as lvm-1, subtitle `"Menggunakan JASP: Bagian 2 - Korelasi"`
- First slide: same logo/author slide as lvm-1 (identical across all 4 slides)
- `--` (incremental reveal on slide "Mengapa memulai dari korelasi?") → `. . .`
- `r emo::ji("exclamation")` → `❗`
- All `.pull-left`/`.pull-right` → columns divs
- All `r fa(...)` → `{{< fa ... >}}`
- `<center><img ...></center>` → `::: {style="text-align: center;"}` div
- Last slide: update xaringan credit to Quarto (same as lvm-1)

Full converted content follows the same structure as lvm-1. Slide-by-slide mapping from source:

1. Logo/author slide → `## {background-color="#14497F"}`
2. Contact slide → `## {.center}`
3. "Mengapa memulai dari korelasi?" → `## Mengapa memulai dari korelasi? {background-color="#14497F"}` with `. . .` incremental
4. "Jenis-jenis korelasi" → `## Jenis-jenis korelasi` (table stays as-is)
5. "Faktor-faktor..." → `## Faktor-faktor yang mempengaruhi korelasi`
6. XKCD image slide → `## {}` with center div
7. "Variance-covariance (1)" → `## *Variance-covariance* dan *correlation matrix* (1)`
8. "Variance-covariance (2)" → `## *Variance-covariance* dan *correlation matrix* (2)` with columns
9. "Koreksi Atenuasi" → `## Koreksi Atenuasi`
10. "WARNING!" inverse slide → `## WARNING! {background-color="#14497F" .center}`
11. "Apa yang terjadi?" → `## Apa yang terjadi? {background-color="#14497F" .center}`
12. "Matrik korelasi non-positive definite" → `## Matrik korelasi dengan *non-positive definite*`
13. "Heywood case" → `## *Heywood* dan *ultra-Heywood case*`
14. "Korelasi Bivariat" → `## Korelasi Bivariat: *Part* dan *partial correlation*`
15. "Metrik variabel" → `## Metrik variabel (*standardised* vs *unstandardised*)`
16. Thank you slide → `## Terima kasih banyak! 😉 {.center}`

**Step 2: Commit**

```bash
git add slides/materi-lvm-2.qmd
git commit -m "feat: convert materi-lvm-2 from xaringan to quarto unair-revealjs"
```

---

## Task 6: Create `slides/materi-lvm-3.qmd`

**Files:**
- Create: `slides/materi-lvm-3.qmd`
- Source: `slides/materi-lvm-3.Rmd`

**Step 1: Create `slides/materi-lvm-3.qmd`**

Apply all global conversion rules. Key specifics:

- YAML subtitle: `"Menggunakan JASP: Bagian 3 - Model Jalur (*Path Model*) dan Model Regresi"`
- `r emo::ji("wink")` → `😉`
- All R code blocks (`eval=FALSE`) stay as-is — just change the chunk syntax from ` ```{r eval=FALSE} ` to ` ```{r} ` with `#| eval: false` option (Quarto style), or keep `{r eval=FALSE}` — both work in Quarto
- All `.pull-left`/`.pull-right` → columns divs
- Images with `<center>` → center div

Slide-by-slide mapping:

1. Logo/author → `## {background-color="#14497F"}`
2. Contact → `## {.center}`
3. "Analisis jalur" → `## Analisis jalur {background-color="#14497F"}`
4. "Korelasi = kausalitas?" columns → `## Korelasi = kausalitas?` with columns
5. "Diagram jalur" center image → `## Diagram jalur` with center div
6. "Contoh" inverse+columns → `## Contoh {background-color="#14497F"}` with columns
7. "Variabel yang diukur Marimar" → `## Variabel yang diukur Marimar`
8. Full-width image slide → `## {}` center div
9. "Nama variabel dan koefisien jalur" table → `## Nama variabel dan koefisien jalur`
10. "Contoh model" image → `## Contoh model dengan koefisien jalur`
11. "TUGAS 1" columns → `## TUGAS 1: Membuat diagram jalur` with columns
12. "Yang diukur..." → `## Yang diukur...`
13. "lavaan Syntax" → `## \`lavaan\` *Syntax*`
14. "Dasar syntax lavaan" → `## Dasar *syntax* \`lavaan\``
15. "Contoh CFA (1)" image → `## Contoh CFA (1)`
16. Code block slide → `## {}` with the R code block (using `#| eval: false`)
17. "Contoh CFA (2)" → `## Contoh CFA (2)`
18. Code block slide → `## {}`
19. "Contoh path analysis (3)" → `## Contoh *path analysis* (3)`
20. Code block slide → `## {}`
21. "Contoh full model (4)" → `## Contoh *full model* (4)`
22. Code block slide → `## {}`
23. "TUGAS 2" → `## TUGAS 2: Menulis *syntax* \`lavaan\``
24. Thank you → `## Terima kasih banyak! 😉 {.center}`

**Step 2: Commit**

```bash
git add slides/materi-lvm-3.qmd
git commit -m "feat: convert materi-lvm-3 from xaringan to quarto unair-revealjs"
```

---

## Task 7: Create `slides/materi-lvm-4.qmd`

**Files:**
- Create: `slides/materi-lvm-4.qmd`
- Source: `slides/materi-lvm-4.Rmd`

**Step 1: Create `slides/materi-lvm-4.qmd`**

Apply all global conversion rules. Key specifics:

- YAML subtitle: `"Menggunakan JASP: Bagian 4 - *Confirmatory Factor Analysis*"`
- `r emo::ji("loud")` → `📢`
- Many `<center><img ...></center>` blocks → wrap in `::: {style="text-align: center;"}` divs
- Note: several images have `style="width=100%"` (using `=` instead of `:`) — this is a bug in the original; keep as-is or fix to `style="width:100%;"` (either is fine)

Slide-by-slide mapping:

1. Logo/author → `## {background-color="#14497F"}`
2. Contact → `## {.center}`
3. "Analisis faktor" columns → `## Analisis faktor` with columns
4. "EFA vs CFA" table → `## EFA vs CFA`
5. "Confirmatory factor analysis" → `## *Confirmatory factor analysis*`
6. Texas Sharpshooter image → `## {.center}`
7. "Constraining parameter model" → `## [*Constraining parameter* model](...)`
8. "Jenis-jenis model pengukuran" → `## Jenis-jenis model pengukuran`
9. Congeneric image → `## {.center}`
10. Tau image → `## {.center}`
11. Paralel image → `## {.center}`
12. "Reflektif vs Formatif" → `## Reflektif vs Formatif`
13. Reflektif image → `## {.center}`
14. Formatif image → `## {.center}`
15. "Apa yang terjadi ketika error variance berkorelasi?" → `## Apa yang terjadi ketika *error variance* berkorelasi?`
16. "Skor faktor" → `## Skor faktor (*factor scores*)`
17. "Memilih metode estimasi" → `## Memilih metode estimasi`
18. "Mengestimasi model" + "Menguji model" → `## Mengestimasi dan menguji model`
19. "Menguji ketepatan model" → `## Menguji ketepatan model`
20. "Chi-square" columns → `## Menguji ketepatan model: *Chi-square*` with columns
21. "Incremental index" → `## *Incremental (comparative/relative) index*`
22. "Parsimony index" → `## *Parsimony index*`
23. "Absolute index" → `## *Absolute index*`
24. "Parameter fit" → `## *Parameter fit*`
25. "Demonstrasi CFA" inverse+center → `## Demonstrasi CFA {background-color="#14497F" .center}`
26. "TUGAS 3" → `## TUGAS 3: Mencoba *confirmatory factor analysis*`
27. Thank you → `## Terima kasih banyak! 😉 {.center}`

**Step 2: Commit**

```bash
git add slides/materi-lvm-4.qmd
git commit -m "feat: convert materi-lvm-4 from xaringan to quarto unair-revealjs"
```

---

## Task 8: Delete old `.Rmd` files

**Files:**
- Delete: `_site.yml`
- Delete: `index.Rmd`
- Delete: `slides/materi-lvm-1.Rmd`
- Delete: `slides/materi-lvm-2.Rmd`
- Delete: `slides/materi-lvm-3.Rmd`
- Delete: `slides/materi-lvm-4.Rmd`
- Delete: `docs/slides/materi-lvm-1.Rmd` (stale copy)
- Delete: `docs/slides/materi-lvm-2.Rmd` (stale copy)
- Delete: `docs/slides/materi-lvm-3.Rmd` (stale copy)
- Delete: `docs/slides/materi-lvm-4.Rmd` (stale copy)

**Step 1: Delete files**

```bash
git rm _site.yml index.Rmd slides/materi-lvm-1.Rmd slides/materi-lvm-2.Rmd slides/materi-lvm-3.Rmd slides/materi-lvm-4.Rmd docs/slides/materi-lvm-1.Rmd docs/slides/materi-lvm-2.Rmd docs/slides/materi-lvm-3.Rmd docs/slides/materi-lvm-4.Rmd
```

**Step 2: Commit**

```bash
git commit -m "chore: remove old xaringan/rmarkdown source files"
```

---

## Task 9: Build and verify

**Step 1: Run quarto render**

From project root:
```bash
quarto render
```
Expected: No errors. `docs/` is populated with `index.html` and `slides/materi-lvm-{1,2,3,4}.html`.

**Step 2: Check output files exist**

```bash
ls docs/
ls docs/slides/
```
Expected:
- `docs/index.html`
- `docs/slides/materi-lvm-1.html`
- `docs/slides/materi-lvm-2.html`
- `docs/slides/materi-lvm-3.html`
- `docs/slides/materi-lvm-4.html`

**Step 3: Preview locally**

```bash
quarto preview
```
Open browser and verify:
- Homepage renders with cosmo theme and correct navbar
- Each slide deck opens and shows the unair-revealjs theme (UNAIR blue/yellow)
- FontAwesome icons render (no `{{< fa >}}` raw text visible)
- Two-column layouts display correctly
- Incremental reveal works on lvm-2 "Mengapa memulai..." slide

**Step 4: Render PDF slides**

```bash
quarto render slides/materi-lvm-1.qmd --to pdf
quarto render slides/materi-lvm-2.qmd --to pdf
quarto render slides/materi-lvm-3.qmd --to pdf
quarto render slides/materi-lvm-4.qmd --to pdf
```
Expected: PDF files created at `docs/slides/materi-lvm-{1,2,3,4}.pdf`.

**Step 5: Commit rendered output**

```bash
git add docs/
git commit -m "build: render quarto site to docs/"
```

---

## Task 10: Update CLAUDE.md

**Files:**
- Modify: `CLAUDE.md`

**Step 1: Update build commands section**

Replace the "Build Commands" section in `CLAUDE.md` to reflect Quarto:

```markdown
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

# Render PDF versions of slides
quarto render slides/materi-lvm-1.qmd --to pdf

# Simulate workshop datasets (R)
source("dataset-simulasi.R")
```

One-time setup (after cloning):
```bash
quarto add rameliaz/quarto-unair-theme --no-prompt
quarto add quarto-ext/fontawesome --no-prompt
```
```

**Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md for quarto migration"
```
