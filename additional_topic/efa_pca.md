# Principal Component Analysis (PCA) & Exploratory Factor Analysis (EFA)
## Rencana Slide — Statistik Multivariat S2 Psikologi

**Mata Kuliah:** Statistik Multivariat (FPS25801008)
**Program:** Magister Psikologi, Universitas Airlangga
**Pengampu:** Dr. Rizqy Amelia Zein, M.Sc.
**Durasi:** 2 pertemuan (Pertemuan 11: Kuliah; Pertemuan 12: Praktikum)
**Versi:** 1.2 (ditambah PENGANTAR 4 slide tentang variabel laten, CTT, keluarga model, attenuation bias; total 51 slide)

---

## OPENING (2 slides)

---

### Slide 1: Title Slide

```
PRINCIPAL COMPONENT ANALYSIS &
EXPLORATORY FACTOR ANALYSIS
Menemukan Struktur Laten dalam Data

Statistik Multivariat
Magister Psikologi, Universitas Airlangga
Dr. Rizqy Amelia Zein, M.Sc.
Semester Genap 2025/26
```

---

### Slide 2: Skala psikologi sering punya puluhan item — apa yang tersembunyi di baliknya?

**Judul:** Kita tidak mengukur 18 hal berbeda — kita mengukur beberapa konstruk yang lebih dalam

**Konten:**

**Contoh: Social Media Fatigue Scale (Dhir et al., 2018)**
- 18 item total
- EE1: "Saya merasa lelah secara emosional setelah menggunakan media sosial"
- IO3: "Saya merasa kesulitan memfilter informasi di media sosial"
- PC2: "Saya khawatir privasi saya terancam di media sosial"

**Pertanyaan:** Apakah 18 item ini mengukur 18 hal yang benar-benar berbeda? Atau ada struktur yang lebih sederhana di baliknya?

**Masalah praktis yang muncul:**
- Tidak bisa divisualisasikan (kita tidak bisa memplot 18 dimensi sekaligus)
- Regresi dengan 18 prediktor: risiko overfitting sangat tinggi
- Item-item saling berkorelasi tinggi — ada redundansi

**Solusi:** Temukan berapa *dimensi sesungguhnya* yang mendasari 18 item ini. PCA dan EFA adalah alat untuk itu.

---

## PENGANTAR: Variabel Laten dalam Psikologi (4 slides)

---

### Slide 3: Section Divider

```
PENGANTAR
Variabel Laten dalam Psikologi
Mengapa Kita Tidak Bisa Mengukur Konstruk Psikologis Secara Langsung?
```

---

### Slide 4: Psikologi mengukur hal-hal yang tidak bisa dilihat — ini tantangan yang berbeda dari ilmu lain

**Judul:** Konstruk psikologis adalah variabel laten: ada secara teoritis, tidak bisa diobservasi langsung

**Konten:**

**Bandingkan dengan ilmu lain:**
- Fisikawan mengukur massa → timbang objeknya, selesai
- Kimiawan mengukur pH → celupkan kertas lakmus, baca angkanya
- **Psikolog mengukur "kecemasan"** → tidak ada alat ukur langsung; hanya bisa mengamati indikatornya

**Variabel laten (latent variable):** Konstruk yang secara teoritis ada dan mempengaruhi perilaku yang kita amati, tetapi tidak bisa diukur secara langsung.

**Contoh konstruk laten dalam psikologi:**
- Kecemasan → diindikasikan oleh: detak jantung cepat, gelisah, sulit berkonsentrasi, khawatir berlebihan
- Kelelahan akademik → diindikasikan oleh: kelelahan emosional, sinisme, efikasi diri rendah
- Dukungan sosial → diindikasikan oleh: merasa didukung keluarga, teman, orang terdekat

**Implikasi:** Yang kita ukur (item kuesioner, skor tes) bukanlah konstruknya — melainkan *manifestasi* dari konstruk itu. Perbedaan ini bukan soal filsafat; ia berdampak langsung pada cara kita menganalisis data.

---

### Slide 5: Classical Test Theory — model variabel laten paling sederhana yang sudah Anda kenal

**Judul:** CTT menyatakan bahwa setiap skor observasi = true score + error — faktor laten adalah true score itu

**Konten:**

**Model CTT (Spearman, 1904):**
$$X = T + E$$

Di mana:
- $X$ = skor yang diobservasi (nilai yang kita catat dari responden)
- $T$ = *true score* — skor "sebenarnya" jika tidak ada error → ini adalah **variabel laten**
- $E$ = measurement error — fluktuasi acak karena mood, kelelahan, ambiguitas item, kondisi pengukuran

**Ini bukan teori abstrak — ini realitas pengukuran psikologi:**
- Responden yang sama mengisi skala kecemasan dua kali → skornya tidak identik → perbedaan = error
- Kita tidak pernah tahu nilai $T$ untuk individu mana pun — kita hanya *mengobservasi* $X$
- Reliabilitas (α, ω) = proporsi variansi $X$ yang berasal dari $T$, bukan $E$

**Hubungan dengan analisis faktor:**
CTT adalah kasus paling sederhana dari model variabel laten: satu faktor laten, satu item. EFA dan CFA adalah generalisasi CTT ke banyak item dan banyak faktor.

---

### Slide 6: EFA, CFA, dan SEM — satu keluarga model yang meningkat dalam ketegasan pengujian

**Judul:** Ketiganya memodelkan variabel laten, tapi berbeda dalam seberapa eksplisit hipotesisnya

**Konten:**

| Model | Pertanyaan yang dijawab | Level formalisasi |
|-------|------------------------|-------------------|
| **CTT** | "Seberapa reliabel skor total ini?" | Paling sederhana — satu faktor per skala |
| **EFA** | "Berapa faktor laten yang mendasari item-item ini?" | Eksplorasi — data yang menentukan strukturnya |
| **CFA** | "Apakah struktur faktor yang saya hipotesiskan cocok dengan data?" | Konfirmasi — peneliti yang menentukan strukturnya |
| **SEM** | "Bagaimana faktor-faktor laten ini saling mempengaruhi?" | Paling formal — model pengukuran + model struktural |

**Narasi perkuliahan:**
- **Pertemuan ini (EFA/PCA):** "Biarkan data menunjukkan strukturnya"
- **Pertemuan 14 (CFA):** "Uji apakah struktur yang ditemukan/dihipotesiskan valid"
- **Penelitian lanjutan (SEM):** "Uji hubungan kausal antar konstruk laten"

**Satu prinsip yang berlaku di semua level:**
Item mengukur konstruk laten → konstruk laten tidak bisa diobservasi langsung → kita *inferensikan* keberadaannya dari pola korelasi antar item.

---

### Slide 7: Measurement error bukan sekadar "gangguan" — ia mendistorsi semua analisis yang bergantung padanya

**Judul:** Korelasi dan koefisien regresi dengan variabel yang diukur dengan error selalu terlalu kecil — ini disebut attenuation bias

**Konten:**

**Attenuation bias (Spearman, 1904):**
Korelasi antara dua variabel yang masing-masing mengandung measurement error akan selalu *lebih kecil* dari korelasi sesungguhnya antar true score-nya:

$$r_{XY_{observed}} = r_{T_X T_Y} \times \sqrt{\rho_{XX'} \times \rho_{YY'}}$$

Di mana $\rho_{XX'}$ dan $\rho_{YY'}$ adalah reliabilitas masing-masing variabel.

