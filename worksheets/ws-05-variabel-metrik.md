# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: ____________________

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|          | IV   |        |        |       |        |               |             |
|          | DV   |        |        |       |        |               |             |
|          | CV   |        |        |       |        |               |             |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [ ] Setiap langkah terdokumentasi
  [ ] Tidak ada "lompatan logis"
  [ ] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah manajemen proses dan struktur memori Linux Ubuntu 22.04 LTS menghasilkan performa website sistem informasi akademik yang lebih efisien berdasarkan response time, penggunaan CPU/memori, dan GTmetrix performance score?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
|Manajemen proses Linux | IV | Efisiensi sistem operasi | CPU utilization, load average | Ratio | %, angka |
|Struktur memori Linux | IV |Pengelolaan memori |Memory usage, cache usage |Ratio |GB, KB |
|Performa website | DV |Kinerja website akademik |Response time, GTmetrix score, LCP |Ratio |Detik, % |
|Lingkungan pengujian|CV|Stabilitas eksperimen|RAM, CPU core, bandwidth|Ratio|GB, Core, Mbps|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [tidak ] Tidak
> Jika ya, di mana? Tidak ada karena semua konsep abstrak telah diterjemahkan menjadi metrik yang dapat diukur secara langsung.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5|Response time dan GTmetrix score secara langsung merepresentasikan performa website |
| Sensitive |4 | Perubahan kecil pada server dan jaringan dapat memengaruhi nilai metrik|
| Feasible |5 |Data mudah dikumpulkan menggunakan tools standar Linux dan GTmetrix |

**Apakah perlu secondary metric?** [ya ] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Largest Contentful Paint (LCP) dan CPU utilization digunakan sebagai secondary metric karena membantu menjelaskan penyebab perubahan performa website secara lebih detail.

**Contoh kasus ceiling effect untuk metrik ini:**
> ika semua website memiliki GTmetrix score sangat tinggi (misalnya 98–100%), maka metrik menjadi kurang sensitif untuk membedakan performa antar sistem.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? | Ada kemungkinan data hilang saat jaringan tidak stabil|Melakukan pengujian berulang minimal 3 kali |
| Consistency | Apakah ada kontradiksi internal?| Bisa terjadi perbedaan hasil antar tools|Menggunakan tools yang sama pada setiap pengujian |
| Validity | Apakah benar-benar mengukur yang dimaksud? | Ya, metrik langsung mengukur performa sistem|Menggunakan metrik standar industri seperti GTmetrix |
| Representativeness | Apakah sampel mewakili populasi target? |Masih terbatas pada satu website akademik |Menambah variasi website akademik pada penelitian lanjutan |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat memilih metrik yang paling menguntungkan hasil penelitian sehingga meningkatkan risiko bias dan kesimpulan yang tidak valid.

> Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan untuk menemukan pola tambahan setelah analisis utama selesai. Hasil eksplorasi tetap dilaporkan sebagai exploratory findings, bukan sebagai bukti utama untuk menerima atau menolak hipotesis.
