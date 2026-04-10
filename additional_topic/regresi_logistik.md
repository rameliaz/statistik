# Regresi Logistik Binomial
## Rencana Slide — Statistik Multivariat S2 Psikologi

**Mata Kuliah:** Statistik Multivariat (FPS25801008)
**Program:** Magister Psikologi, Universitas Airlangga
**Pengampu:** Dr. Rizqy Amelia Zein, M.Sc.
**Durasi:** 2 pertemuan (Pertemuan 9: Kuliah; Pertemuan 10: Praktikum)
**Versi:** 1.0 (gabungan dari dua draft sebelumnya; akurasi sumber dicek ulang)

---

## OPENING (2 slides)

---

### Slide 1: Title Slide

```
REGRESI LOGISTIK BINOMIAL
Memprediksi Probabilitas dari Outcome Kategorikal

Statistik Multivariat
Magister Psikologi, Universitas Airlangga
Dr. Rizqy Amelia Zein, M.Sc.
Semester Genap 2025/26
```

---

### Slide 2: Banyak outcome psikologi berbentuk ya/tidak

**Judul:** Banyak outcome penting dalam psikologi bukan skor — melainkan keputusan

**Konten:**
- **Putus studi di PJJ:** Studi di berbagai program pendidikan jarak jauh menunjukkan angka putus studi yang konsisten tinggi — sampai sepertiga mahasiswa tidak menyelesaikan studinya (Tinto, 1987; Park & Choi, 2009)
- **Relapse gangguan kecemasan:** 40–60% pasien mengalami kekambuhan dalam jangka panjang setelah remisi (Bruce et al., 2005, *American Journal of Psychiatry*)
- **Turnover karyawan:** 15–20% per tahun dianggap normal; di atas angka itu menandakan masalah organisasi (SHRM, 2023)
- **Percobaan bunuh diri:** 2.4% prajurit militer AS melakukan percobaan bunuh diri dalam satu tahun (Kessler et al., 2014, *Molecular Psychiatry*)

**Narasi:** "Outcome ini bukan skor 1–100. Mereka adalah keputusan biner: terjadi atau tidak terjadi. Kita butuh metode statistik yang dirancang untuk memodelkan probabilitas kejadian seperti ini."

---

## BAGIAN 1: Mengapa Regresi Logistik? (2 slides)

---

### Slide 3: Section Divider

```
BAGIAN 1
Mengapa Regresi Logistik?
```

---

### Slide 4: Regresi linear menghasilkan prediksi yang mustahil untuk outcome biner

**Judul:** Regresi linear bisa memprediksi probabilitas > 1 atau < 0 — keduanya tidak mungkin

**Konten:**

Kita ingin memprediksi putus studi mahasiswa PJJ berdasarkan jarak ke pokjar (kelompok belajar).

**Jika menggunakan regresi linear (OLS):**

| Mahasiswa | Jarak ke pokjar | Prediksi P(putus studi) | Valid? |
|-----------|-----------------|--------------------------|--------|
| A | 5 km | 0.25 | ✓ |
| B | 50 km | **1.45** | ✗ Tidak mungkin! |
| C | 0 km | **−0.10** | ✗ Tidak mungkin! |

**Masalah fundamental:** Probabilitas harus berada di rentang 0 sampai 1. Regresi linear tidak menjamin ini karena ia memodelkan hubungan linear tanpa batas.

**Solusi yang dibutuhkan:** Fungsi yang secara otomatis membatasi prediksi dalam rentang [0, 1] — itulah fungsi logistik.

---

### Slide 5: Fungsi logistik mengubah nilai tak terbatas menjadi probabilitas

**Judul:** Kurva S (sigmoid) menjamin prediksi selalu valid

**Konten:**

**Fungsi logistik:**
$$P = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X)}}$$

**Tiga sifat penting kurva S (sigmoid):**
- Asimptot bawah = 0 — probabilitas tidak pernah negatif
- Asimptot atas = 1 — probabilitas tidak pernah melampaui 1
- Transisi halus di bagian tengah — perubahan probabilitas melambat di ujung-ujungnya

**Artinya:** Tidak peduli seberapa ekstrim nilai prediktor — jarak 100 km sekalipun — probabilitas yang diprediksi tetap berada dalam rentang yang valid.

**Visual:** Plot kurva S dengan sumbu X = "Jarak ke pokjar (km)" dan sumbu Y = "P(putus studi)"; bandingkan dengan garis lurus OLS yang keluar batas [0, 1].

---

## BAGIAN 2: Konsep Dasar (6 slides)

---

### Slide 6: Section Divider

```
BAGIAN 2
Probabilitas, Odds, Log Odds, dan Odds Ratio
```

---

### Slide 7: Probabilitas — bahasa yang sudah kita kenal

**Judul:** Probabilitas adalah titik awal — tapi bukan yang dimodelkan secara langsung

**Konten:**

**Definisi:** Proporsi kejadian dalam populasi; rentang 0 sampai 1.

$$P(A) = \frac{\text{jumlah kejadian A}}{\text{total kemungkinan}}$$

**Contoh dari penelitian psikologi:**

| Konteks | Probabilitas |
|---------|--------------|
| 135 dari 450 mahasiswa PJJ putus studi | P(putus studi) = 0.30 |
| 8 dari 200 mahasiswa pernah mencoba bunuh diri | P(attempt) = 0.04 |
| 60 dari 200 karyawan resign dalam 1 tahun | P(turnover) = 0.30 |

**Narasi:** "Kita sudah familiar dengan probabilitas. Tapi regresi logistik tidak memodelkan P secara langsung — ia memodelkan transformasinya, yaitu log odds. Mengapa? Karena P tidak linear, sementara log odds bisa diperlakukan sebagai linear."

---

### Slide 8: Odds = "berapa kali lebih mungkin terjadi dibanding tidak terjadi"

**Judul:** Odds mengekspresikan probabilitas sebagai perbandingan, bukan proporsi

**Konten:**

$$\text{Odds} = \frac{P}{1 - P}$$

**Contoh:** Jika P(putus studi) = 0.30:
- Odds = 0.30 / 0.70 = **0.43**
- Cara baca: "Untuk setiap 7 mahasiswa yang bertahan, ada 3 yang putus studi" (atau 3:7)

**Perbandingan P dan Odds:**

| P(kejadian) | Odds | Cara baca |
|-------------|------|-----------|
| 0.10 | 0.11 | 1 banding 9 |
| 0.25 | 0.33 | 1 banding 3 |
| 0.50 | 1.00 | Sama rata |
| 0.75 | 3.00 | 3 banding 1 |
| 0.90 | 9.00 | 9 banding 1 |

**Catatan penting:** Odds = 1 artinya peluang terjadi sama dengan tidak terjadi. Odds > 1 artinya kejadian lebih mungkin terjadi; Odds < 1 artinya lebih tidak mungkin.

---

### Slide 9: Log odds (logit) membuat odds menjadi simetris dan linear