**Contoh konkret:**
Peneliti ingin menguji: "Apakah kecemasan akademik → prestasi akademik?"
- Reliabilitas skala kecemasan = .80
- Reliabilitas IPK sebagai ukuran prestasi = .90
- Korelasi sesungguhnya antar konstruk (*true r*) = −.40

→ **Korelasi yang terobservasi** = −.40 × √(.80 × .90) = −.40 × .85 = **−.34**

Kita *underestimate* hubungan sebesar 15% hanya karena measurement error — meskipun pengukurannya terbilang cukup reliabel!

**Implikasi untuk analisis faktor:**
- EFA dan CFA secara eksplisit memodelkan *unique variance* (termasuk error) per item
- Ini memisahkan sinyal (*common variance*) dari noise — memberikan estimasi loading yang lebih akurat
- Dalam CFA/SEM, koefisien struktural antar konstruk lebih mendekati hubungan sesungguhnya dibanding regresi biasa dengan total skor

**Pesan kunci:** Analisis faktor bukan hanya soal "meringkas item" — ini tentang memisahkan sinyal dari noise untuk mendapatkan gambaran yang lebih akurat tentang konstruk psikologis.

---

## BAGIAN 1: Principal Component Analysis (PCA) (7 slides)

---

### Slide 8: Section Divider

```
BAGIAN 1
Principal Component Analysis (PCA)
```

---

### Slide 9: PCA mencari "arah" yang menangkap variansi paling banyak

**Judul:** PC1 adalah kombinasi linear item yang paling informatif — PC2 yang berikutnya, dan seterusnya

**Konten:**

**Konsep inti:**
PCA mencari "arah" (*component*) dalam ruang data yang menangkap variansi sebesar mungkin.

**Hierarki komponen:**
- **PC1:** Arah dengan variansi terbesar dari seluruh data
- **PC2:** Arah *orthogonal* (tegak lurus) terhadap PC1, dengan variansi terbesar berikutnya
- **PC3, PC4, ...:** Dst., selalu orthogonal terhadap semua komponen sebelumnya

**Artinya dalam praktik:**
- PC1 = dimensi paling "penting" — menjelaskan paling banyak variasi antar partisipan
- PC2 = dimensi penting kedua, tidak berkorelasi dengan PC1
- Dengan 18 item, kita mendapatkan 18 PC — tapi sebagian besar informasi biasanya ada di 2–4 PC pertama

**Visual:** Scatter plot 2D dengan dua sumbu (PC1 dan PC2), menunjukkan arah variansi maksimal.

---

### Slide 10: Eigenvalue — ukuran seberapa penting setiap komponen

**Judul:** Eigenvalue mengukur seberapa banyak variansi yang dijelaskan oleh setiap komponen

**Konten:**

**Eigenvalue (λ):** Jumlah variansi yang dijelaskan oleh suatu komponen. Total eigenvalue = jumlah item.

**Contoh: Social Media Fatigue Scale (18 item)**

| Komponen | Eigenvalue (λ) | % Variansi | Kumulatif % |
|----------|:--------------:|:----------:|:-----------:|
| PC1 | 5.4 | 30.0% | 30.0% |
| PC2 | 3.2 | 17.8% | 47.8% |
| PC3 | 2.1 | 11.7% | 59.4% |
| PC4 | 1.3 | 7.2% | 66.6% |
| PC5–PC18 | < 1.0 | ... | ... |

**Kaiser criterion:** Pertahankan komponen dengan eigenvalue > 1.
→ Logika: komponen dengan λ < 1 menjelaskan variansi *kurang* dari satu item tunggal.

**Catatan penting:** Kaiser criterion cenderung *over-extract* (menghasilkan terlalu banyak komponen). Selalu kombinasikan dengan scree plot dan parallel analysis.

---

### Slide 11: Scree plot — "elbow test" secara visual

**Judul:** Scree plot memperlihatkan di mana komponen berhenti bermakna

**Konten:**

**Scree plot:** Grafik eigenvalue dari tertinggi ke terendah. Cari "elbow" (titik siku) di mana kurva mulai mendatar.

**Cara baca:**
- Bagian yang turun curam = komponen bermakna
- Bagian yang mendatar = komponen tidak bermakna
- Pertahankan komponen *sebelum* elbow

**Dari contoh SMF Scale:**
- PC1: λ = 5.4 → turun tajam
- PC2: λ = 3.2 → masih turun
- PC3: λ = 2.1 → elbow ada di sini
- PC4: λ = 1.3 → sudah mendatar

→ **Kesimpulan: 3 komponen**

**Visual:** Scree plot dengan eigenvalue PC1–PC8, elbow ditandai di PC3.

**Referensi:** Cattell (1966). Subjektif, tapi intuitif. Kombinasikan dengan parallel analysis untuk keputusan yang lebih kuat.

---

### Slide 12: Component loadings — apa arti setiap komponen?

**Judul:** Loading adalah korelasi antara item dan komponen — inilah yang memberi nama komponen

**Konten:**

**Loading:** Korelasi antara item asli dengan komponen. Rentang −1 sampai +1.
- |loading| > 0.40: item bermakna untuk komponen ini (*salient loading*)
- |loading| < 0.30: item tidak relevan untuk komponen ini

**Contoh: SMF Scale setelah rotasi Varimax**

| Item | PC1 | PC2 | PC3 |
|------|:---:|:---:|:---:|
| EE1 "Merasa lelah emosional" | **.82** | .15 | −.05 |
| EE2 "Merasa terkuras" | **.79** | .08 | .10 |
| EE3 "Merasa overwhelmed" | **.75** | .12 | −.08 |
| IO1 "Terlalu banyak informasi" | .10 | **.85** | .06 |
| IO2 "Sulit memfilter informasi" | .15 | **.81** | −.12 |
| PC1 "Khawatir privasi" | −.02 | .11 | **.78** |
| PC2 "Takut data disalahgunakan" | .08 | −.06 | **.83** |

**Interpretasi:**
- PC1 = *Emotional Exhaustion* (item EE load tinggi)
- PC2 = *Information Overload* (item IO load tinggi)
- PC3 = *Privacy Concerns* (item PC load tinggi)

---

### Slide 13: Rotasi — dari solusi matematis ke struktur yang bisa diinterpretasi

**Judul:** Rotasi tidak mengubah variansi yang dijelaskan — hanya mendistribusikannya agar lebih mudah dibaca

**Konten:**

**Masalah:** Komponen yang belum dirotasi sering memiliki banyak *cross-loading* (item load moderat di banyak komponen) — sulit diinterpretasikan.

**Solusi:** Rotasi mengejar *simple structure* (Thurstone, 1947):
- Setiap item load tinggi di SATU komponen, mendekati nol di yang lain
- Setiap komponen punya campuran loading tinggi dan mendekati nol

**Dua jenis rotasi:**

| | Orthogonal | Oblique |
|---|---|---|
| **Komponen** | Tidak berkorelasi | Boleh berkorelasi |
| **Metode umum** | Varimax | Promax, Direct Oblimin |
| **Kapan** | Komponen dianggap independen | Faktor diperkirakan berkorelasi |

**Rekomendasi praktis:**
- Mulai dengan Varimax untuk eksplorasi
- Gunakan Promax/Oblimin jika ada alasan teoretis bahwa konstruk saling berkorelasi (misalnya depresi dan kecemasan)
- Rotasi **tidak** mengubah total variansi yang dijelaskan — hanya redistribusinya

---

### Slide 14: Component scores — nilai setiap partisipan pada setiap komponen

