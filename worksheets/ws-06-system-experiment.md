# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: ____________________

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|          | IV   |                 |                           |
|          | DV   |                 |                           |
|          | CV   |                 |                           |

4 Prinsip Desain:
  [ ] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [ ] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [ ] Measurement Integration — Pengukuran DV built-in
  [ ] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : ____________________
  Parameter      : ____________________
  Output format  : ____________________
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah manajemen proses dan struktur memori Linux Ubuntu 22.04 LTS menghasilkan performa website sistem informasi akademik yang lebih efisien berdasarkan response time, penggunaan CPU/memori, dan GTmetrix performance score?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Manajemen proses Linux | IV | Modul monitoring proses (htop, vmstat) | Mengamati CPU utilization, load average, proses aktif |
|Struktur memori Linux | IV |Modul monitoring memori |Mengukur penggunaan RAM, cache, dan virtual memory |
|Performa website | DV |Modul pengujian performa (curl/time dan GTmetrix) | Mengukur response time, GTmetrix score, LCP|
|Lingkungan pengujian|CV|Konfigurasi hardware dan jaringan|Menjaga RAM, CPU, bandwidth, dan OS tetap sama|

**Apakah semua variabel bisa di-map?** [ ya] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? Tidak perlu tambahan karena seluruh variabel sudah memiliki komponen sistem yang sesuai.

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ | Setiap komponen monitoring dan pengujian terhubung langsung dengan variabel penelitian|
| Modularity |✅ |Pengujian CPU, memori, dan website dilakukan dengan tools terpisah |
| Controllability | ✅|Konfigurasi sistem, jaringan, dan spesifikasi hardware dijaga tetap |
| Measurability | ✅| Semua data performa otomatis dihasilkan oleh tools Linux dan GTmetrix|

**Prinsip mana yang paling sulit dipenuhi?** Controllability
**Strategi untuk mengatasinya:**
> Menjaga kondisi jaringan, spesifikasi hardware, dan jumlah proses latar belakang tetap stabil selama eksperimen dilakukan.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ Monitoring proses Linux | ✅ Monitoring memori Linux |✅ GTmetrix & curl testing | Data performa lengkap dan stabil |
| – A | ❌ Tanpa monitoring proses | ✅ | ✅ | Analisis CPU dan proses menjadi tidak lengkap|
| – B | ✅ |❌ Tanpa monitoring memori | ✅ |Pengaruh penggunaan RAM tidak dapat dianalisis |
| – C | ✅ | ✅ | ❌ Tanpa GTmetrix/curl| Tidak ada data performa website eksternal|

**Komponen mana yang diprediksi paling berkontribusi?** Komponen C (GTmetrix dan curl testing)
**Mengapa?**
> Karena komponen ini secara langsung menghasilkan data performa website seperti response time, loading speed, dan performance score yang menjadi fokus utama penelitian.

---

## Refleksi
Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
Jika sistem dibangun seperti produk monolitik dengan banyak fitur tambahan, maka eksperimen akan sulit dilakukan karena variabel penelitian bercampur dengan fitur lain yang tidak relevan. Hal ini meningkatkan noise dan menyulitkan peneliti menentukan faktor yang benar-benar memengaruhi hasil penelitian.

Arsitektur modular penting dalam riset karena memungkinkan setiap variabel dipisahkan dan diuji secara independen. Dengan modularitas, peneliti dapat mengubah satu variabel tanpa memengaruhi komponen lain sehingga eksperimen menjadi lebih terkontrol, terukur, dan mudah direproduksi.