**Judul:** Logit = ln(Odds) — transformasi yang membuat regresi logistik bisa bekerja

**Konten:**

**Masalah odds:** Rentangnya 0 sampai ∞, dan tidak simetris — nilai di bawah 1 terkompresi.

**Solusi: Log odds (logit)**
$$\text{Logit}(P) = \ln\!\left(\frac{P}{1 - P}\right)$$

**Sifat penting logit:**
- Rentang: −∞ sampai +∞ (simetris di sekitar 0)
- Logit = 0 → P = 0.50 (odds sama rata)
- Logit positif → P > 0.50 (lebih mungkin terjadi)
- Logit negatif → P < 0.50 (lebih tidak mungkin terjadi)

**Ilustrasi transformasi:**

| P | Odds | Logit |
|---|------|-------|
| 0.10 | 0.11 | −2.20 |
| 0.25 | 0.33 | −1.10 |
| 0.50 | 1.00 | 0.00 |
| 0.75 | 3.00 | +1.10 |
| 0.90 | 9.00 | +2.20 |

**Kunci:** Regresi logistik memodelkan logit(P) sebagai fungsi linear dari prediktor — lalu kita balik transformasinya untuk mendapatkan P.

---

### Slide 10: Persamaan model regresi logistik

**Judul:** Model regresi logistik = persamaan linear dalam logit, bukan dalam P

**Konten:**

**Persamaan dalam logit:**
$$\ln\!\left(\frac{P}{1 - P}\right) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_k X_k$$

**Untuk memprediksi probabilitas, balik transformasinya:**
$$P = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X_1 + \cdots + \beta_k X_k)}}$$

**Komponen:**
- β₀ = intercept (log odds ketika semua prediktor = 0)
- β₁, …, βₖ = koefisien regresi (perubahan logit per satu unit prediktor)
- **e^β = Odds Ratio** — inilah yang diinterpretasikan dalam praktik

---

### Slide 11: Odds Ratio (OR) adalah ukuran efek utama dalam regresi logistik

**Judul:** OR = e^β — mengukur seberapa banyak odds berubah ketika prediktor naik 1 unit

**Konten:**

**Definisi:** OR = e^β = perubahan odds outcome ketika prediktor naik 1 unit, dengan prediktor lain dikontrol.

**Panduan interpretasi:**

| OR | Interpretasi |
|----|--------------|
| = 1.00 | Tidak ada efek |
| > 1.00 | Odds outcome *naik* |
| < 1.00 | Odds outcome *turun* |
| = 1.50 | Odds naik 50% |
| = 2.00 | Odds naik 100% (dua kali lipat) |
| = 0.67 | Odds turun 33% |
| = 0.50 | Odds turun 50% (setengahnya) |

**Selalu laporkan 95% Confidence Interval untuk OR!**

Jika CI melewati 1.0, prediktor tidak signifikan secara statistik (misal: OR = 1.20, 95% CI [0.85, 1.69] → tidak signifikan).

---

### Slide 12: Studi kasus: apa yang memprediksi putus studi mahasiswa PJJ?

**Judul:** Model tiga prediktor: jarak, keterlibatan akademik, dan kecemasan

**Konten:**

**Konteks:** 450 mahasiswa Pendidikan Jarak Jauh (PJJ); 30% putus studi sebelum semester ke-5.

**Prediktor:**
- Jarak ke pokjar/learning center (km)
- Keterlibatan akademik (skor 1–7; diukur di awal semester)
- Kecemasan akademik awal (skor 0–63)

**Hasil (ilustrasi pedagogis):**

| Prediktor | β | OR | 95% CI | p | Interpretasi |
|-----------|---|----|--------|---|--------------|
| Jarak (per 10 km) | 0.49 | 1.63 | [1.21, 2.19] | <.001 | Jarak +10 km → odds +63% |
| Keterlibatan akademik | −0.65 | 0.52 | [0.38, 0.71] | <.001 | Keterlibatan ↑ → odds −48% |
| Kecemasan akademik | 0.02 | 1.02 | [0.99, 1.05] | .182 | Tidak signifikan |

**Kesimpulan praktis:** Keterlibatan akademik yang tinggi dapat "melawan" efek jarak yang jauh — implikasi langsung untuk desain intervensi program PJJ.

---

## BAGIAN 3: Estimasi dan Fit Model (5 slides)

---

### Slide 13: Section Divider

```
BAGIAN 3
Estimasi dan Evaluasi Fit Model
```

---

### Slide 14: Maximum Likelihood Estimation — cara koefisien ditemukan

**Judul:** Regresi logistik tidak meminimalkan error — ia memaksimalkan kemungkinan data

**Konten:**

**Regresi linear (OLS):** Cari β yang meminimalkan jumlah kuadrat error (SSE).

**Regresi logistik (MLE):** Cari β yang membuat data yang kita observasi "paling mungkin terjadi."

**Intuisi MLE:**
Bayangkan berbagai kemungkinan nilai β. Nilai mana yang paling "mendukung" pola data yang kita lihat? Itulah yang dipilih MLE.

**Secara praktis:**
- Software (JASP, jamovi, R, SPSS) menghitung secara iteratif (algoritma Newton-Raphson)
- Proses berjalan dalam beberapa iterasi sampai *converge*
- Jika tidak converge: tanda adanya masalah — sampel terlalu kecil, atau ada *perfect separation* (lihat Bagian 5)

**Implikasi:** Karena MLE, kita tidak mendapatkan F-statistic seperti ANOVA. Kita mendapat **χ²** sebagai uji signifikansi.

---

### Slide 15: Deviance dan Likelihood Ratio Test — uji signifikansi keseluruhan model

**Judul:** Seberapa besar prediktor meningkatkan fit model dibanding model kosong?

**Konten:**

**Deviance** = −2 × log-likelihood (makin kecil, makin baik)

**Dua deviance yang dibandingkan:**

| | Deviance | Arti |
|---|---------|------|
| **Null deviance** | 612.4 | Model tanpa prediktor — "tebakan terbaik tanpa informasi" |
| **Residual deviance** | 487.2 | Model dengan prediktor kita |
| **Penurunan** | **125.2** | Bukti bahwa prediktor kita berguna |

**Likelihood Ratio Test:**
$$\chi^2 = \text{Null deviance} - \text{Residual deviance}$$
$$\chi^2(3) = 125.2,\ p < .001 \rightarrow \text{Model secara keseluruhan signifikan!}$$

**Narasi:** "Penurunan deviance sebesar 125.2 dengan 3 prediktor memberikan χ²(3) = 125.2, p < .001. Ini adalah uji omnibus — setara dengan uji F keseluruhan dalam regresi linear."

---

### Slide 16: AIC dan BIC — memilih model terbaik dengan penalti kompleksitas

**Judul:** Lebih banyak prediktor selalu menurunkan deviance — tapi belum tentu lebih baik

**Konten:**

**Masalah:** Menambah prediktor selalu menurunkan deviance, bahkan jika prediktor tersebut tidak bermakna (*overfitting*).