**Judul:** Component score merangkum 18 kolom item menjadi 3 skor komposit per partisipan

**Konten:**

**Component score:** Nilai komposit setiap partisipan pada setiap komponen — *weighted sum* dari item asli dengan loading sebagai bobot.

**Analogi:**
- Data asli = 18 kolom (item)
- Component scores = 3 kolom (PC1, PC2, PC3)

**Contoh satu partisipan:**
- PC1 score = 1.5 → kelelahan emosional tinggi
- PC2 score = −0.3 → information overload rendah
- PC3 score = 0.8 → kekhawatiran privasi moderat

**Gunanya:**
- Digunakan sebagai prediktor dalam analisis regresi berikutnya
- Digunakan untuk klusterisasi partisipan
- Divisualisasikan: plot PC1 vs PC2 untuk melihat distribusi partisipan

**Alternatif praktis:** *Sum scores* (rata-rata item per faktor) hampir identik jika loadings tinggi — lebih mudah dihitung dan diinterpretasikan untuk keperluan klinis.

---

## BAGIAN 2: Exploratory Factor Analysis (EFA) (7 slides)

---

### Slide 15: Section Divider

```
BAGIAN 2
Exploratory Factor Analysis (EFA)
```

---

### Slide 16: PCA vs EFA — perbedaan yang sering disalahpahami

**Judul:** PCA merangkum data; EFA mencari konstruk laten yang *menyebabkan* pola korelasi

**Konten:**

| Aspek | PCA | EFA |
|-------|-----|-----|
| **Tujuan** | Reduksi dimensi | Identifikasi konstruk laten |
| **Variansi** | Total variansi (termasuk *unique*) | Hanya *common variance* |
| **Model** | Komponen = fungsi linear item | Item = fungsi linear faktor + error |
| **Error** | Tidak dimodelkan | Eksplisit dimodelkan |
| **Penggunaan** | Kompresi data, feature extraction | Pengembangan & validasi skala |

**Analogi:**
- **PCA:** "Kompres 18 item menjadi 3 variabel ringkasan"
- **EFA:** "18 item ini mengukur 3 konstruk laten apa?"

**Dalam praktik:** Jika *communalities* tinggi (> 0.6) dan struktur jelas, PCA dan EFA sering memberikan hasil yang hampir identik. Perbedaan muncul ketika *communalities* rendah atau struktur kompleks.

---

### Slide 17: Model EFA — item adalah manifestasi dari konstruk laten

**Judul:** Dalam EFA, konstruk laten yang menyebabkan item — bukan sebaliknya

**Konten:**

**Konsep model EFA:**
Item yang kita observasi adalah *manifestasi* (indikator) dari faktor laten yang tidak bisa kita ukur langsung.

**Contoh:**
Item "Saya merasa lelah emosional setelah menggunakan media sosial"
= dipengaruhi oleh faktor laten *Emotional Exhaustion*
+ *unique variance* (varians spesifik item ini)
+ error pengukuran

**Model formal (disederhanakan):**
$$X_i = \lambda_i F + \delta_i$$

Di mana:
- $X_i$ = skor item ke-*i* yang diobservasi
- $\lambda_i$ = *factor loading* (kekuatan hubungan item dengan faktor)
- $F$ = skor faktor laten
- $\delta_i$ = *unique variance* + error (tidak dijelaskan oleh faktor)

**Perbedaan kritis dari PCA:** EFA secara eksplisit mengakui bahwa setiap item punya *unique variance* yang tidak bisa dijelaskan oleh faktor bersama.

---

### Slide 18: Komunalitas dan keunikan — seberapa baik item diwakili oleh faktor?

**Judul:** Komunalitas tinggi = item adalah indikator yang baik; komunalitas rendah = item bermasalah

**Konten:**

**Komunalitas (h²):** Proporsi variansi item yang dijelaskan oleh *semua* faktor bersama.

**Keunikan (u²):** 1 − h² = Variansi yang *tidak* dijelaskan oleh faktor mana pun (variansi spesifik + error).

**Contoh:**

| Item | h² | u² | Interpretasi |
|------|:--:|:--:|--------------|
| EE1 | .68 | .32 | 68% variansi dijelaskan faktor ✓ |
| EE2 | .72 | .28 | Baik |
| IO1 | .65 | .35 | Baik |
| Item X | .22 | .78 | Hanya 22% — pertimbangkan untuk dihapus |

**Panduan praktis:**
- h² > 0.50: Baik — item diwakili dengan baik oleh faktor
- h² 0.30–0.50: Cukup — perlu evaluasi lebih lanjut
- h² < 0.30: Bermasalah — pertimbangkan menghapus item dari skala

---

### Slide 19: Metode ekstraksi — bagaimana faktor ditemukan dari data

**Judul:** Pilih metode ekstraksi berdasarkan distribusi data dan tujuan analisis

**Konten:**

**Tiga metode utama:**

| Metode | Asumsi distribusi | Keunggulan | Kapan digunakan |
|--------|-------------------|------------|-----------------|
| **Maximum Likelihood (ML)** | Normalitas multivariat | Memberikan fit indices (χ², RMSEA, CFI) | Data mendekati normal; ingin uji fit formal |
| **Principal Axis Factoring (PAF)** | Tidak diperlukan | Robust terhadap pelanggaran normalitas | Data non-normal; sampel moderat |
| **Minimum Residual (MinRes)** | Tidak diperlukan | Meminimalkan residual korelasi; stabil | Data psikologi skala Likert; direkomendasikan secara umum |

**Rekomendasi:**
- **Data Likert ordinal:** Gunakan MinRes atau PAF (dengan matriks *polychoric correlation* jika software mendukung)
- **Data mendekati normal, ingin fit indices:** Gunakan ML
- **Default yang aman untuk psikologi:** MinRes

---

### Slide 20: Berapa faktor yang dipertahankan? — Gunakan kombinasi kriteria

**Judul:** Tidak ada satu kriteria yang cukup — selalu gunakan kombinasi

**Konten:**

**Lima kriteria yang tersedia:**

**1. Kaiser criterion** — Eigenvalue > 1
- Pro: Sederhana, default di hampir semua software
- Kontra: Terbukti *over-extract* secara konsisten (Zwick & Velicer, 1986)

**2. Scree plot** — Cari titik elbow
- Pro: Visual, intuitif
- Kontra: Subjektif; dua peneliti bisa membaca scree plot yang sama berbeda

**3. Parallel analysis** ← **DIREKOMENDASIKAN**
- Bandingkan eigenvalue data nyata dengan eigenvalue dari data acak (N × p yang sama)
- Pertahankan faktor di mana eigenvalue nyata > eigenvalue acak (persentil ke-95)
- Pro: Paling akurat secara empiris; tidak subjektif (Hayton, Allen & Scarpello, 2004)
- Con: Butuh software (tersedia di JASP, R)

**4. Teori** — Berapa faktor yang diharapkan berdasarkan literatur?

**5. Fit indices (khusus ML)** — CFI > .95, TLI > .95, RMSEA < .06

**Praktik terbaik:** Parallel analysis + scree plot + teori = dasar keputusan yang solid.

---

### Slide 21: Parallel analysis — mengapa lebih baik dari Kaiser criterion

**Judul:** Kaiser criterion bisa menghasilkan faktor dari data acak pun — parallel analysis tidak

**Konten:**

**Masalah Kaiser criterion:**
Bahkan data yang *sepenuhnya acak* (tidak ada struktur) bisa menghasilkan beberapa eigenvalue > 1, terutama jika jumlah item banyak.

