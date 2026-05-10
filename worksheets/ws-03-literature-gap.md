# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : ____________________
Database   : ____________________
Query      : ____________________
Tahun      : ____________________
Hasil awal : ____ paper → Screening → ____ paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|       |       |        |      |        |            |

Pola yang ditemukan:
  Metode dominan     : ____________________
  Dataset umum       : ____________________
  Limitasi berulang  : ____________________

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : ____________________
  Bukti        : ____________________
  Signifikansi : ____________________

Gap 2: [Jenis: ____]
  Deskripsi    : ____________________
  Bukti        : ____________________
  Signifikansi : ____________________

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|          |           |               |        |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Analisis performa sistem informasi akademik berbasis web pada sistem operasi Linux
**Query pencarian:** ("website performance" OR "web performance") AND ("academic information system" OR "sistem informasi akademik") AND (Linux OR Ubuntu) AND (GTmetrix OR "PageSpeed Insights")
**Database:** Google Scholar, IEEE Xplore, Scopus

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|1|Ramadhan & Rachmatika|2025|Eksperimen kuantitatif menggunakan htop, vmstat, curl, GTmetrix|Website unpam.ac.id|Linux stabil dengan 129 proses aktif, GTmetrix score 56% grade D|Hanya menggunakan satu website akademik|
|2|Arni et al.|2023|Analisis performa menggunakan GTmetrix|  Website organisasi|Performa website memperoleh grade E dengan performa 54%|Tidak menganalisis pengaruh sistem operasi|
|3|Muriyatmoko & Musthafa|2022|Speed testing model|Website jurnal Indonesia|Performa rata-rata website pendidikan 60–70%|Fokus hanya pada performa eksternal|
|4|Tengriano et al.|2022|GTmetrix dan PageSpeed Insights|Website AyoMulai|Grade B dengan performa 77%|Tidak membahas manajemen memori dan CPU|
|5|Yunianto & Adhiyarta|2021|Perbandingan performa OS|Linux vs Windows|Linux lebih efisien dalam penggunaan memori|Tidak fokus pada sistem informasi akademik|

**Pola yang terlihat — Metode dominan:** ___________________
**Limitasi yang berulang:** ______________________________

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [ ] Ya / [ ] Tidak | *Contoh: Akurasi turun di bawah 80% untuk kelas minoritas* |
| Method Gap | [ ] Ya / [ ] Tidak | |
| Data Gap | [ ] Ya / [ ] Tidak | |
| Context Gap | [ ] Ya / [ ] Tidak | |

**Gap utama yang dipilih:** _____________________________
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> ___________________________________________________

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | *Contoh: RF + TF-IDF* | *Task sama: klasifikasi teks* | *Dipakai 6 dari 10 paper* | *Bukan, tapi common practice* | *Lee et al., 2022* |
| 2 | | | | | |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ] Tidak
> Justifikasi: ________________________________________

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> ___________________________________________________
> ___________________________________________________