**Solusi:** AIC dan BIC memberi penalti untuk kompleksitas model.

$$\text{AIC} = -2\log L + 2k \qquad \text{BIC} = -2\log L + k\ln(n)$$

Di mana k = jumlah parameter, n = ukuran sampel. **Makin kecil, makin baik. Hanya bermakna untuk membandingkan model.**

**Contoh perbandingan:**

| Model | Prediktor | AIC | BIC | |
|-------|-----------|-----|-----|-|
| Model 1 | Jarak saja | 502.1 | 510.3 | |
| Model 2 | Jarak + Keterlibatan | 489.7 | 502.1 | ← Terbaik |
| Model 3 | Jarak + Keterlibatan + Usia + Gender | 493.2 | 518.9 | |

Model 2 menang: fit bagus tanpa terlalu kompleks. BIC lebih ketat dari AIC karena penaltinya lebih besar — pilih BIC jika prioritasnya parsimoni.

---

### Slide 17: Pseudo R² — seberapa banyak variasi yang dijelaskan model?

**Judul:** Pseudo R² bukan R² regresi linear — tapi tetap berguna sebagai indikator fit

**Konten:**

**Masalah:** Regresi logistik tidak punya R² sejati karena tidak ada "total variance" yang bisa dibagi.

**Dua versi yang paling sering dipakai:**

**McFadden's R²:**
$$R^2_{McFadden} = 1 - \frac{\log L_{\text{model}}}{\log L_{\text{null}}}$$

**Nagelkerke R²:** Versi yang sudah di-*adjust* agar rentangnya 0–1; yang paling sering dilaporkan.

**Pedoman interpretasi Nagelkerke R²:**

| Nagelkerke R² | Interpretasi |
|---------------|--------------|
| < 0.20 | Lemah |
| 0.20 – 0.40 | Cukup |
| 0.40 – 0.60 | Baik |
| > 0.60 | Sangat baik |

**Peringatan penting:** Pseudo R² bukan "proporsi varians yang dijelaskan" seperti R² OLS. Lebih tepat diartikan sebagai "peningkatan fit dibanding model kosong." Nilainya cenderung lebih rendah dari R² OLS, dan tidak bisa langsung dibandingkan.

---

### Slide 18: Prediktor kategorik membutuhkan dummy coding

**Judul:** Variabel kategorik diubah menjadi serangkaian variabel biner sebelum masuk model

**Konten:**

**Contoh:** Jalur registrasi PJJ (3 kategori): Tatap Muka Terbatas, Daring, Mandiri

**Cara kerja dummy coding:** K kategori → K−1 variabel dummy

| Jalur Registrasi | Dummy_Daring | Dummy_Mandiri |
|------------------|:------------:|:-------------:|
| Tatap Muka Terbatas *(referensi)* | 0 | 0 |
| Daring | 1 | 0 |
| Mandiri | 0 | 1 |

**Interpretasi OR untuk dummy:**

| Prediktor | OR | Interpretasi |
|-----------|----|--------------|
| Dummy_Daring | 0.85 | Daring vs. Tatap Muka: odds putus studi 15% lebih rendah |
| Dummy_Mandiri | 0.68 | Mandiri vs. Tatap Muka: odds putus studi 32% lebih rendah |

**Kabar baik:** JASP, jamovi, dan SPSS melakukan dummy coding secara otomatis ketika variabel diidentifikasi sebagai nominal. Pilih kategori referensi yang paling bermakna secara teoritis.

---

## BAGIAN 4: Model dengan Banyak Prediktor (3 slides)

---

### Slide 19: Section Divider

```
BAGIAN 4
Model dengan Banyak Prediktor
```

---

### Slide 20: Adjusted OR — efek prediktor setelah mengontrol variabel lain

**Judul:** Analisis bivariat bisa menyesatkan — always report adjusted OR

**Konten:**

**Masalah:** Dalam analisis bivariat (satu prediktor pada satu waktu), efek yang terlihat bisa dipengaruhi oleh *confounding*.

**Contoh:** Mahasiswa yang tinggal jauh dari pokjar cenderung memiliki keterlibatan akademik yang lebih rendah (karena kesempatan terlibat lebih terbatas). Sehingga efek jarak dan efek keterlibatan saling tumpang tindih.

**Perbandingan unadjusted vs. adjusted OR:**

| Prediktor | Unadjusted OR | Adjusted OR | 95% CI |
|-----------|:-------------:|:-----------:|--------|
| Jarak (per 10 km) | 1.70 | 1.63 | [1.21, 2.19] |
| Keterlibatan akademik | 0.48 | 0.52 | [0.38, 0.71] |
| Usia (per 10 tahun) | 1.15 | 1.08 | [0.88, 1.32] |

Setelah dikontrol, efek jarak sedikit mengecil — sebagian efeknya bekerja *melalui* keterlibatan akademik.

**Aturan:** Dalam artikel ilmiah, selalu laporkan adjusted OR dari model multipel.

---

### Slide 21: Interaksi — apakah efek jarak sama untuk semua mahasiswa?

**Judul:** Efek moderasi dalam regresi logistik: efek prediktor bisa berbeda antar subgrup

**Konten:**

**Pertanyaan riset:** Apakah efek jarak pada putus studi *berbeda* tergantung tingkat keterlibatan akademik?

**Model dengan interaksi:**
$$\text{logit}(P) = \beta_0 + \beta_1(\text{Jarak}) + \beta_2(\text{Keterlibatan}) + \beta_3(\text{Jarak} \times \text{Keterlibatan})$$

**Hasil (ilustrasi):** β₃ = −0.08, p = .03 → Interaksi signifikan!

| Subgrup | Efek jarak (OR per km) | Interpretasi |
|---------|------------------------|--------------|
| Keterlibatan rendah | 1.12 | Jarak sangat berpengaruh |
| Keterlibatan tinggi | 1.02 | Jarak hampir tidak berpengaruh |

**Makna praktis:** Keterlibatan akademik yang tinggi bisa *membuffer* dampak jarak yang jauh. Ini penting untuk merancang intervensi yang tepat sasaran.

**Visual:** Two-line plot: sumbu X = jarak, sumbu Y = P(putus studi), dua garis untuk keterlibatan rendah vs. tinggi.

---

### Slide 22: Strategi membangun model — mulai dari teori

**Judul:** Jangan biarkan data memilih prediktornya sendiri

**Konten:**

**Theory-driven (DIREKOMENDASIKAN):**
1. Pilih prediktor berdasarkan teori dan literatur sebelum melihat data
2. Uji hipotesis yang sudah *pre-specified*
3. Hasil lebih mudah diinterpretasi dan lebih kredibel

**Stepwise selection (KONTROVERSIAL):**
- *Forward*: tambahkan prediktor satu per satu berdasarkan p-value
- *Backward*: mulai dengan semua prediktor, hapus yang tidak signifikan
- **Masalah:** Overfitting, inflasi Type I error, hasil tidak replicable, dan CI tidak valid secara formal