**Cara kerja parallel analysis:**
1. Generate 1000 dataset acak dengan dimensi yang sama (N × jumlah item)
2. Hitung eigenvalue untuk setiap dataset acak
3. Ambil persentil ke-95 dari distribusi eigenvalue acak
4. Pertahankan faktor di mana eigenvalue nyata **>** eigenvalue acak

**Contoh perbandingan:**

| Komponen | Data nyata | Data acak (P95) | Keputusan |
|----------|:----------:|:---------------:|:---------:|
| 1 | 5.4 | 1.6 | ✓ Pertahankan |
| 2 | 3.2 | 1.4 | ✓ Pertahankan |
| 3 | 2.1 | 1.3 | ✓ Pertahankan |
| 4 | 1.3 | 1.2 | ✗ Hapus |
| 5 | 0.9 | 1.1 | ✗ Hapus |

→ **3 faktor** (bukan 4 seperti Kaiser!)

**Catatan:** Di JASP, parallel analysis tersedia langsung di menu EFA/PCA. Di R, gunakan `fa.parallel()` dari package `psych`.

---

### Slide 22: Rotasi orthogonal vs oblique dalam EFA

**Judul:** Untuk konstruk psikologi, oblique lebih realistis — konstruk psikologi hampir selalu berkorelasi

**Konten:**

**Rotasi orthogonal (faktor tidak berkorelasi):**
- **Varimax:** Paling umum; memaksimalkan variansi loading kuadrat
- Menghasilkan satu matriks: *factor loadings*
- Asumsi independensi sering tidak realistis dalam psikologi

**Rotasi oblique (faktor boleh berkorelasi):**
- **Promax:** Efisien secara komputasi; dimulai dari Varimax lalu disesuaikan
- **Direct Oblimin:** Lebih fleksibel; parameter delta mengontrol tingkat korelasi
- Menghasilkan **tiga** matriks:
  - *Pattern matrix*: Kontribusi unik faktor ke item (setara dengan β dalam regresi) — **ini yang dilaporkan**
  - *Structure matrix*: Korelasi total item dengan faktor (termasuk korelasi tidak langsung)
  - *Factor correlation matrix*: Korelasi antar faktor

**Contoh korelasi faktor yang masuk akal:**
Depresi dan kecemasan: r ≈ 0.60 — jelas berkorelasi, oblique lebih tepat.
Emotional Exhaustion dan Privacy Concerns: r ≈ 0.20 — lebih mandiri, orthogonal bisa dipertahankan.

**Rekomendasi:** Gunakan **Promax** atau **Direct Oblimin** secara default untuk data psikologi. Jika korelasi antar faktor ternyata sangat rendah (< 0.15), orthogonal bisa digunakan.

---

## BAGIAN 3: Asumsi dan Kesiapan Data (4 slides)

---

### Slide 23: Section Divider

```
BAGIAN 3
Asumsi dan Kesiapan Data
```

---

### Slide 24: Asumsi PCA dan EFA

**Judul:** Lebih longgar dari regresi, tapi bukan tanpa syarat

**Konten:**

**Yang HARUS dipenuhi:**
1. **Korelasi antar item yang memadai** — Item harus saling berkorelasi; jika tidak ada korelasi, tidak ada struktur yang bisa ditemukan. Periksa: ada r > 0.30 di matriks korelasi?
2. **Ukuran sampel yang cukup** — Lihat panduan di Slide 21
3. **Linearitas** — Hubungan antar item harus linear (periksa dengan scatterplot matrix)
4. **Tidak ada outlier multivariate ekstrem** — Cek dengan Mahalanobis distance

**Yang TIDAK perlu (untuk PAF/MinRes):**
- ✗ Normalitas univariat (tapi normalitas membantu)
- ✗ Homoskedastisitas

**Khusus untuk ML extraction:**
- ✓ Diperlukan normalitas multivariat (lebih ketat)

**Missing data:**
Regresi menggunakan *listwise deletion* secara default. Jika missing > 5%, pertimbangkan imputasi sebelum analisis.

---

### Slide 25: KMO dan Bartlett — apakah data siap untuk analisis faktor?

**Judul:** Dua uji wajib sebelum EFA/PCA: KMO dan Bartlett's test

**Konten:**

**KMO (Kaiser-Meyer-Olkin Measure of Sampling Adequacy):**
Mengukur apakah pola korelasi antar item cukup kompak untuk analisis faktor.
"Apakah korelasi parsial antar item kecil dibanding korelasi bivariatnya?"

**Interpretasi KMO** (label asli dari Kaiser, 1974):

| KMO | Label |
|-----|-------|
| > 0.90 | *Marvelous* |
| 0.80 – 0.90 | *Meritorious* |
| 0.70 – 0.80 | *Middling* |
| 0.60 – 0.70 | *Mediocre* |
| 0.50 – 0.60 | *Miserable* |
| < 0.50 | *Unacceptable* — jangan lanjutkan EFA |

**Bartlett's Test of Sphericity:**
- H₀: Matriks korelasi = matriks identitas (tidak ada korelasi antar item)
- p < .05 → Tolak H₀ → Ada korelasi yang cukup → EFA layak dilakukan

**Contoh output:**
KMO = 0.87 (*Meritorious*) ✓
Bartlett's test: χ²(153) = 2456.3, p < .001 ✓
→ **Data sangat cocok untuk analisis faktor!**

---

### Slide 26: Ukuran sampel — seberapa besar N yang dibutuhkan?

**Judul:** N ≥ 300 adalah target yang aman untuk sebagian besar kondisi

**Konten:**

**Panduan umum (Comrey & Lee, 1992):**

| N | Keterangan |
|---|------------|
| < 100 | Tidak memadai — hindari |
| 100 – 200 | Minimal, bisa diterima hanya jika loadings tinggi (> 0.70) |
| 200 – 300 | Cukup (*fair*) |
| 300 – 500 | Baik (*good*) |
| 500 – 1000 | Sangat baik |
| > 1000 | Excellent |

**Aturan rasio item:partisipan:**
- Minimum: 5:1 (18 item → N = 90) — hanya jika loadings sangat tinggi
- Direkomendasikan: 10:1 (18 item → N = 180)
- Ideal: 20:1 (18 item → N = 360)

**Faktor yang mempengaruhi:**
- Loadings tinggi (> 0.70) → N yang lebih kecil bisa cukup
- Komunalitas rendah (< 0.40) → butuh N lebih besar
- Banyak faktor → butuh N lebih besar

**Praktis:** Targetkan **N ≥ 300** untuk penelitian pengembangan skala psikologi.

---

### Slide 27: Komunalitas rendah — identifikasi item bermasalah

**Judul:** Item dengan komunalitas < 0.30 tidak diwakili dengan baik oleh faktor — pertimbangkan untuk dihapus

**Konten:**

**Mengapa komunalitas rendah bermasalah?**
Item dengan h² rendah mengukur sesuatu yang unik, tidak berbagi variansi dengan item lain — sinyal bahwa item tersebut "berbicara sendiri."

**Penyebab komunalitas rendah:**
- Redaksi item ambigu (item bisa diinterpretasikan berbeda-beda)
- Item mengukur konstruk yang berbeda dari yang dimaksud
- Terlalu banyak *unique variance* atau error pengukuran

**Tindakan yang disarankan:**
1. Cek ulang redaksi item — apakah ambigu?
2. Pertimbangkan revisi item sebelum dihapus
3. Jika tetap rendah → hapus dan jalankan ulang analisis
4. Laporkan item yang dihapus beserta alasannya

