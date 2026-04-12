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
| Kejujuran ilmiah | Peneliti harus melaporkan hasil penelitian secara jujur dengan menampilkan dua versi analisis, yaitu data dengan outlier dan tanpa outlier, serta menjelaskan alasan penghapusan data tersebut. |
| Transparansi | Peneliti harus menjelaskan secara terbuka metode pengolahan data, termasuk alasan mengapa data outlier dianggap tidak representatif atau perlu dihapus. |
| Peer review | Proses peer review memungkinkan peneliti lain mengevaluasi apakah penghapusan outlier valid secara metodologis atau justru merupakan manipulasi data. |

**Keputusan akhir dan justifikasi:**
> Peneliti sebaiknya tidak langsung menghapus outlier tanpa penjelasan, tetapi harus melaporkan kedua hasil analisis. Hal ini penting untuk menjaga integritas penelitian, transparansi data, dan kepercayaan ilmiah, sehingga pembaca atau peneliti lain dapat menilai sendiri validitas hasil penelitian.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** 

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 | 2 | 3 |
| Jenis data yang dikumpulkan | Data kuantitatif seperti penggunaan CPU, memori, jumlah proses, waktu respon, dan skor performa website | Data kualitatif seperti persepsi pengguna atau pengalaman pengguna terhadap sistem | Data hasil perancangan atau pengembangan sistem serta evaluasi implementasi teknologi |
| Limitasi paradigma | Kurang menjelaskan faktor sosial atau pengalaman pengguna | Tidak fokus pada pengukuran performa sistem secara teknis | Fokus pada pembuatan artefak atau solusi sistem, bukan pada analisis performa sistem yang sudah ada |

**Paradigma yang dipilih:** Positivis
**Alasan:** Karena penelitian menggunakan data kuantitatif dan pengujian eksperimental untuk mengukur performa sistem secara objektif melalui tools seperti htop, vmstat, curl, dan GTmetrix, sehingga pendekatan positivis paling sesuai untuk menganalisis hubungan antara manajemen memori, proses, dan performa website.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya biasanya menerima klaim seperti “95% akurat” tanpa terlalu mempertanyakan bagaimana angka tersebut diperoleh. Setelah memahami konsep rantai distorsi dalam penelitian, saya menyadari bahwa hasil penelitian dapat dipengaruhi oleh berbagai faktor seperti cara pengumpulan data, proses pengolahan data, metode analisis, dan interpretasi hasil. Oleh karena itu, saat membaca sebuah paper saya akan lebih kritis dengan menanyakan bagaimana data dikumpulkan, apakah terdapat bias atau distorsi dalam proses pengolahan data, apakah metode analisis yang digunakan sudah tepat, serta apakah kesimpulan yang diambil benar-benar didukung oleh data penelitian.
