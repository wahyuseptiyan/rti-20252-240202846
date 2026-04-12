# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : ____________________
Tanggal          : ____________________

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: ____________________
   - Data yang dibutuhkan untuk verifikasi: ____________________

2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan: ____________________

3. Identifikasi distorsi:
   - Asumsi tersembunyi: ____________________
   - Sumber bias potensial: ____________________
   - Langkah mitigasi: ____________________

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: ____________________
   - Batasan yang diakui sejak awal: ____________________
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Analisis Performa Sistem Informasi Akademik: Pengaruh Struktur Memori dan Manajemen Proses pada Sistem Operasi Linux Menggunakan Metode Eksperimental Kuantitatif
> Penulis (Tahun): Muhammad Rafli Ramadhan, Rinna Rachmatika (2025)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengakses website sistem informasi akademik unpam.ac.id pada Linux Ubuntu 22.04 dan mengumpulkan data performa menggunakan tools htop, vmstat, curl, dan GTmetrix | Pengujian hanya dilakukan pada kondisi jaringan tertentu sehingga hasil mungkin tidak mewakili semua kondisi akses |
| Data → Processing | Data dari pengujian seperti jumlah proses aktif, penggunaan memori, CPU usage, dan waktu respon dikumpulkan lalu dihitung rata-rata dari tiga kali pengujian| Pengulangan pengujian hanya 3 kali, sehingga kemungkinan variasi performa belum sepenuhnya terwakili |
| Processing → Analysis | Data yang sudah dirata-ratakan dianalisis untuk melihat kinerja CPU, manajemen memori, waktu akses website, dan performa sistem secara keseluruhan | Analisis hanya fokus pada sistem operasi Linux, tanpa perbandingan langsung dengan sistem operasi lain |
| Analysis → Inference | Peneliti menyimpulkan bahwa Linux mampu mengelola proses dan memori secara efisien, tetapi performa website masih kurang optimal | Kesimpulan bisa dipengaruhi oleh kondisi server website atau jaringan saat pengujian |
| Inference → Knowledge | Hasil penelitian dijadikan referensi untuk meningkatkan performa sistem informasi akademik, seperti menggunakan CDN, kompresi file, dan HTTP/2 | Rekomendasi mungkin tidak berlaku untuk semua website karena konfigurasi sistem yang berbeda |

**Distorsi paling besar di tahap:** **Data → Processing**

Karena jumlah pengujian hanya tiga kali, sehingga kemungkinan variasi performa sistem belum sepenuhnya terwakili.

**Dua distorsi spesifik yang teridentifikasi:**
1. Jumlah pengujian terbatas (3 kali) sehingga data mungkin belum cukup merepresentasikan kondisi sebenarnya.
2. Pengujian dilakukan pada satu sistem operasi (Linux Ubuntu) tanpa perbandingan langsung dengan sistem operasi lain seperti Windows atau macOS.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | *Contoh: Laporkan kedua versi (dengan dan tanpa outlier)* |
| Transparansi | |
| Peer review | |

**Keputusan akhir dan justifikasi:**
> ___________________________________________________

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** ________________________________________

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | *Contoh: 4* | *Contoh: 2* | *Contoh: 5* |
| Jenis data yang dikumpulkan | | | |
| Limitasi paradigma | | | |

**Paradigma yang dipilih:** _____________________________
**Alasan:** ____________________________________________

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> ___________________________________________________
> ___________________________________________________