**Contoh keputusan:**

| Item | h² | Tindakan |
|------|:--:|----------|
| EE1 | .68 | ✓ Pertahankan |
| IO2 | .55 | ✓ Pertahankan |
| Item X | .24 | ✗ Evaluasi ulang — kemungkinan hapus |

---

## BAGIAN 4: Evaluasi Model dan Reliabilitas (5 slides)

---

### Slide 28: Section Divider

```
BAGIAN 4
Evaluasi Model dan Reliabilitas
```

---

### Slide 29: Fit indices — seberapa baik model EFA menjelaskan data? (khusus ML)

**Judul:** Fit indices hanya tersedia jika menggunakan ML extraction — tapi sangat informatif

**Konten:**

**Chi-square (χ²):**
- H₀: Model fit sempurna
- p > .05 = fit baik
- **Masalah:** Sangat sensitif terhadap N besar → selalu signifikan jika N > 300, meskipun fit sebenarnya baik. Jangan jadikan satu-satunya kriteria.

**RMSEA (Root Mean Square Error of Approximation):**

| RMSEA | Interpretasi |
|-------|-------------|
| < .05 | Fit sangat baik |
| .05 – .08 | Fit cukup baik |
| .08 – .10 | Fit buruk (*mediocre*) |
| > .10 | Fit tidak dapat diterima |

Selalu sertakan **90% CI** untuk RMSEA.

**Catatan:** Ambang batas RMSEA < .06 (Hu & Bentler, 1999) sering dikutip sebagai "fit baik," tetapi ini berasal dari simulasi dengan kondisi spesifik. Untuk model dengan banyak indikator atau sampel besar, RMSEA < .08 sudah dapat diterima — jangan terlalu kaku pada angka .06.

**CFI dan TLI (Comparative/Tucker-Lewis Fit Index):**
- > .95: Fit baik
- > .90: Fit dapat diterima
- TLI memberi penalti lebih besar untuk kompleksitas model

**Contoh output:**
χ²(102) = 145.6, p = .004
CFI = .97, TLI = .96
RMSEA = .04, 90% CI [.02, .06]
→ **Fit sangat baik!**

---

### Slide 30: Interpretasi factor loadings — panduan membaca matriks

**Judul:** Loadings menunjukkan seberapa kuat item "berbicara tentang" faktor

**Konten:**

**Panduan threshold (Tabachnick & Fidell, 2019):**

| |Loading| | Variansi bersama | Keterangan |
|---------|:---:|:----------------:|:----------:|
| > .71 | 50% | Excellent |
| > .63 | 40% | Very good |
| > .55 | 30% | Good |
| > .45 | 20% | Fair |
| > .32 | 10% | Minimal |

**Praktis:**
- **Primary loading:** |λ| > 0.40 — item dianggap "milik" faktor ini
- **Suppress di output:** |λ| < 0.30 — sembunyikan untuk kejelasan
- **Cross-loading:** Item load > 0.30 pada *lebih dari satu* faktor → bermasalah

**Contoh cross-loading yang bermasalah:**

| Item | F1 | F2 | F3 | Keputusan |
|------|:--:|:--:|:--:|-----------|
| EE1 | .72 | .08 | −.05 | ✓ Bersih |
| **Item B** | **.55** | **.48** | .12 | ✗ Cross-loading |
| IO1 | .09 | .81 | .06 | ✓ Bersih |

**Solusi untuk cross-loading:** (1) Hapus item; (2) Revisi redaksi item; (3) Izinkan item di dua faktor jika ada alasan teoritis yang kuat.

---

### Slide 31: Memberi nama faktor — proses teoritis, bukan mekanis

**Judul:** Nama faktor harus mencerminkan konstruk psikologis yang mendasari, bukan sekadar label deskriptif

**Konten:**

**Langkah interpretasi:**
1. Identifikasi item dengan *primary loading* tertinggi pada setiap faktor
2. Baca konten item-item tersebut — apa yang sama?
3. Beri nama yang mencerminkan konstruk laten — bukan nama item-nya
4. Periksa apakah ada item dengan muatan *negatif* — interpretasikan arahnya
5. Cek *cross-loading* — item ambigu menunjukkan batas konstruk yang tidak jelas

**Contoh:**
Faktor dengan loading tinggi pada: "Merasa lelah", "Merasa terkuras", "Merasa overwhelmed" setelah menggunakan medsos
→ Nama: **Kelelahan Emosional** (bukan "Faktor Lelah" atau "Faktor Medsos")

**Jebakan umum:**
- Memberi nama berdasarkan satu item saja — butuh minimal 3 item untuk konstruk yang bermakna
- Nama terlalu sempit (nama satu item) atau terlalu luas (tidak mencerminkan isi spesifik)
- Mengabaikan item dengan loading negatif

---

### Slide 32: Cronbach's Alpha — reliabilitas internal konsistensi

**Judul:** Alpha mengukur konsistensi internal — seberapa "kompak" item mengukur hal yang sama

**Konten:**

**Cronbach's α:** Proporsi variansi skor total yang disebabkan oleh *true score* (bukan error).

**Interpretasi:**

| α | Keterangan |
|---|------------|
| > .90 | Excellent (perhatikan: mungkin redundan jika item sangat mirip) |
| .80 – .90 | Baik |
| .70 – .80 | Dapat diterima |
| .60 – .70 | Questionable |
| < .60 | Tidak memadai |

**Contoh SMF Scale:**
- Kelelahan Emosional: α = .88 ✓
- Information Overload: α = .85 ✓
- Privacy Concerns: α = .82 ✓

**Dua catatan penting:**
1. **Alpha sensitif terhadap jumlah item** — lebih banyak item → alpha lebih tinggi, bahkan jika loadings biasa-biasa saja. Alpha tinggi ≠ otomatis bagus.
2. **Alpha mengasumsikan tau-equivalence** — semua item punya bobot kontribusi yang sama terhadap konstruk. Jika tidak (loadings berbeda-beda), alpha *underestimates* reliabilitas yang sebenarnya.

---

### Slide 33: McDonald's Omega — alternatif yang lebih akurat

**Judul:** Omega berbasis model faktor — lebih akurat saat loadings item tidak setara

**Konten:**

**Keterbatasan Alpha:**
Alpha mengasumsikan semua item berkontribusi *sama* terhadap konstruk (*tau-equivalence*). Jika loading berbeda (yang hampir selalu terjadi), alpha bisa bias.

**McDonald's ω (Omega):**
Dihitung langsung dari factor loadings — tidak mengasumsikan tau-equivalence.

$$\omega = \frac{(\sum \lambda_i)^2}{(\sum \lambda_i)^2 + \sum (1 - \lambda_i^2)}$$

**Perbandingan:**

| Faktor | α | ω | Selisih |
|--------|---|---|---------|
| Kelelahan Emosional | .88 | .90 | Kecil — loadings relatif setara |
| Faktor hipotetis | .78 | .86 | Besar — alpha underestimate |

**Rekomendasi:** Laporkan keduanya — α dan ω. Jika ω > α, berarti item punya loadings yang tidak setara (tau-equivalence terlanggar).

**Referensi:** McNeish (2018) merekomendasikan omega sebagai pengganti alpha secara default dalam psikologi, terutama saat item loadings bervariasi — kasus yang hampir universal dalam skala psikologi nyata.

