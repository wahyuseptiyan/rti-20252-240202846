# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : ____________________

Research Question:
  Tipe         : [ ] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : ____________________
  Variabel IV  : ____________________
  Variabel DV  : ____________________
  Metrik       : ____________________
  Dataset      : ____________________
  Baseline     : ____________________

Quality Check RQ:
  [ ] Variabel spesifik
  [ ] Metrik jelas
  [ ] Baseline ada
  [ ] Konteks disebutkan
  [ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : ____________________
  Jenis kontribusi        : [ ] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          : ____________________

Hypothesis Pair:
  H₀ : ____________________
  H₁ : ____________________
  Threshold              : ____________________
  Justifikasi threshold  : ____________________
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Sebagian besar penelitian performa website akademik hanya menggunakan pengujian eksternal seperti GTmetrix tanpa menganalisis hubungan manajemen proses dan struktur memori pada sistem operasi Linux terhadap performa website.

**RQ versi pertama (tulis bebas):**
> Bagaimana pengaruh manajemen proses dan struktur memori Linux terhadap performa sistem informasi akademik berbasis web?
**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | ya |Monitoring menggunakan htop, vmstat, curl, dan GTmetrix |
| Metrik terukur | ya |Load average, penggunaan memori, response time, performance score |
| Baseline | ya |GTmetrix dan monitoring Linux standar |
| Dataset/konteks | ya |Website sistem informasi akademik berbasis Linux Ubuntu 22.04 |

**Tipe RQ:** [ya ] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah manajemen proses dan struktur memori pada Linux Ubuntu 22.04 LTS menghasilkan performa website sistem informasi akademik yang lebih efisien berdasarkan metrik response time, penggunaan CPU/memori, dan GTmetrix performance score?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ |Tidak ada pengaruh signifikan manajemen proses dan struktur memori Linux Ubuntu 22.04 terhadap performa sistem informasi akademik berbasis web berdasarkan response time, penggunaan CPU/memori, dan GTmetrix score|
| H₁ |Terdapat pengaruh signifikan manajemen proses dan struktur memori Linux Ubuntu 22.04 terhadap performa sistem informasi akademik berbasis web berdasarkan response time, penggunaan CPU/memori, dan GTmetrix score |
| Metrik |Response time, CPU utilization, memory usage, GTmetrix performance score |
| Threshold |p-value < 0.05 |
| Justifikasi threshold | Nilai 0.05 umum digunakan dalam penelitian kuantitatif untuk menentukan signifikansi statistik|

**Apakah hipotesis ini falsifiable?** [ya ] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? 
Dengan melakukan pengujian performa dan analisis statistik. Jika hasil pengujian menunjukkan tidak ada perbedaan atau pengaruh signifikan pada metrik performa (p-value ≥ 0.05), maka H₁ ditolak dan H₀ diterima.
---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah manajemen proses dan struktur memori Linux Ubuntu 22.04 LTS menghasilkan performa website sistem informasi akademik yang lebih efisien berdasarkan response time, penggunaan CPU/memori, dan GTmetrix performance score? |
| Variable (IV) | Manajemen proses dan struktur memori Linux |
| Variable (DV) |Performa website sistem informasi akademik |
| Metric |CPU utilization, memory usage, response time, GTmetrix score |
| Data source |Pengujian website akademik menggunakan htop, vmstat, curl, dan GTmetrix |
| Analysis method |Analisis kuantitatif dan perbandingan hasil performa |

**Apakah rantai lengkap?** [ya ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi?Tidak perlu revisi karena semua komponen sudah saling terhubung.

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Analisis Performa Sistem Informasi Akademik: Pengaruh Struktur Memori dan Manajemen Proses pada Sistem Operasi Linux Menggunakan Metode Eksperimental Kuantitatif
**RQ yang diekstrak:** Apakah struktur memori dan manajemen proses Linux berpengaruh terhadap performa sistem informasi akademik berbasis web?
**Komponen yang hilang:** RQ belum menyebutkan baseline secara eksplisit dan belum mencantumkan threshold atau ukuran keberhasilan performa secara spesifik.