**Praktis:**
- Selalu mulai dari teori
- Analisis eksplorasi boleh untuk *generate* hipotesis — tapi harus dipisahkan dari analisis konfirmatori
- Laporkan *semua* model yang diuji, bukan hanya yang paling bagus

---

## BAGIAN 5: Asumsi dan Diagnostik (5 slides)

---

### Slide 23: Section Divider

```
BAGIAN 5
Asumsi dan Diagnostik
```

---

### Slide 24: Asumsi regresi logistik — lebih longgar dari regresi linear

**Judul:** Kabar baik: regresi logistik tidak membutuhkan normalitas atau homoskedastisitas

**Konten:**

**Yang HARUS dipenuhi:**
1. **Outcome biner** — variabel dependen harus dikotomus (0/1)
2. **Observasi independen** — satu partisipan tidak mempengaruhi partisipan lain
3. **Linearitas dalam log odds** — prediktor kontinu harus punya hubungan linear dengan logit(P)
4. **Tidak ada multikolinearitas ekstrem** — prediktor tidak boleh saling berkorelasi sangat tinggi
5. **Jumlah sampel cukup** — minimal 10 *events* per prediktor (lihat Bagian 8)

**Yang TIDAK perlu:**
- ✗ Normalitas residual
- ✗ Homoskedastisitas (varians error yang sama)
- ✗ Outcome kontinu
- ✗ Hubungan linear antara prediktor dan P (hanya harus linear dalam logit)

**Narasi:** "Lebih robust untuk data riil — tapi asumsi yang ada tetap harus dicek dan dilaporkan."

---

### Slide 25: Linearitas dalam log odds — prediktor kontinu harus linear dalam logit

**Judul:** Prediktor kontinu harus punya hubungan linear dengan logit(P), bukan dengan P

**Konten:**

**Cara memeriksa:**
1. **Box-Tidwell test:** Tambahkan interaksi X × ln(X) ke model. Jika signifikan → hubungan tidak linear.
2. **Inspeksi visual:** Plot logit(P̂) vs. X dan cari pola kurvilinear.

**Contoh pelanggaran yang umum:**
Efek jarak mungkin *plateau* setelah 30 km — mahasiswa yang tinggal 35 km atau 60 km dari pokjar memiliki hambatan yang serupa. Dalam logit, ini akan terlihat sebagai kurva, bukan garis.

**Solusi jika tidak linear:**
- Transformasi prediktor: log(Jarak), √Jarak
- Tambahkan suku kuadratik: Jarak + Jarak²
- Gunakan *splines* untuk fleksibilitas lebih

---

### Slide 26: Multikolinearitas — prediktor yang terlalu mirip satu sama lain

**Judul:** VIF > 10 adalah tanda prediktor tidak bisa diestimasi secara stabil

**Konten:**

**Masalah:** Jika dua prediktor berkorelasi sangat tinggi, koefisien menjadi tidak stabil — *standard error* membengkak dan CI melebar.

**Cara memeriksa: VIF (Variance Inflation Factor)**

| VIF | Interpretasi |
|-----|--------------|
| < 5 | Tidak ada masalah |
| 5 – 10 | Moderate — perlu hati-hati |
| > 10 | Masalah serius |

**Contoh masalah:**
"Durasi studi (semester)" dan "biaya pendidikan kumulatif (Rp)" — keduanya naik bersama, korelasi r = 0.95 → VIF ≈ 18 → masalah serius.

**Solusi:**
- Hapus salah satu prediktor yang redundan (pertahankan yang lebih relevan secara teoritis)
- Gabungkan menjadi variabel komposit
- Gunakan PCA untuk mereduksi dimensi (advanced)

**JASP dan jamovi** menampilkan VIF secara otomatis di output regresi logistik.

---

### Slide 27: Perfect separation — ketika satu prediktor "terlalu baik"

**Judul:** Jika satu prediktor memisahkan outcome secara sempurna, model tidak bisa diestimasi

**Konten:**

**Masalah:** Satu prediktor memisahkan outcome secara sempurna — semua Y = 1 ada di satu sisi, semua Y = 0 di sisi lain.

**Contoh:**
Semua mahasiswa dengan jarak > 45 km putus studi (100%).
Semua mahasiswa dengan jarak ≤ 45 km lanjut studi (100%).

**Akibat:**
- Koefisien meluncur ke ±∞ karena MLE mencoba memaksimalkan kemungkinan yang sudah sempurna
- *Standard error* sangat besar
- Model tidak *converge* — muncul peringatan di output

**Tanda-tanda di output:**
- Koefisien sangat besar (β > 10 atau < −10)
- *Standard error* sangat besar
- Pesan "Algorithm did not converge"

**Solusi:**
- Firth's penalized likelihood (tersedia di R; paket `logistf`)
- Gabungkan kategori yang bermasalah
- Kumpulkan lebih banyak data

---

## BAGIAN 6: Evaluasi Model (6 slides)

---

### Slide 28: Section Divider

```
BAGIAN 6
Evaluasi Model
```

---

### Slide 29: Confusion matrix — dasar evaluasi akurasi prediksi

**Judul:** Confusion matrix membandingkan prediksi model dengan kondisi aktual

**Konten:**

Setelah model difit, gunakan *default threshold* P ≥ 0.50 → prediksi putus studi; P < 0.50 → prediksi lanjut.

|  | Prediksi: Lanjut | Prediksi: Putus Studi |
|--|:-----------------:|:----------------------:|
| **Aktual: Lanjut** | 240 **(TN)** | 30 **(FP)** |
| **Aktual: Putus Studi** | 50 **(FN)** | 130 **(TP)** |

**Definisi:**
- **TP (True Positive):** Prediksi putus studi → aktual putus studi ✓
- **TN (True Negative):** Prediksi lanjut → aktual lanjut ✓
- **FP (False Positive):** Prediksi putus studi → aktual lanjut ✗ *(false alarm)*
- **FN (False Negative):** Prediksi lanjut → aktual putus studi ✗ *(miss — yang paling berbahaya)*

**Narasi:** "FN = mahasiswa berisiko yang tidak terdeteksi. Untuk program intervensi PJJ, ini adalah kesalahan yang paling merugikan."

---

### Slide 30: Accuracy, sensitivity, specificity — pilih sesuai konteks

**Judul:** Tidak ada satu metrik yang cukup — pilih sesuai konsekuensi kesalahan

**Konten:**

Dari confusion matrix (TP=130, TN=240, FP=30, FN=50, N=450):

**Accuracy** = (TP + TN) / N = 370 / 450 = **82.2%**
→ "Berapa persen prediksi yang benar secara keseluruhan?"

**Sensitivity (Recall)** = TP / (TP + FN) = 130 / 180 = **72.2%**
→ "Dari yang benar-benar putus studi, berapa % yang berhasil kita tangkap?"