**Software:** JASP (tersedia langsung), R (`psych` package: `omega()`), jamovi (plugin `jmv`).

---

## BAGIAN 5: PCA vs EFA — Kapan Menggunakan yang Mana? (3 slides)

---

### Slide 34: Section Divider

```
BAGIAN 5
PCA vs EFA — Kapan Menggunakan yang Mana?
```

---

### Slide 35: Gunakan PCA ketika tujuannya reduksi dimensi

**Judul:** PCA adalah alat kompresi data — tidak ada asumsi tentang konstruk laten

**Konten:**

**Tujuan utama:** Mereduksi banyak variabel menjadi sedikit variabel ringkasan (*summary variables*), sambil mempertahankan sebanyak mungkin informasi.

**Use cases yang tepat:**
✓ Membuat indeks komposit dari banyak prediktor untuk analisis regresi
✓ Reduksi dimensi untuk visualisasi (scatter plot PC1 vs PC2)
✓ Feature extraction untuk machine learning
✓ Tidak ada teori tentang konstruk laten yang mendasari

**Contoh di psikologi:**
- Neuroimaging: 100.000 voxel → 10 *principal components* sebagai prediktor
- Data perilaku konsumen: 50 kategori pembelian → 5 komponen ringkasan

**Keunggulan:** Lebih cepat, lebih sederhana, tidak ada asumsi model pengukuran.

**Keterbatasan:** Komponen mungkin tidak bermakna secara psikologis — hanya meringkas variansi, bukan mengidentifikasi konstruk.

---

### Slide 36: Gunakan EFA ketika tujuannya menemukan atau memvalidasi konstruk laten

**Judul:** EFA adalah alat psikometri — digunakan untuk pengembangan dan validasi skala

**Konten:**

**Tujuan utama:** Mengidentifikasi *latent constructs* yang menjelaskan pola korelasi antar item.

**Use cases yang tepat:**
✓ Pengembangan skala baru (skala kepuasan kerja, skala kecemasan)
✓ Memvalidasi struktur skala yang sudah ada di populasi baru
✓ Menguji dimensionalitas konstruk psikologis
✓ Langkah awal sebelum CFA (Confirmatory Factor Analysis)
✓ Ada teori tentang faktor laten yang mendasari item

**Contoh di psikologi:**
- Pengembangan Big Five: item NEO-PI-R → 5 faktor kepribadian
- Validasi BDI-II: 21 item depresi → 2–3 faktor (kognitif-afektif, somatik)
- Pengembangan SMF Scale: 18 item → 3 faktor kelelahan medsos

**Keunggulan:** Berdasarkan model pengukuran yang eksplisit; memisahkan *common variance* dari *unique variance*.

---

### Slide 37: Hasil PCA dan EFA sering konvergen — tapi berbeda saat data bermasalah

**Judul:** Jika komunalitas tinggi dan struktur jelas, PCA ≈ EFA — perbedaan muncul ketika data kompleks

**Konten:**

**Kapan hasil konvergen (PCA ≈ EFA):**
- Komunalitas tinggi (> 0.60)
- Simple structure jelas
- N cukup besar

→ Dalam kondisi ini, pilihan metode tidak terlalu kritis secara praktis.

**Kapan hasil divergen (EFA lebih reliabel):**
- Komunalitas rendah (< 0.40) — PCA melebih-lebihkan kontribusi faktor
- Struktur kompleks dengan banyak cross-loading
- N kecil

**Praktik terbaik:**
1. **Jalankan keduanya**, bandingkan hasilnya
2. **Laporkan metode secara eksplisit** di artikel — pembaca perlu tahu
3. **Gunakan teori** untuk membenarkan pilihan
4. **Tujuan menentukan pilihan:**
   - Analisis eksplorasi → keduanya umumnya OK
   - Pengembangan skala → pilih EFA
   - Reduksi data untuk ML → pilih PCA

---

## BAGIAN 6: Aplikasi dalam Penelitian Psikologi (4 slides)

---

### Slide 38: Section Divider

```
BAGIAN 6
Aplikasi dalam Penelitian Psikologi
```

---

### Slide 39: Big Five Personality — model kepribadian yang paling teruji

**Judul:** EFA menemukan Big Five secara empiris — sebelum ada teori yang memprediksinya

**Konten:**

**Costa & McCrae (1992): NEO-PI-R**
- 240 item, skala *self-report*
- Divalidasi lintas budaya di > 50 negara (McCrae & Terracciano, 2005)

**Lima faktor yang konsisten muncul:**
1. **Openness to Experience** — rasa ingin tahu, kreativitas, keterbukaan estetika
2. **Conscientiousness** — disiplin, terorganisir, berorientasi tujuan
3. **Extraversion** — sosiabilitas, asertivitas, afek positif
4. **Agreeableness** — kepercayaan, kooperatif, empati
5. **Neuroticism** — kecemasan, impulsivitas, ketidakstabilan emosi

**Robustness yang luar biasa:**
- Direplikasi dengan metode *self-report* dan *peer-report*
- Stabil sepanjang rentang hidup
- Berbagai bahasa dan budaya

**Catatan:** Big Five *ditemukan* dari EFA — bukan dihipotesiskan lebih dulu. Ini contoh ideal bagaimana EFA bekerja dalam pembangunan teori psikologi.

---

### Slide 40: Beck Depression Inventory-II (BDI-II) — faktor yang menginformasikan intervensi

**Judul:** Dua subskala BDI-II mengidentifikasi subtipe depresi yang berbeda secara klinis

**Konten:**

**BDI-II:** 21 item mengukur keparahan gejala depresi; skala 0–3 per item.

**Struktur faktor yang konsisten ditemukan lintas studi:**

| Faktor | Item yang masuk | Contoh item |
|--------|-----------------|-------------|
| **Kognitif-Afektif** | 13 item | Sedih, pesimis, rasa bersalah, harga diri rendah, pikiran bunuh diri |
| **Somatik** | 8 item | Kelelahan, gangguan tidur, perubahan nafsu makan, konsentrasi |

**Relevansi klinis:**
- Gejala kognitif-afektif → merespons lebih baik terhadap terapi kognitif-behavioral
- Gejala somatik → mungkin merespons lebih baik terhadap farmakoterapi
- Monitoring per subskala memberikan informasi lebih kaya dibanding skor total saja

**Catatan:** Struktur 2 vs 3 faktor masih diperdebatkan di literatur — faktor ketiga (*performance*: kesulitan kerja, pengambilan keputusan) muncul di beberapa sampel tapi tidak konsisten.

---

### Slide 41: Social Media Fatigue Scale — pengembangan skala kontemporer

**Judul:** SMF Scale mendemonstrasikan workflow EFA dari pengembangan item hingga validasi

**Konten:**

**Dhir et al. (2018)** meneliti kelelahan media sosial (*social media fatigue*) dan kaitannya dengan *psychological wellbeing*.
(*International Journal of Information Management*, 40, 141–152)

**Konteks penelitian:** Pengguna media sosial aktif (mahasiswa dan profesional muda).

**Tiga dimensi kelelahan media sosial yang diidentifikasi:**
1. **Emotional Exhaustion** — merasa lelah, terkuras, overwhelmed setelah menggunakan medsos
2. **Information Overload** — kelebihan informasi, sulit memfilter konten
3. **Privacy Concerns** — kekhawatiran tentang keamanan data dan privasi

**Ilustrasi hasil EFA (data simulasi pedagogis; N = 500, 3 faktor):**

