# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |          |      |           |        |       |             |
| 2     |          |      |           |        |       |             |
| 3     |          |      |           |        |       |             |
| ...   |          |      |           |        |       |             |

Jumlah runs per skenario : ____
Total runs               : ____

DATA LOG (per run):
  Run ID    : ____________________
  Timestamp : ____________________
  Skenario  : ____________________
  Input     : ____________________
  Output    : ____________________
  Anomali   : ____________________
  Catatan   : ____________________
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Cek kecepatan respon web SIAKAD | Gak pakai (Locked) | URL Login, jeda tiap 2 menit | Beres dijalankan |
| 2 | Cek kecepatan respon web SIAKAD | Gak pakai (Locked) | URL Login, jeda tiap 2 menit | Beres dijalankan |
| 3 | Cek kecepatan respon web SIAKAD | Gak pakai (Locked) | URL Login, jeda tiap 2 menit | Beres dijalankan |
| 4 | Cek kecepatan respon web SIAKAD | Gak pakai (Locked) | URL Login, jeda tiap 2 menit | Beres dijalankan |
| 5 | Cek kecepatan respon web SIAKAD | Gak pakai (Locked) | URL Login, jeda tiap 2 menit | Beres dijalankan |

**Total skenario:** 1 skenario pengujian utama buat cari performa awal (baseline).
**Run per skenario:** Diulang 5 kali run biar adil.
**Total run keseluruhan:** 5 kali uji coba.

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | Mulai dari `run-001` sampai `run-005` |
| Timestamp | `2026-06-23T23:00:00Z` (Waktu pas ngetik di terminal) |
| Operator | Wahyu Septiyan |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | Dikunci (Nggak pakai pengacakan) |
| Code version | Alamat web target: https://siakad.target-kampus.ac.id |
| Target OS | Linux Ubuntu 22.04 LTS yang jalan di VirtualBox |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Waktu Respon (`curl`) | float (angka desimal) | 0.00 – 10.00 detik |
| Skor Performa GTmetrix | integer (angka bulat) | 0 – 100% |
| Beban CPU (`htop`) | float (angka persen) | 0.0 – 100.0% |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Koneksi internet tiba-tiba putus pas perintah `curl` lagi jalan | Ubah status run jadi *Failed*, cek dulu Wi-Fi laptop Lenovo-nya, lalu bikin Run ID baru buat tes ulang tanpa menghapus data yang gagal. |
| Hasil ekstrem | Angka response time tiba-tiba melonjak sampai `15.0 detik` | Cek apakah Windows di laptop lagi diam-diam update atau server SIAKAD-nya yang emang lagi down. Tandai datanya sebagai *Outlier* (jangan dihapus) biar tetap jujur. |
| Waktu eksekusi anomali | Jeda pengujian meleset jadi 15 menit gara-gara ditinggal bikin kopi | Biarkan data tetap masuk ke log pengujian, tapi kasih keterangan tambahan *Protoplan Delay* biar ketahuan kenapa jedanya kelamaan. |
| Inkonsistensi dengan run lain | Skor performa di GTmetrix mendadak drop jauh di run ke-4 dan ke-5 | Cek apakah laptop mulai panas (*thermal throttling*) yang bikin performa CPU AMD Ryzen-nya turun. Catat kondisi suhunya, dan jadikan itu bahan analisis tambahan. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Jujur, kalau pas ngerjain tugas kuliah atau praktikum biasa, saya sering banget cuma ngetes program sekali (*single run*) saja. Begitu programnya jalan dan keluar angkanya, ya sudah langsung saya ambil dan kumpulin ke dosen. Risikonya baru terasa sekarang, datanya bisa jadi bias banget. Kalau pas kebetulan pas diklik internetnya lagi lemot, nanti kesimpulannya jadi ikutan salah, padahal aslinya sistemnya nggak sejelek itu.

**Yang akan dilakukan berbeda:**
> Ke depannya, saya bakal pakai cara *multiple runs* (diulang minimal 5 kali) kayak di tugas ini. Selain itu, semua kondisi lingkungan laptop dan server juga wajib dicatat di log data yang rapi. Dengan cara diulang-ulang begini, kita bisa tahu nilai rata-rata yang sebenarnya dan kelihatan juga internetnya lagi stabil atau naik-turun. Hasil risetnya pun jadi lebih kuat, meyakinkan, dan nggak bisa didebat sama dosen.