**Specificity** = TN / (TN + FP) = 240 / 270 = **88.9%**
→ "Dari yang benar-benar lanjut studi, berapa % yang kita prediksi dengan benar?"

**Precision** = TP / (TP + FP) = 130 / 160 = **81.3%**
→ "Dari yang kita prediksi putus studi, berapa % yang benar-benar putus studi?"

---

### Slide 31: Trade-off sensitivity vs. specificity — tidak ada threshold yang "benar"

**Judul:** Menaikkan sensitivity selalu menurunkan specificity — sesuaikan dengan konteks klinis

**Konten:**

**Skenario A: Screening risiko bunuh diri**
False Negative = orang berisiko tidak terdeteksi → berbahaya!
→ Prioritaskan **SENSITIVITY tinggi** — lebih baik over-identify
→ Turunkan threshold: P ≥ 0.30 → prediksi risiko tinggi

**Skenario B: Pemberian label diagnosis klinis**
False Positive = label yang tidak tepat → stigma, biaya, kecemasan
→ Prioritaskan **SPECIFICITY tinggi** — pastikan yang diprediksi positif benar-benar positif
→ Naikkan threshold: P ≥ 0.70 → prediksi positif

**Cara mengatur trade-off:**
*Default threshold* = 0.50. Bisa disesuaikan berdasarkan konteks dan pertimbangan etis — tidak ada angka yang "benar" secara universal.

---

### Slide 32: ROC curve — melihat performa model di semua threshold sekaligus

**Judul:** ROC curve memplot sensitivity vs. (1 − specificity) di setiap nilai threshold

**Konten:**

**ROC (Receiver Operating Characteristic) Curve:**
- Sumbu Y: Sensitivity (True Positive Rate)
- Sumbu X: 1 − Specificity (False Positive Rate)
- Setiap titik di kurva = satu nilai threshold

**Membaca ROC curve:**
- **Garis diagonal** = model acak (*no better than coin flip*)
- **Makin mendekati sudut kiri atas** = model makin baik
- **AUC (Area Under the Curve)** = ringkasan performa dalam satu angka

**Visual:** ROC curve dengan AUC = 0.84 dan garis diagonal sebagai pembanding.