| Faktor | Jumlah Item | α | % Variansi |
|--------|:-----------:|:-:|:----------:|
| Emotional Exhaustion | 6 | .88 | 30.0% |
| Information Overload | 6 | .85 | 17.8% |
| Privacy Concerns | 6 | .82 | 11.7% |

*Catatan: angka di atas adalah ilustrasi untuk keperluan pembelajaran; lihat artikel asli untuk hasil empiris.*

**Fit model ilustrasi:** KMO = .89, Bartlett p < .001, CFI = .96, RMSEA = .05

**Aplikasi:**
- Memprediksi *social media discontinuance* (berhenti menggunakan)
- Memahami *digital wellbeing*
- Dasar desain fitur platform yang lebih manusiawi

---

## BAGIAN 7: Pelaporan Hasil EFA (3 slides)

---

### Slide 42: Section Divider

```
BAGIAN 7
Pelaporan Hasil EFA
```

---

### Slide 43: Elemen wajib dalam laporan EFA

**Judul:** Laporan EFA yang baik memungkinkan pembaca mereplikasi dan mengevaluasi keputusan analisis

**Konten:**

**Checklist pelaporan (Costello & Osborne, 2005; Fabrigar et al., 1999):**

☐ **Deskripsi sampel** — N, karakteristik, cara pengumpulan data

☐ **Prosedur analisis:**
- Software yang digunakan
- Metode ekstraksi (MinRes/ML/PAF)
- Kriteria penentuan jumlah faktor (parallel analysis, scree, Kaiser)
- Metode dan jenis rotasi

☐ **Kelayakan analisis:**
- Nilai KMO
- Hasil Bartlett's test (χ², df, p)

☐ **Hasil ekstraksi:**
- Jumlah faktor yang dipertahankan
- Eigenvalue tiap faktor
- % variansi yang dijelaskan tiap faktor dan total

☐ **Matriks loading faktor** (setelah rotasi; *pattern matrix* untuk oblique)
- Sertakan komunalitas (h²)
- Korelasi antar faktor jika rotasi oblique

☐ **Reliabilitas:**
- Cronbach's α dan/atau McDonald's ω per faktor

☐ **Fit indices** (jika ML extraction): RMSEA + 90% CI, CFI, TLI

---

### Slide 44: Contoh paragraf hasil dan tabel APA

**Judul:** Cara melaporkan EFA sesuai APA 7th

**Konten:**

**Contoh paragraf:**

> "An exploratory factor analysis was conducted on the 18-item Social Media Fatigue Scale using minimum residual extraction with Direct Oblimin rotation. The Kaiser-Meyer-Olkin measure of sampling adequacy was .89 and Bartlett's test of sphericity was significant (χ²(153) = 2456.3, *p* < .001), indicating that the data were suitable for factor analysis. The number of factors to retain was determined using parallel analysis, yielding three factors that explained 59.4% of the total variance. Factor loadings, communalities, and factor intercorrelations are presented in Table 1. Internal consistency was acceptable for all three subscales: Emotional Exhaustion (α = .88, ω = .90), Information Overload (α = .85, ω = .87), and Privacy Concerns (α = .82, ω = .84)."

**Format tabel (APA-style):**

| Item | F1 Emosi | F2 Info | F3 Privasi | h² |
|------|:--------:|:-------:|:----------:|:--:|
| EE1 "Merasa lelah emosional" | **.82** | .15 | −.05 | .68 |
| EE2 "Merasa terkuras" | **.79** | .08 | .10 | .72 |
| IO1 "Terlalu banyak informasi" | .10 | **.85** | .06 | .65 |
| PC1 "Khawatir privasi" | −.02 | .11 | **.78** | .70 |
| Eigenvalue | 5.4 | 3.2 | 2.1 | |
| % Variance | 30.0% | 17.8% | 11.7% | |
| α / ω | .88 / .90 | .85 / .87 | .82 / .84 | |

*Note.* N = 500. Loadings < .30 disembunyikan. Rotasi: Direct Oblimin.

---

### Slide 45: Kesalahan umum dalam EFA

**Judul:** Tujuh kesalahan yang sering muncul dalam artikel psikologi

**Konten:**

**1. Menggunakan Kaiser criterion saja**
Menghasilkan terlalu banyak faktor secara konsisten. Selalu gunakan parallel analysis.

**2. Menggunakan PCA untuk pengembangan skala**
PCA bukan model pengukuran. Untuk pengembangan skala, gunakan EFA.

**3. Rotasi orthogonal tanpa alasan**
Konstruk psikologi hampir selalu berkorelasi. Default ke oblique kecuali ada alasan independensi.

**4. Mengabaikan cross-loadings**
Item dengan cross-loading > 0.30 menandakan definisi konstruk yang tidak jelas — jangan diabaikan.

**5. Memaksakan jumlah faktor yang diinginkan**
"Saya ingin 5 faktor" → analisis dipaksakan menghasilkan 5 faktor tanpa memeriksa bukti empiris.

**6. Hanya melaporkan item yang "berhasil"**
Laporkan semua item, termasuk yang dihapus dan alasannya — transparansi adalah kewajiban ilmiah.

**7. Tidak melakukan CFA di sampel independen**
EFA hanya eksplorasi. Validasi struktur yang ditemukan selalu harus dilakukan dengan CFA di sampel berbeda.

---

## BAGIAN 8: Aplikasi di JASP/jamovi (3 slides)

---

### Slide 46: Section Divider

```
BAGIAN 8
Aplikasi di JASP/jamovi
```

---

### Slide 47: Menjalankan PCA dan EFA di JASP/jamovi

**Judul:** Centang output yang relevan sejak awal — KMO, parallel analysis, dan reliabilitas

**Konten:**

**Di JASP:**

**PCA:**
1. **Factor → Principal Component Analysis**
2. Masukkan semua item ke "Variables"
3. Di **"Number of Components":** pilih *Parallel Analysis*
4. Di **"Rotation":** pilih *Varimax* (orthogonal) atau *Oblimin* (oblique)
5. Centang: ☑ Component loadings, ☑ Scree plot, ☑ Path diagram

**EFA:**
1. **Factor → Exploratory Factor Analysis**
2. Masukkan semua item ke "Variables"
3. Di **"Extraction method":** pilih *Minimum Residual* (default aman)
4. Di **"Rotation":** pilih *Oblimin* atau *Promax*
5. Centang: ☑ Factor loadings, ☑ Parallel analysis, ☑ Scree plot, ☑ KMO, ☑ Bartlett's

**Di jamovi:**
1. **Factor → Principal Component Analysis** atau **Exploratory Factor Analysis**
2. Isi "Variables"
3. Di tab **"Extraction":** pilih metode dan centang *Parallel Analysis*
4. Di tab **"Rotation":** pilih jenis rotasi
5. Di tab **"Assumption Checks":** centang KMO dan Bartlett's

---

### Slide 48: Membaca output EFA secara sistematis

**Judul:** Baca output dalam urutan: asumsi → jumlah faktor → loadings → reliabilitas

**Konten:**

**Urutan membaca output yang benar:**

**Langkah 1 — Cek asumsi:**
KMO = ? (harus > 0.60, idealnya > 0.80)
Bartlett's test: p < .05?
→ Jika tidak terpenuhi: data belum siap untuk EFA

**Langkah 2 — Tentukan jumlah faktor:**
Lihat hasil parallel analysis + scree plot + Kaiser
→ Ambil keputusan berdasarkan konvergensi ketiga kriteria

