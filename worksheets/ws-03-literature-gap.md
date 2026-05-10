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

**Pola yang terlihat — Metode dominan:** 
Pengujian performa website menggunakan GTmetrix dan monitoring resource Linux.
**Limitasi yang berulang:** Sebagian besar penelitian hanya fokus pada performa eksternal website dan belum menghubungkan performa dengan manajemen memori serta proses sistem operasi Linux.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [Ya ] Ya / [ ] Tidak | Banyak website akademik masih memiliki skor performa rendah (grade D/E) dan waktu loading tinggi|
| Method Gap | [Ya ] Ya / [ ] Tidak |Sebagian penelitian hanya menggunakan GTmetrix tanpa analisis internal sistem operasi Linux |
| Data Gap | [Ya ] Ya / [ ] Tidak |Dataset penelitian terbatas pada satu website dan sedikit variasi lingkungan sistem |
| Context Gap | [ Ya] Ya / [ ] Tidak |Belum banyak penelitian pada sistem informasi akademik berbasis Linux di lingkungan perguruan tinggi Indonesia |

**Gap utama yang dipilih:** Method Gap dan Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena performa website tidak hanya dipengaruhi oleh tampilan front-end, tetapi juga oleh manajemen proses dan memori pada sistem operasi Linux. Sebagian besar penelitian sebelumnya hanya mengukur performa dari sisi eksternal tanpa melihat hubungan langsung dengan resource sistem operasi, sehingga analisis performa belum menyeluruh.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | GTmetrix Performance Testing | Sama-sama mengukur performa website | Banyak digunakan dalam penelitian website | Bukan SOTA penuh, tetapi common practice | Arni et al., 2023 |
| 2 |GTmetrix + PageSpeed Insights |Sama-sama mengevaluasi kecepatan dan efisiensi web |Digunakan luas untuk analisis web modern |Ya, termasuk tools populer terbaru |Tengriano et al., 2022 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [Tidak] Tidak
> Justifikasi: Karena baseline yang dipilih merupakan tools yang umum digunakan dalam penelitian performa website dan relevan dengan topik penelitian. Baseline tidak dipilih secara sengaja untuk terlihat lemah, melainkan representatif terhadap praktik umum pada penelitian sebelumnya.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Pernyataan “belum ada yang meneliti ini” hanya merupakan klaim umum tanpa bukti pencarian literatur yang jelas. Sedangkan research gap yang valid harus didukung oleh hasil analisis dari beberapa penelitian sebelumnya sehingga terlihat kekurangan, keterbatasan, atau masalah yang belum terjawab.

Cara membuktikan adanya gap adalah dengan melakukan systematic literature search menggunakan database seperti Google Scholar, IEEE Xplore, atau Scopus, kemudian membandingkan metode, hasil, dan limitasi dari penelitian terdahulu. Dari sana dapat ditemukan pola kekurangan, kontradiksi, atau konteks yang belum diteliti secara mendalam.