*Catatan: Amelia sudah memiliki deck terpisah tentang ROC ([hackmd.io/@ameliazein/roc](https://hackmd.io/@ameliazein/roc)) — pertimbangkan referensi silang ke sana.*

---

### Slide 33: AUC — ringkasan performa diskriminasi model dalam satu angka

**Judul:** AUC = probabilitas model memberi skor lebih tinggi ke kasus positif dibanding kasus negatif

**Konten:**

**Makna intuitif AUC:**
Ambil satu mahasiswa yang putus studi (Y=1) dan satu yang lanjut (Y=0) secara acak. AUC = probabilitas bahwa model memberikan *predicted probability* yang lebih tinggi kepada yang putus studi.

**Panduan interpretasi:**

| AUC | Interpretasi | Contoh Penggunaan |
|-----|--------------|-------------------|
| 0.50 | Tidak lebih baik dari tebakan | Tidak berguna |
| 0.60 – 0.70 | Lemah | Butuh improvement |
| 0.70 – 0.80 | Cukup | Pakai dengan hati-hati |
| 0.80 – 0.90 | Baik | Layak untuk aplikasi |
| > 0.90 | Sangat baik — atau *overfitting*? | Cek dulu! |

**Contoh dari dataset demo:** AUC = 0.71 → cukup untuk model 3 prediktor; realistis untuk penelitian psikologi dengan data observasional.

---

### Slide 34: Hosmer-Lemeshow test — uji kalibrasi model

**Judul:** AUC tinggi tidak menjamin probabilitas yang diprediksi akurat

**Konten:**

**Perbedaan diskriminasi vs. kalibrasi:**
- **Diskriminasi** (AUC): apakah model bisa membedakan kasus positif dari negatif?
- **Kalibrasi** (H-L test): apakah *predicted probability* mencerminkan frekuensi aktual?

**Hosmer-Lemeshow Test:**
1. Bagi data menjadi 10 *decile* berdasarkan *predicted probability*
2. Bandingkan *observed* vs. *expected counts* di setiap *decile*
3. H₀: Observed = Expected (model terkalibrasi dengan baik)

**Interpretasi:**
- p > 0.05 → Tidak tolak H₀ → Kalibrasi model *acceptable*
- p < 0.05 → Tolak H₀ → Kalibrasi buruk — predicted probability tidak mencerminkan risiko aktual

**Catatan penting:**
- Dengan N besar, tes ini mudah signifikan bahkan jika miskalibasi kecil
- Dengan N kecil, tes tidak cukup sensitif → p > 0.05 belum tentu berarti kalibrasi bagus
- Selalu lengkapi dengan *calibration plot* (observed vs. predicted probability per decile) untuk evaluasi yang lebih informatif (Steyerberg et al., 2010)

---

## BAGIAN 7: Pelaporan dan Interpretasi (4 slides)

---

### Slide 35: Section Divider

```
BAGIAN 7
Pelaporan dan Interpretasi
```

---

### Slide 36: Pelaporan hasil regresi logistik sesuai APA 7th

**Judul:** Laporan yang lengkap menyertakan uji model, OR + CI, metrik klasifikasi, dan fit statistics

**Konten:**

**Contoh paragraf hasil (APA 7th):**

> "A binary logistic regression was conducted to predict study withdrawal among distance education students using distance to the learning center (km), initial academic anxiety, and academic engagement as predictors. The overall model was statistically significant, χ²(3, *N* = 450) = 125.2, *p* < .001, Nagelkerke *R*² = .32. The model correctly classified 82.2% of cases (sensitivity = 72.2%, specificity = 88.9%, AUC = .84). Distance to the learning center significantly predicted withdrawal (*OR* = 1.05, 95% CI [1.02, 1.08], *p* < .001). Academic engagement was also a significant predictor (*OR* = 0.52, 95% CI [0.38, 0.71], *p* < .001), with higher engagement associated with lower odds of withdrawal. Initial academic anxiety did not significantly predict withdrawal (*OR* = 1.02, 95% CI [0.99, 1.05], *p* = .182)."

**Tabel APA-style:**

| Prediktor | *B* | *SE* | Wald χ² | *p* | *OR* | 95% CI |
|-----------|------|------|---------|-----|------|--------|
| Jarak (km) | 0.05 | 0.01 | 12.3 | <.001 | 1.05 | [1.02, 1.08] |
| Keterlibatan akademik | −0.65 | 0.16 | 16.5 | <.001 | 0.52 | [0.38, 0.71] |
| Kecemasan akademik | 0.02 | 0.02 | 1.78 | .182 | 1.02 | [0.99, 1.05] |

*Note.* N = 450. Model χ²(3) = 125.2, p < .001. Nagelkerke R² = .32.

---

### Slide 37: Menerjemahkan OR ke bahasa yang bisa dipahami semua orang

**Judul:** Terjemahkan OR ke kalimat konkrit — jangan serahkan interpretasi ke pembaca

**Konten:**

**Technical:** OR = 1.05 untuk jarak ke pokjar (per 1 km)

**Tiga cara menerjemahkan:**

**Opsi 1: Persentase perubahan odds**
→ "Setiap tambahan 1 km jarak dari pokjar, odds putus studi naik 5%."

**Opsi 2: Interval jarak yang konkrit**
→ "Mahasiswa yang tinggal 10 km lebih jauh punya odds putus studi 1.63 kali lebih tinggi."
(Perhitungan: 1.05^10 = 1.63)

**Opsi 3: Perbandingan probabilitas**
→ "Mahasiswa yang tinggal 5 km dari pokjar memiliki peluang ~20% putus studi; mahasiswa yang tinggal 15 km memiliki peluang ~30%."

**Rekomendasi:**
Kombinasikan opsi teknis (untuk peer review) dengan bahasa sederhana (untuk laporan ke stakeholder atau implikasi kebijakan).

---

### Slide 38: Enam kesalahan umum dalam regresi logistik

**Judul:** Enam kesalahan yang sering muncul dalam artikel psikologi

**Konten:**

**1. Mengacaukan OR dengan Risk Ratio (RR)**
OR ≠ RR, terutama jika prevalensi outcome > 10%. Jangan tulis "X kali lebih *mungkin*" untuk OR — itu bahasa RR. OR harus dikatakan: "X kali lebih tinggi *odds*-nya" (Zhang & Yu, 1998, *JAMA*).

**2. Mengklaim kausalitas**
Regresi logistik adalah korelasional. Kausalitas membutuhkan desain eksperimental atau quasi-eksperimental.

**3. Mengabaikan multikolinearitas**
"Usia" dan "tahun lahir" keduanya dimasukkan sebagai prediktor? Sudah pasti multikolinear.

**4. Tidak memeriksa asumsi**
Terutama linearitas dalam logit dan kemungkinan *perfect separation*.

**5. Hanya melaporkan prediktor yang signifikan**
Laporkan SEMUA prediktor yang dimasukkan ke model — bukan *cherry-pick* yang p < .05.

**6. EPV terlalu rendah**
Dengan hanya 50 *events*, jangan masukkan lebih dari 5 prediktor (EPV = 10). Kurang dari itu → estimasi tidak stabil.

---

### Slide 39: Keterbatasan regresi logistik binomial

**Judul:** Keterbatasan yang perlu diakui dalam laporan penelitian

**Konten:**

1. **Asumsi independensi:** Data yang tersarang (*nested/clustered*) — misalnya mahasiswa dalam satu pokjar — membutuhkan *multilevel logistic regression*

2. **Interpretasi OR menyesatkan jika prevalensi tinggi:** Pada prevalensi > 10%, OR melebih-lebihkan efek dibanding Risk Ratio (Zhang & Yu, 1998). Pertimbangkan Poisson regression dengan *robust SE* untuk mendapatkan RR langsung.

3. **Generalisasi model:** Model yang dilatih pada satu populasi mungkin tidak bekerja dengan baik di populasi lain — *internal validity* ≠ *external validity*

4. **Tidak ada "model terbaik" yang tunggal:** Pilihan prediktor bergantung pada teori dan konteks — bukan hanya pada angka statistik

5. **Outcome biner kehilangan informasi:** Jika outcome sebenarnya kontinu (misalnya waktu hingga dropout), *survival analysis* mungkin lebih tepat

---

## BAGIAN 8: Use Case dalam Penelitian Psikologi (4 slides)

---

### Slide 40: Section Divider

```
BAGIAN 8
Use Case dalam Penelitian Psikologi
```

---

### Slide 41: Use case 1 — Prediksi percobaan bunuh diri di militer

**Judul:** Regresi logistik mendeteksi siapa yang paling berisiko sebelum krisis terjadi

**Konten:**

**Studi:** Army Study to Assess Risk and Resilience in Servicemembers (Army STARRS) — Kessler et al. (2015, *JAMA Psychiatry*)

**N:** ± 38.000 prajurit Angkatan Darat AS

**Outcome:** Percobaan bunuh diri dalam 1 tahun (prevalensi ~2%)

**Prediktor:** Tingkat depresi, ideasi bunuh diri sebelumnya, *hopelessness*, impulsivitas, penggunaan zat, trauma masa kecil (total ~20 variabel)

**Hasil:**
- AUC ≈ 0.77–0.83 (tergantung subpopulasi)
- Prediktor terkuat: ideasi bunuh diri sebelumnya dan depresi berat

**Dampak kebijakan:** Menjadi dasar pengembangan program *screening* mental health sistematis di militer AS — contoh nyata bagaimana regresi logistik berdampak di luar laboratorium.

---

### Slide 42: Use case 2 — Prediksi keberhasilan akademik mahasiswa

**Judul:** IPK semester pertama adalah early warning indicator terkuat

**Konten:**

**Studi:** Richardson, Abraham, & Bond (2012) — Meta-analisis 241 studi, > 200.000 mahasiswa, *Psychological Bulletin*, 138(2), 353–387.

**Catatan metodologi:** Richardson et al. melaporkan ukuran efek sebagai korelasi (r), bukan OR. Tabel berikut adalah konversi aproksimasi untuk ilustrasi.

**Prediktor terkuat keberhasilan akademik (diukur sebagai GPA):**

| Prediktor | r (dari meta-analisis) | OR ≈ | Interpretasi |
|-----------|------------------------|------|--------------|
| Self-efficacy akademik | .30 | ~2.1 | Keyakinan bisa berhasil |
| Motivasi intrinsik | .26 | ~1.8 | Belajar karena ingin tahu |
| Kecemasan ujian | −.20 | ~0.6 | Sifat negatif jika tinggi |
| IPK semester 1 | .37 | ~2.7 | Prediktor terkuat |

**Implikasi praktis:** IPK semester pertama bisa dijadikan *early warning indicator* untuk sistem intervensi berbasis data di universitas.

---

### Slide 43: Use case 3 — Prediksi turnover karyawan

**Judul:** Komitmen organisasi lebih prediktif dibanding gaji

**Konten:**

**Studi:** Griffeth, Hom, & Gaertner (2000) — Meta-analisis, *Journal of Management*, 26(3), 463–488.

**Catatan metodologi:** Griffeth et al. melaporkan ukuran efek sebagai korelasi (r). OR berikut adalah konversi aproksimasi untuk ilustrasi.

**Prediktor turnover sukarela:**

| Prediktor | r (meta-analisis) | Arah efek | Interpretasi |
|-----------|-------------------|-----------|--------------|
| Komitmen organisasi | −.23 | Protektif | Terkuat di meta-analisis |
| Kepuasan kerja | −.17 | Protektif | Lebih penting dari gaji |
| Ketersediaan alternatif pekerjaan | +.16 | Risiko | Pasar kerja terbuka → resign naik |
| Level gaji | −.12 | Protektif | Lebih lemah dari kepuasan |

**Temuan penting:** Kepuasan kerja dan komitmen lebih prediktif dari level gaji — implikasi besar untuk praktik HR.

**ROI analisis:** Biaya pergantian karyawan = 50–200% gaji tahunan. Model prediksi turnover yang akurat memungkinkan intervensi lebih dini → penghematan biaya yang signifikan.

---

## BAGIAN 9: Merencanakan Jumlah Sampel (3 slides)

---

### Slide 44: Section Divider

```
BAGIAN 9
Merencanakan Jumlah Sampel
```

---

### Slide 45: EPV rule — berapa banyak events yang dibutuhkan?

**Judul:** Minimal 10 events per prediktor — tapi prevalensi outcome juga menentukan N total

**Konten:**

**Aturan EPV (Events Per Variable):**
Minimal **10 events per prediktor** di model (Peduzzi et al., 1996, *J Clinical Epidemiology*).

"Events" = kasus pada kategori yang lebih jarang — biasanya Y = 1.

**Contoh:**
- 450 mahasiswa PJJ, 30% putus studi → 135 events
- EPV = 10 → maksimal **13 prediktor**
- EPV = 20 (lebih aman) → maksimal **6 prediktor**

**Mengapa prevalensi penting?**

| Prevalensi outcome | N yang dibutuhkan (EPV = 10, 3 prediktor) |
|--------------------|--------------------------------------------|
| 50% | 60 |
| 20% | 150 |
| 10% | 300 |
| 5% | 600 |

Outcome yang langka membutuhkan N yang jauh lebih besar.

**Catatan:** EPV = 10 adalah *rule of thumb* dari 1996. Pendekatan kontemporer (Riley et al., 2019, *Statistics in Medicine*) menyarankan perencanaan berbasis *anticipated R²* dan *shrinkage* — lebih akurat untuk riset yang mementingkan presisi estimasi.

---

### Slide 46: Menghitung sampel dengan G*Power

**Judul:** G*Power memperhitungkan OR yang diharapkan, baseline probability, dan power

**Konten:**

**Langkah-langkah:**
1. Buka G*Power → pilih **"Logistic Regression"**
2. Pilih **"A priori"** (hitung N yang dibutuhkan)
3. Input parameter:
   - **Odds ratio H1:** perkiraan OR prediktor utama (dari literatur atau penelitian sebelumnya)
   - **Pr(Y=1 | X=1):** baseline probability outcome
   - **α:** 0.05
   - **Power (1−β):** 0.80 (minimal) atau 0.90 (lebih konservatif)
   - **R²_other_X:** proporsi varians prediktor utama yang dijelaskan oleh prediktor lain
4. Klik "Calculate"

**Contoh konkrit:**
Prediksi putus studi mahasiswa PJJ, 3 prediktor, OR prediktor utama = 1.05 (per km), P(putus studi) baseline = 0.20.
→ Output G*Power: **N ≈ 385**
→ Tambahkan 10–20% untuk antisipasi *missing data* → **N target = 430–460**

**Tip:** Ambil OR dari meta-analisis atau studi yang paling mirip dengan topik dan populasi penelitian Anda.

---

## BAGIAN 10: Aplikasi di JASP/jamovi (4 slides)

---

### Slide 47: Section Divider

```
BAGIAN 10
Aplikasi di JASP/jamovi
```

---

### Slide 48: Persiapan data sebelum menjalankan analisis

**Judul:** Pastikan format data sudah benar sebelum menekan "Run"

**Konten:**

**Checklist persiapan:**

☐ **Variabel outcome** sudah dikode 0/1 (bukan "Ya"/"Tidak" sebagai teks)
☐ **Variabel kategorik** sudah diidentifikasi sebagai nominal/ordinal di software
☐ **Missing data** sudah diperiksa — regresi logistik menggunakan *listwise deletion* secara default
☐ **Multikolinearitas awal** dicek dari matriks korelasi antar prediktor
☐ **Outlier** sudah diperiksa (Mahalanobis distance, Cook's D)

**Di JASP:**
- Buka dataset → pastikan tipe variabel benar (Nominal vs. Scale)
- Outcome 0/1 harus di-set sebagai **Nominal**

**Di jamovi:**
- Outcome → "Nominal"
- Prediktor kontinu → "Continuous"
- Prediktor kategorik → "Nominal" (dummy coding otomatis)

---

### Slide 49: Menjalankan regresi logistik binomial di JASP/jamovi

**Judul:** Centang output yang relevan sejak awal — jangan analisis dua kali

**Konten:**

**Di JASP:**
1. **Regression → Logistic Regression**
2. Outcome → **"Dependent Variable"**; Prediktor kontinu → **"Covariates"**; Prediktor kategorik → **"Factors"**
3. Di tab **"Statistics"** centang:
   - ☑ Odds ratios + Confidence intervals (95%)
   - ☑ Classification table
   - ☑ AUC (ROC)
   - ☑ Nagelkerke R²
   - ☑ VIF (multicollinearity diagnostics)

**Di jamovi:**
1. **Analyses → Regression → Logistic Regression**
2. Isi "Dependent Variable" dan "Covariates/Factors"
3. Tab **"Model Fit":** centang R²N, AIC, BIC
4. Tab **"Prediction":** centang Classification table, AUC
5. Tab **"Estimates":** centang Odds Ratio dan CI

---

### Slide 50: Membaca output: tabel koefisien

**Judul:** Fokus pada OR dan CI — bukan hanya β dan p-value

**Konten:**

**Contoh output JASP (studi putus studi PJJ):**

| Prediktor | β | SE | Wald χ² | p | OR | 95% CI |
|-----------|---|----|---------|---|----|--------|
| Konstanta | −1.84 | 0.31 | 35.1 | <.001 | — | — |
| Jarak_pokjar_km | 0.049 | 0.014 | 12.3 | <.001 | 1.05 | [1.02, 1.08] |
| Keterlibatan_Akademik | −0.650 | 0.160 | 16.5 | <.001 | 0.52 | [0.38, 0.71] |
| Kecemasan_Akademik | 0.020 | 0.015 | 1.78 | .182 | 1.02 | [0.99, 1.05] |

**Cara membaca secara sistematis:**
1. Cek **p-value**: signifikan?
2. Baca **OR**: arah efek — naik atau turun?
3. Cek **95% CI**: melewati 1.0? Jika ya → tidak signifikan
4. Interpretasikan **dalam konteks penelitian** — angka tanpa narasi tidak bermakna

**Jangan lupa:** Prediktor kategorik menghasilkan beberapa baris (satu per kategori, kecuali referensi).

---

### Slide 51: Membaca output: evaluasi model secara menyeluruh

**Judul:** Evaluasi model harus holistik — tidak ada satu angka yang cukup

**Konten:**

**Checklist evaluasi model:**

**1. Omnibus test — apakah model signifikan secara keseluruhan?**
χ²(3) = 125.2, p < .001 ✓

**2. Nagelkerke R² — seberapa baik fit?**
R² = 0.32 → Cukup (acceptable)

**3. Classification accuracy:**
- Overall accuracy: 82.2% ✓
- Sensitivity: 72.2% (tangkap 72% yang putus studi)
- Specificity: 88.9% (identifikasi 89% yang lanjut studi)

**4. AUC:**
AUC = 0.84 → Baik *(angka pedagogis; dataset demo menghasilkan AUC = 0.71 — lebih realistis)*

**5. VIF — multikolinearitas:**
Semua VIF < 3 → Tidak ada masalah ✓

**Narasi:** "Tidak ada satu angka yang cukup. Model yang baik harus lolos dari semua pemeriksaan ini — fit, diskriminasi, kalibrasi, dan asumsi."

---

## CLOSING (3 slides)

---

### Slide 52: Take-home messages

**Judul:** Yang perlu dibawa pulang dari pertemuan hari ini

**Konten:**

✓ **Regresi logistik** adalah metode utama untuk outcome biner — lebih valid dari OLS untuk data seperti ini

✓ **Odds Ratio (OR)** adalah ukuran efek utama — OR > 1 (odds naik), OR < 1 (odds turun); selalu sertakan 95% CI

✓ **OR ≠ Risk Ratio** — jangan tulis "X kali lebih mungkin" untuk OR, terutama jika prevalensi > 10%

✓ **Evaluasi model bersifat multi-faceted** — AUC untuk diskriminasi, Nagelkerke R² untuk fit, confusion matrix untuk akurasi klasifikasi, H-L test untuk kalibrasi

✓ **Asumsi lebih sedikit dari regresi linear**, tapi wajib dicek: linearitas dalam logit, tidak ada multikolinearitas ekstrem, tidak ada *perfect separation*

✓ **Sample size harus direncanakan** — minimal 10 *events per predictor* (EPV rule); gunakan G*Power

✓ **Pelaporan harus lengkap** — OR + CI + uji model + metrik klasifikasi, sesuai APA 7th

✓ **Aplikasi luas di psikologi** — klinis, pendidikan, industri-organisasi, perkembangan

---

### Slide 53: Dataset demo — praktikum hari ini

**Judul:** Dataset demo: putus studi mahasiswa PJJ (N = 450)

**Konten:**

**File:** `Demo_DropoutMahasiswa.csv` (tersedia di folder Praktikum/)

**Variabel:**
- `putus_studi`: outcome (0 = lanjut, 1 = putus studi sebelum semester ke-5)
- `usia`: 18–65 tahun
- `jenis_kelamin`: 0 = Laki-laki, 1 = Perempuan
- `jalur_registrasi`: 1 = Tatap Muka Terbatas, 2 = Daring, 3 = Mandiri
- `kecemasan_akademik`: skor kecemasan awal (0–63)
- `jarak_pokjar_km`: 0.5–50 km
- `keterlibatan_akademik`: skor keterlibatan (1–7)

**Hasil yang diharapkan (realistis, bukan angka pedagogis):**
- Jarak: OR ≈ 1.05 per km, p < .001 ✓ signifikan
- Keterlibatan akademik: OR ≈ 0.54, p < .001 ✓ signifikan (protektif)
- Kecemasan akademik: OR ≈ 1.00, p = ns ✓ tidak signifikan
- Nagelkerke R² ≈ 0.19; AUC ≈ 0.71; Accuracy ≈ 74%
- Sensitivity (threshold 0.50) ≈ 35% — **diskusikan mengapa rendah dan apa artinya untuk interpretasi**

*Catatan: Angka di slide kuliah (Bagian 1–7) menggunakan skenario yang dioptimasi secara pedagogis. Dataset ini memberikan hasil yang lebih realistis — justru lebih mendidik karena menunjukkan bahwa model 3-prediktor biasanya tidak langsung mencapai AUC = 0.84.*

---

### Slide 54: Referensi

**Judul:** Referensi

**Konten:**

**Textbooks:**
- Hosmer, D. W., Lemeshow, S., & Sturdivant, R. X. (2013). *Applied Logistic Regression* (3rd ed.). Wiley.
- Menard, S. (2010). *Logistic Regression: From Introductory to Advanced Concepts and Applications*. Sage.

**Studi yang dikutip:**
- Bruce, S. E., Yonkers, K. A., Otto, M. W., et al. (2005). Influence of psychiatric comorbidity on recovery and recurrence in generalized anxiety disorder, social phobia, and panic disorder. *American Journal of Psychiatry*, *162*(6), 1179–1187.
- Griffeth, R. W., Hom, P. W., & Gaertner, S. (2000). A meta-analysis of antecedents and correlates of employee turnover. *Journal of Management*, *26*(3), 463–488.
- Kessler, R. C., et al. (2015). Predicting suicides after psychiatric hospitalization in US Army soldiers: The Army Study to Assess Risk and Resilience in Servicemembers (Army STARRS). *JAMA Psychiatry*, *72*(1), 49–57.
- Park, J.-H., & Choi, H. J. (2009). Factors influencing adult learners' decision to drop out or persist in online learning. *Educational Technology & Society*, *12*(4), 206–217.
- Peduzzi, P., Concato, J., Kemper, E., Holford, T. R., & Feinstein, A. R. (1996). A simulation study of the number of events per variable in logistic regression analysis. *Journal of Clinical Epidemiology*, *49*(12), 1373–1379.
- Richardson, M., Abraham, C., & Bond, R. (2012). Psychological correlates of university students' academic performance: A systematic review and meta-analysis. *Psychological Bulletin*, *138*(2), 353–387.
- Riley, R. D., et al. (2019). Calculating the sample size required for developing a clinical prediction model. *Statistics in Medicine*, *38*(7), 1276–1296.
- Steyerberg, E. W., et al. (2010). Assessing the performance of prediction models. *Epidemiology*, *21*(1), 128–138.
- Tinto, V. (1987). *Leaving College: Rethinking the Causes and Cures of Student Attrition*. University of Chicago Press.
- Zhang, J., & Yu, K. F. (1998). What's the relative risk? A method of correcting the odds ratio in cohort studies of common outcomes. *JAMA*, *280*(19), 1690–1691.

**Tutorial metodologi:**
- Peng, C.-Y. J., Lee, K. L., & Ingersoll, G. M. (2002). An introduction to logistic regression analysis and reporting. *The Journal of Educational Research*, *96*(1), 3–14.
- Sperandei, S. (2014). Understanding logistic regression analysis. *Biochemia Medica*, *24*(1), 12–18.

---

**Versi:** 1.0
**Dibuat:** 2026-03-25
**Penulis:** Dr. Rizqy Amelia Zein, M.Sc. (dengan Claude Code)
**Sumber:** Gabungan dari `Pertemuan09-10_RegresiLogistik_REVISED.md` (v3.2) dan `Regresi Logistik untuk Statistik Psikologi S2(1).md`; akurasi referensi dicek ulang