**Langkah 3 — Baca pattern matrix (rotasi oblique) atau factor matrix (rotasi orthogonal):**
- Identifikasi *salient loadings* (|λ| > 0.40)
- Tandai cross-loadings (|λ| > 0.30 di lebih dari satu faktor)
- Cek komunalitas — ada yang < 0.30?

**Langkah 4 — Interpretasi dan beri nama faktor:**
Baca konten item dengan loading tertinggi → apa konstruk psikologis yang mendasarinya?

**Langkah 5 — Cek reliabilitas:**
α dan ω per faktor — apakah > 0.70?

**Langkah 6 — Cek fit indices (jika ML):**
RMSEA < .08? CFI > .90?

---

## CLOSING (3 slides)

---

### Slide 49: Take-home messages

**Judul:** Yang perlu dibawa pulang dari pertemuan hari ini

**Konten:**

✓ **PCA untuk reduksi dimensi** — merangkum banyak variabel menjadi sedikit komponen, tanpa asumsi konstruk laten

✓ **EFA untuk identifikasi konstruk laten** — model pengukuran yang eksplisit; tepat untuk pengembangan dan validasi skala

✓ **Parallel analysis** lebih akurat dibanding Kaiser criterion — gunakan sebagai kriteria utama penentuan jumlah faktor

✓ **Oblique rotation default** untuk psikologi — konstruk psikologis hampir selalu berkorelasi; gunakan Promax atau Direct Oblimin

✓ **Komunalitas < 0.30** = sinyal item bermasalah — evaluasi dan pertimbangkan penghapusan

✓ **KMO > 0.80 dan Bartlett p < .05** — cek wajib sebelum analisis

✓ **Laporkan α dan ω** — jangan hanya alpha; omega lebih akurat jika loadings item tidak setara

✓ **EFA adalah langkah awal** — validasi struktur dengan CFA di sampel independen sebelum skala dipublikasikan

✓ **Laporkan dengan transparan** — metode ekstraksi, rotasi, kriteria retensi faktor, semua item (termasuk yang dihapus)

---

### Slide 50: Dataset demo — Academic Burnout Scale

**Judul:** Dataset demo: Academic Burnout Scale (N = 350)

**Konten:**

**File:** `Demo_AkademikBurnout.csv` (tersedia di folder `slides plan/`)

**Konteks penelitian:** Data simulasi yang merepresentasikan burnout akademik mahasiswa pascasarjana. Skala terinspirasi dari Maslach Burnout Inventory—Student Survey (MBI-SS; Schaufeli et al., 2002).

**Variabel demografis:**
- `usia`: 20–35 tahun
- `jenis_kelamin`: 0 = Laki-laki, 1 = Perempuan
- `semester`: semester aktif (1–4)
- `ipk`: Indeks Prestasi Kumulatif (2.00–4.00)

**Variabel item (15 item, skala Likert 1–5):**
- `ab_ee_1` s.d. `ab_ee_5`: *Emotional Exhaustion* — merasa lelah, terkuras, kehabisan energi karena tuntutan akademik
- `ab_cy_1` s.d. `ab_cy_5`: *Cynicism* — sikap jarak, tidak peduli, pesimis terhadap studi
- `ab_ef_1` s.d. `ab_ef_5`: *Academic Efficacy* — keyakinan pada kemampuan akademik diri sendiri (skor tinggi = efikasi tinggi)

**Hasil yang diharapkan:**
- KMO ≈ 0.87 ✓; Bartlett p < .001 ✓
- Eigenvalue: 6.29, 2.16, 1.37 → lalu turun ke 0.62 (elbow jelas di faktor ke-3)
- Parallel analysis: 3 faktor
- EE items load pada Faktor 1; CY items pada Faktor 2; EF items pada Faktor 3
- Komunalitas rata-rata ≈ 0.60–0.65
- α ≈ .88 (EE) / .87 (CY) / .84 (EF)
- 65.5% total variansi dijelaskan oleh 3 faktor

**Catatan penting untuk demonstrasi:**
Faktor EF (*Academic Efficacy*) berkorelasi *negatif* dengan EE dan CY — ini contoh yang bagus untuk mendiskusikan arah korelasi antar faktor dalam rotasi oblique.

---

### Slide 51: Referensi

**Judul:** Referensi

**Konten:**

**Textbooks:**
- Brown, T. A. (2015). *Confirmatory Factor Analysis for Applied Research* (2nd ed.). Guilford Press.
- Fabrigar, L. R., & Wegener, D. T. (2012). *Exploratory Factor Analysis*. Oxford University Press.
- Tabachnick, B. G., & Fidell, L. S. (2019). *Using Multivariate Statistics* (7th ed.). Pearson.

**Artikel metodologi:**
- Cattell, R. B. (1966). The scree test for the number of factors. *Multivariate Behavioral Research*, *1*(2), 245–276.
- Comrey, A. L., & Lee, H. B. (1992). *A First Course in Factor Analysis* (2nd ed.). Erlbaum.
- Costello, A. B., & Osborne, J. (2005). Best practices in exploratory factor analysis. *Practical Assessment, Research, and Evaluation*, *10*(7), 1–9.
- Fabrigar, L. R., Wegener, D. T., MacCallum, R. C., & Strahan, E. J. (1999). Evaluating the use of exploratory factor analysis in psychological research. *Psychological Methods*, *4*(3), 272–299.
- Hayton, J. C., Allen, D. G., & Scarpello, V. (2004). Factor retention decisions in exploratory factor analysis: A tutorial on parallel analysis. *Organizational Research Methods*, *7*(2), 191–205.
- Howard, M. C. (2016). A review of exploratory factor analysis decisions and overview of current practices. *Organizational Research Methods*, *19*(1), 2–32.
- Hu, L., & Bentler, P. M. (1999). Cutoff criteria for fit indexes in covariance structure analysis. *Structural Equation Modeling*, *6*(1), 1–55.
- McNeish, D. (2018). Thanks coefficient alpha, we'll take it from here. *Psychological Methods*, *23*(3), 412–433.
- Revelle, W., & Zinbarg, R. E. (2009). Coefficients alpha, beta, omega, and the glb. *Psychometrika*, *74*(1), 145–154.
- Zwick, W. R., & Velicer, W. F. (1986). Comparison of five rules for determining the number of components to retain. *Psychological Bulletin*, *99*(3), 432–442.

**Studi yang dikutip:**
- Costa, P. T., & McCrae, R. R. (1992). *Revised NEO Personality Inventory (NEO-PI-R) and NEO Five-Factor Inventory (NEO-FFI) professional manual*. Psychological Assessment Resources.
- Dhir, A., Yossatorn, Y., Kaur, P., & Chen, S. (2018). Online social media fatigue and psychological wellbeing. *International Journal of Information Management*, *40*, 141–152.
- McCrae, R. R., & Terracciano, A. (2005). Universal features of personality traits from the observer's perspective. *Journal of Personality and Social Psychology*, *88*(3), 547–561.

---

**Versi:** 1.1
**Dibuat:** 2026-03-25
**Direvisi:** 2026-03-27 (v1.2: PENGANTAR variabel laten ditambahkan sebagai Slides 3-7)
**Penulis:** Dr. Rizqy Amelia Zein, M.Sc. (dengan Claude Code)
**Sumber:** Gabungan dari `Pertemuan11-12_PCA_EFA_REVISED.md` (v2.0) dan `Analisis Faktor Eksploratori dalam Psikologi S2(1).md`; akurasi referensi dicek ulang
