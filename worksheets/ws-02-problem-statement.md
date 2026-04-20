# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Sistem Operasi dan Performa Website
  Konteks  : Analisis performa sistem informasi akademik berbasis web pada sistem operasi Linux

System Context
  Input       : Permintaan akses website (HTTP request) dari pengguna melalui browser
  Process     : Sistem operasi Linux mengelola memori dan proses saat website diakses serta dilakukan pemantauan menggunakan tools htop, vmstat, curl, dan GTmetrix
  Output      : Data performa sistem seperti penggunaan CPU, memori, jumlah proses aktif, dan waktu respon website
  Outcome     : Diketahui tingkat efisiensi manajemen proses dan struktur memori terhadap performa website
  Constraints : Pengujian dilakukan pada Linux Ubuntu 22.04 di lingkungan VirtualBox dan jumlah pengujian terbatas
  Stakeholders: Pengembang sistem, administrator server, perguruan tinggi, mahasiswa, dan dosen

Fenomena → Problem
  Fenomena yang diamati             : Website sistem informasi akademik kadang mengalami keterlambatan akses
  Gejala (symptom) yang terukur     : Waktu loading website cukup lama dan skor performa website masih rendah
  Masalah yang didiagnosis          : Manajemen proses dan struktur memori sistem operasi belum optimal dalam mendukung performa website
  Masalah riset (researchable)      : Bagaimana pengaruh struktur memori dan manajemen proses pada sistem operasi Linux terhadap performa sistem informasi akademik berbasis web
  Variabel yang terukur             : Penggunaan CPU, penggunaan memori, jumlah proses aktif, waktu respon website, dan skor performa website

Problem Quality Check
  [ ya ] Clarity — Apakah satu orang membaca akan paham?
  [ya ] Measurability — Apakah ada metrik kuantitatif?
  [ya ] Relevance — Apakah penting untuk domain?
  [ya ] Testability — Apakah bisa gagal?
  [ya ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Penelitian ini bertujuan untuk menganalisis pengaruh struktur memori dan manajemen proses pada sistem operasi Linux terhadap performa sistem informasi akademik berbasis web. Permasalahan muncul karena akses website akademik sering mengalami keterlambatan yang dapat mempengaruhi kenyamanan pengguna. Oleh karena itu, penelitian ini mengukur beberapa variabel seperti penggunaan CPU, penggunaan memori, jumlah proses aktif, serta waktu respon website menggunakan berbagai tools pengujian sistem. Hasil penelitian diharapkan dapat memberikan pemahaman mengenai efisiensi pengelolaan sumber daya sistem operasi serta memberikan rekomendasi untuk meningkatkan performa sistem informasi akademik.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Analisis performa sistem informasi akademik berbasis web pada sistem operasi Linux.

| Tahap | Hasil |
|-------|-------|
| Reality | Sistem informasi akademik berbasis web sering mengalami keterlambatan akses ketika digunakan oleh banyak pengguna. |
| Observed Issue (Symptom) | Waktu akses website akademik cukup lama dengan rata-rata sekitar 2,45 detik dan performa website hanya memperoleh skor 56% (grade D) pada pengujian GTmetrix. |
| Diagnosed Problem (Root Cause) | Pengelolaan sumber daya sistem operasi seperti struktur memori dan manajemen proses serta optimalisasi website yang belum maksimal. |
| Researchable Problem | Bagaimana pengaruh struktur memori dan manajemen proses pada sistem operasi Linux terhadap performa sistem informasi akademik berbasis web? |
| Measurable Variable | Jumlah proses aktif, penggunaan memori, CPU usage, waktu akses website, serta skor performa website dari GTmetrix. |

**Apakah terjebak solution-first thinking?** [ ] Ya / [ ini ] Tidak
> Jika ya, kembali ke tahap mana? 



## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Permintaan akses website sistem informasi akademik (HTTP request) dari pengguna melalui browser. |
| Process | Sistem operasi Linux mengelola proses dan memori saat website diakses, kemudian dilakukan pemantauan performa menggunakan tools seperti htop, vmstat, curl, dan GTmetrix. |
| Output | Data hasil pengujian performa seperti penggunaan CPU, penggunaan memori, jumlah proses aktif, serta waktu respon website. |
| Outcome | Diketahui tingkat efisiensi manajemen memori dan proses pada sistem operasi Linux serta performa website sistem informasi akademik. |
| Constraints | Pengujian dilakukan pada lingkungan Linux Ubuntu 22.04 di VirtualBox, jumlah pengujian terbatas, dan kondisi jaringan dapat mempengaruhi hasil. |
| Stakeholders | Pengembang sistem informasi akademik, administrator server, institusi perguruan tinggi, dan pengguna sistem (mahasiswa dan dosen). |

**Komponen mana yang paling relevan dengan masalah riset?** Process 

Alasan: karena penelitian fokus pada analisis manajemen proses dan struktur memori pada sistem operasi Linux yang mempengaruhi performa website.

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 4 | Masalah penelitian sudah jelas yaitu menganalisis pengaruh struktur memori dan manajemen proses terhadap performa website, namun masih bisa diperjelas dengan menambahkan konteks lingkungan pengujian. |
| Measurability | 5 | Variabel penelitian dapat diukur secara kuantitatif seperti penggunaan CPU, memori, jumlah proses aktif, dan waktu respon website. |
| Relevance | 5 | Penelitian sangat relevan dengan kebutuhan peningkatan performa sistem informasi akademik yang digunakan di perguruan tinggi. |
| Testability | 5 | Masalah dapat diuji melalui metode eksperimen menggunakan tools seperti htop, vmstat, curl, dan GTmetrix. |
| Impact | 4 | Hasil penelitian dapat membantu optimalisasi sistem informasi akademik, meskipun implementasinya masih terbatas pada lingkungan tertentu. |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Penelitian ini bertujuan untuk menganalisis pengaruh struktur memori dan manajemen proses pada sistem operasi Linux terhadap performa sistem informasi akademik berbasis web. Pengujian dilakukan dengan mengukur penggunaan CPU, memori, jumlah proses aktif, serta waktu respon website menggunakan beberapa tools pengujian sistem. Hasil analisis diharapkan dapat memberikan pemahaman mengenai efisiensi pengelolaan sumber daya sistem operasi serta memberikan rekomendasi untuk meningkatkan performa sistem informasi akademik.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah yang biasa ditemui saat coding seperti bug atau error umumnya memiliki penyebab yang jelas dan dapat langsung diperbaiki dengan menemukan kesalahan pada kode program. Pendekatan yang digunakan biasanya bersifat teknis dan langsung, seperti melakukan debugging, memeriksa log error, atau memperbaiki sintaks program.

Sedangkan masalah riset bersifat lebih kompleks dan belum memiliki solusi yang pasti. Dalam penelitian, masalah harus didefinisikan melalui proses analisis, pengamatan fenomena, serta pengumpulan data terlebih dahulu sebelum dapat ditarik kesimpulan. Pendekatannya juga lebih sistematis, menggunakan metode ilmiah seperti perumusan masalah, pengumpulan data, analisis, dan pengujian hipotesis.

Perbedaan fundamentalnya adalah bahwa masalah coding biasanya memiliki solusi yang jelas dan langsung, sedangkan masalah riset membutuhkan proses investigasi dan analisis yang mendalam untuk menemukan atau memahami solusi yang mungkin.
