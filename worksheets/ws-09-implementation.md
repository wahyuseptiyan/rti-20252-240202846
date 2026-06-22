# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : ____________________
  RAM     : ____________________
  GPU     : ____________________
  Storage : ____________________

Software:
  OS        : ____________________
  Runtime   : ____________________
  Framework : ____________________

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
|         |         |        |               |
|         |         |        |               |

Konfigurasi:
  Config file     : ____________________
  Random seed     : ____________________
  Hyperparameters : ____________________

Reproducibility Check:
  [ ] Dependency terdokumentasi (requirements.txt / lock file)
  [ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [ ] Config di version control
  [ ] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | AMD Ryzen 5 7530U @ 2.00 GHz (6 Cores, 12 Threads) |
| RAM | 8 GB / 16 GB DDR4 (Host Laptop Lenovo) |
| GPU | Integrated AMD Radeon Graphics |
| OS | Microsoft Windows 11 Home Single Language 64-bit |
| Runtime | Oracle VM VirtualBox Version 7.0 |
| Framework | Linux Ubuntu 22.04 LTS (Alokasi VM: RAM 4GB, CPU 2 Cores) |
| Random Seed | Locked (Sistem Pengujian Tidak Menggunakan Fungsi Acak) |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| `htop` | 3.0.5 | Monitoring visual proses aktif dan beban core CPU secara real-time |
| `vmstat` | 3.3.17 | Merekam statistik memori virtual, free RAM, dan aktivitas swapping |
| `curl` | 7.81.0 | Melakukan HTTP request ke SIAKAD dan mengukur network response time |
| `procps` | 3.3.17 | Paket utilitas dasar Linux yang menyediakan engine internal vmstat |
| `openssl` | 3.0.2 | Menyediakan library enkripsi TLS/SSL untuk request HTTPS via curl |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed / Kondisi Jaringan | Metrik Utama 1: Response Time (`curl`) | Metrik Utama 2: Score (`GTmetrix`) | Hasil Sama/Mirip? |
|:---:|:---|:---:|:---:|:---:|
| 1 | Jam 23:00 WIB (Idle Background) | 2.15 detik | 58% | — |
| 2 | Jam 23:05 WIB (Idle Background) | 2.20 detik | 57% | [x] Ya / [ ] Tidak |
| 3 | Jam 23:10 WIB (Idle Background) | 2.12 detik | 59% | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> Hasil pengujian simulasi menunjukkan angka yang sangat mirip (berkisar antara 2.12 - 2.20 detik dengan skor GTmetrix 57% - 59%), yang menandakan tingkat repeatability sistem sudah baik. Sedikit variasi milidetik yang terjadi murni disebabkan oleh fluktuasi kecil pada latensi jaringan internet publik (network jitter) saat melakukan request ke server sistem informasi akademik dari jaringan lokal peneliti.

**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Cache dibersihkan antar-run
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Dampak Manajemen Proses dan Memori Linux Ubuntu Terhadap Performa Web Sistem Informasi Akademik

## 1. Environment
- Host OS: Windows 11 Home Single Language 64-bit (Lenovo Laptop)
- Hypervisor: Oracle VM VirtualBox v7.0
- Guest OS (Target): Linux Ubuntu 22.04 LTS
- VM Resource: RAM 4GB, CPU 2 Cores
- Tools Utama: htop v3.0.5, vmstat v3.3.17, curl v7.81.0

## 2. Installation
Untuk menyiapkan lingkungan pengujian di Ubuntu, jalankan perintah berikut di terminal:
$ sudo apt update
$ sudo apt install htop vmstat curl -y

## 3. Data
- Sumber Data: Endpoint URL halaman login Sistem Informasi Akademik (SIAKAD).
- Format Data: Output log teks mentah (raw text) dari terminal untuk metrik CPU, RAM, dan waktu respon HTTP (dalam satuan detik).

## 4. Execution
Langkah-langkah untuk mengeksekusi pengujian:
1. Buka terminal Ubuntu, lalu bersihkan cache memori RAM agar adil sebelum mulai:
   $ sudo sync && echo 3 | sudo tee /proc/sys/vm/drop_caches
2. Jalankan perintah curl untuk mengukur response time website target:
   $ curl -o /dev/null -s -w "Connect: %{time_connect}s | TTFB: %{time_starttransfer}s | Total: %{time_total}s\n" [https://siakad.target-kampus.ac.id](https://siakad.target-kampus.ac.id)
3. Di tab terminal baru, rekam status memori internal selama 5 detik:
   $ vmstat 1 5

## 5. Configuration
- Target URL: [https://siakad.target-kampus.ac.id](https://siakad.target-kampus.ac.id) (Kunci pada halaman login statis).
- Waktu Pengujian: Pukul 23:00 WIB s.d. 23:30 WIB (Kondisi latensi jaringan internet publik dalam keadaan stabil/idle).
- Interval Replikasi: Dijeda selama 2 menit antar-run untuk pendinginan resource kernel OS.

## 6. Expected Output
Output yang diharapkan keluar di terminal berupa catatan waktu seperti ini:
Connect: 0.045s | TTFB: 1.210s | Total: 2.152s

Dan output dari vmstat akan menunjukkan status alokasi memori bebas (free) dan swapping (si/so):
procs -----------memory---------- ---swap--
 r  b   swpd   free   buff  cache   si   so
 1  0      0 210452  84320 452104    0    0
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya

**Komponen yang belum terdokumentasi:**
> Saat ini eksperimen baru mencapai level **Repeatability**, karena pengujian baru terbukti stabil jika dijalankan ulang oleh peneliti yang sama di perangkat hardware laptop Lenovo yang sama. 
> 
> Komponen yang masih hilang untuk mencapai level *Reproducibility* penuh adalah script otomatisasi pengujian (seperti script bash otomatis untuk menjalankan curl dan vmstat secara serentak) serta petunjuk standarisasi bandwidth jaringan internet eksternal yang lebih detail. Tanpa hal tersebut, jika orang lain mencobanya di jaringan internet yang berbeda, fluktuasi luar dapat mengganggu validitas data performa webnya.
