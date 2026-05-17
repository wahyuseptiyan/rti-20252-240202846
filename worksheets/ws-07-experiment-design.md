# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : ____________________
Hypothesis        : ____________________
Tipe Eksperimen   : [ ] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |           |          |             |
| Treatment |         |          |             |

Fairness Checklist:
  [ ] Dataset identik untuk semua kondisi
  [ ] Preprocessing setara
  [ ] Tuning effort setara
  [ ] Environment identik
  [ ] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |                 |          |
| External    |                 |          |
| Construct   |                 |          |
| Conclusion  |                 |          |

Statistical Plan:
  Uji statistik   : ____________________
  Justifikasi      : ____________________
  Alpha            : ____________________
  Effect size min  : ____________________
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah manajemen proses dan struktur memori Linux Ubuntu 22.04 LTS menghasilkan performa website sistem informasi akademik yang lebih efisien berdasarkan response time, penggunaan CPU/memori, dan GTmetrix performance score?
**Tipe eksperimen:** [ya] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Pengujian website tanpa optimasi monitoring detail |Monitoring dasar sistem Linux| Ubuntu 22.04, RAM 4GB, CPU dual-core, koneksi internet tetap|
| Treatment |Pengujian website dengan monitoring proses dan memori lengkap menggunakan htop, vmstat, curl, dan GTmetrix |Monitoring proses + struktur memori Linux |Ubuntu 22.04, RAM 4GB, CPU dual-core, koneksi internet tetap |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ | Menggunakan website akademik yang sama|
| Preprocessing setara |✅ |Tidak ada perubahan data atau konfigurasi website |
| Tuning effort setara | ✅| Semua pengujian menggunakan konfigurasi Linux yang sama|
| Environment identik | ✅|Hardware, OS, dan jaringan dibuat sama |
| Metrik evaluasi sama | ✅|Semua kondisi menggunakan response time, CPU usage, memory usage, dan GTmetrix score |

**Ada yang tidak fair?** [ ] Ya / [ tidak] Tidak
> Jika ya, bagaimana cara memperbaikinya? Tidak perlu perbaikan karena seluruh kondisi eksperimen sudah dijaga tetap identik.

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Aktivitas proses background Linux dapat memengaruhi hasil performa | Menutup aplikasi yang tidak diperlukan selama pengujian |
| External | Hasil eksperimen hanya menggunakan satu website akademik| Menambah objek website lain pada penelitian lanjutan|
| Construct |GTmetrix score mungkin tidak sepenuhnya merepresentasikan pengalaman pengguna |Menggunakan metrik tambahan seperti response time dan LCP |
| Conclusion |Jumlah pengujian terlalu sedikit dapat menghasilkan kesimpulan yang lemah | Melakukan pengujian berulang minimal 3 kali|

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
Karena hasil penelitian hanya menggunakan satu sistem informasi akademik sehingga generalisasi hasil ke website lain masih terbatas.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
Jika sebuah paper mengklaim “metode kami mengalahkan semua baseline”, maka tiga pertanyaan pertama yang harus diajukan adalah:

1. Apakah semua baseline diuji dengan kondisi yang benar-benar sama?
- Dataset, environment, preprocessing, dan metrik harus identik.
2. Apakah baseline yang dipilih representatif dan relevan?
- Jangan sampai menggunakan baseline lama atau lemah hanya agar metode baru terlihat lebih baik.
3. Apakah hasil perbedaannya signifikan secara statistik?
- Harus ada bukti statistik seperti p-value atau effect size, bukan hanya selisih angka kecil.
