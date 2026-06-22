# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [ ] Semua skenario tercakup
  [ ] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: ____ dari ____ data points

Format Consistency:
  [ ] Semua file format sama (CSV/JSON/...)
  [ ] Header konsisten
  [ ] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [ ] Nilai dalam range masuk akal
  [ ] Tidak ada waktu negatif
  [ ] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: ____________________

Cross-Validation:
  [ ] Run identik → hasil mendekati
  [ ] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Uji Response Time Web SIAKAD | 5 | 5 | 0 | Aman, semua data terekam lengkap |

**Total expected:** 5 | **Total actual:** 5 | **Missing:** 0

**Keputusan untuk data missing:**
> Karena datanya sudah masuk semua 100% alias tidak ada yang hilang atau nge-crash di jalan, kita bisa langsung gas lanjut ke tahap pemeriksaan anomali data.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (Data Fiktif Response Time):**

| Run | Response Time (Detik) |
|-----|-------------|
| 1   | 2.15        |
| 2   | 2.20        |
| 3   | 2.12        |
| 4   | 2.18        |
| 5   | 2.14        |

**Deteksi outlier (diurutkan dari kecil ke gede: 2.12, 2.14, 2.15, 2.18, 2.20):**
- Q1 (Kuartil Bawah) = 2.135 | Q3 (Kuartil Atas) = 2.19 | IQR = 0.055
- Batas bawah (Q1 - 1.5 × IQR) = 2.0525
- Batas atas (Q3 + 1.5 × IQR) = 2.2725
- Outlier terdeteksi: Gak ada (Semua data fiktif kita berada di dalam batas aman)

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| - | - | Gak ada data yang aneh atau lompat kejauhan | Data fiktif ini bersih dan bisa lanjut dipakai |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data berhasil terkumpul tanpa ada yang kurang.
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Gak ditemukan anomali sama sekali, semua angka response time masuk akal di rentang 2.12 - 2.20 detik.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

**Jawaban Saya:**
> Bedanya begini: "data yang benar" itu asal angkanya keluar otomatis dari komputer, ya kita anggap benar karena bersumber dari sistem. Tapi belum tentu data itu bisa "dipercaya" untuk riset. Bisa saja komputer kita lagi nge-bug, atau internet pas run ke-4 tiba-tiba drop tanpa kita sadari. 

> Makanya, validasi formal (seperti cek kelengkapan dan rumus IQR) itu wajib banget dilakukan. Biarpun semua data tercatat otomatis, kita harus tetap menyaringnya secara manual. Tujuannya agar kita yakin kalau data fiktif maupun data asli yang kita pegang ini emang sehat, jujur, terbebas dari error sistem, dan layak buat dipresentasikan ke dosen tanpa bikin malu.
