# StudyTrack — Progres Tugas Besar RPL (SSD30)

Repositori ini berisi **dokumen progres pengerjaan** Tugas Besar Rekayasa Perangkat Lunak SSD30,
disusun bertahap mengikuti bagian **Tahapan Pengerjaan Proyek** pada spesifikasi tugas (Tahap 1–8).

Kode program tidak berada di sini — kode berada di repositori terpisah agar riwayat commit
implementasi tetap bersih dan mudah ditelusuri.

| | |
|---|---|
| **Judul proyek** | StudyTrack — Aplikasi Analisis Kebiasaan Belajar Mahasiswa dengan K-Means Clustering |
| **Mata kuliah** | Rekayasa Perangkat Lunak (SSD30) |
| **Program studi** | Data Sains |
| **Fakultas** | Sains dan Teknologi |
| **Institusi** | UIN K.H. Abdurrahman Wahid Pekalongan |
| **Komponen Data Sains** | Clustering (K-Means) + regresi linear sederhana |
| **Aplikasi (live)** | <https://whitefoxrakka-cloud.github.io/studytrack-ssd30/?demo=1> |
| **Repositori kode** | <https://github.com/whitefoxrakka-cloud/studytrack-ssd30> |

---

## Status pengerjaan

| Tahap | Nama tahap | Keluaran | Status | Dokumen |
|:-----:|-----------|----------|:------:|---------|
| 1 | Identifikasi Masalah | Deskripsi masalah dan gambaran solusi | **Selesai** | [Buka](laporan/tahap-1-identifikasi-masalah.md) |
| 2 | Analisis Kebutuhan Sistem | Dokumen analisis kebutuhan | **Selesai** | [Buka](laporan/tahap-2-analisis-kebutuhan.md) |
| 3 | Perancangan Sistem (UML) | Use Case, Activity, Sequence, Class Diagram | Belum | — |
| 4 | Perancangan Sistem & Basis Data | Arsitektur, ERD, rancangan antarmuka | Belum | — |
| 5 | Implementasi Aplikasi | Aplikasi berjalan + source code | Sedang berjalan¹ | [Repo kode](https://github.com/whitefoxrakka-cloud/studytrack-ssd30) |
| 6 | Pengujian Perangkat Lunak | Dokumen pengujian | Sebagian² | — |
| 7 | User Acceptance Testing | Dokumen hasil UAT | Belum | — |
| 8 | Evaluasi dan Penyelesaian | Aplikasi final | Belum | — |

> ¹ Versi web sudah berjalan penuh dan mencakup seluruh 11 kebutuhan fungsional. Versi final
> (Flask + SQLite + scikit-learn) belum dikerjakan.
> ² Uji unit (8 uji) sudah otomatis dan lulus; integration test, black-box test, dan dokumentasi
> pengujian formal belum disusun.

---

## Isi repositori

```
studytrack-ssd30-progress/
├─ README.md                                  halaman ini — indeks & status
├─ laporan/
│  ├─ tahap-1-identifikasi-masalah.md         latar belakang, masalah, solusi, pengguna, manfaat
│  └─ tahap-2-analisis-kebutuhan.md           aktor, 11 FR, 17 NFR, proses bisnis, data, prioritas
└─ lampiran/
   └─ dataset.md                              skema dataset, statistik, cara mengganti dengan data asli
```

---

## Ringkasan Tahap 1

**Masalah:** mahasiswa tidak punya alat ukur objektif untuk menilai kebiasaan belajarnya. Penilaian
hanya berdasarkan ingatan dan berhenti pada label "rajin/malas", sehingga saran perbaikan tidak
terarah. Diidentifikasi lima masalah turunan (P-01 … P-05).

**Solusi:** aplikasi yang mengubah catatan sesi belajar menjadi **enam variabel terukur**, lalu
mengelompokkannya dengan **K-Means** sehingga setiap mahasiswa tahu posisinya dan variabel mana yang
paling menahan.

**Pengguna:** mahasiswa (utama), dosen pembimbing akademik, dan pengelola data survei.

→ [Baca selengkapnya](laporan/tahap-1-identifikasi-masalah.md)

---

## Ringkasan Tahap 2

| Komponen | Jumlah | Keterangan |
|----------|:------:|-----------|
| Aktor | 3 | Mahasiswa, Pembimbing Akademik, Pengelola Data |
| Kebutuhan fungsional | 11 | FR-01 … FR-11, semuanya sudah terimplementasi |
| Kebutuhan nonfungsional | 17 | NFR-01 … NFR-17, semuanya bertolok ukur terukur |
| Alur proses bisnis | 4 | Alur utama, pengelolaan dataset, siklus sesi, alur Data Sains |
| Prioritas Must (MVP) | 7 | FR-01, 02, 03, 04, 05, 06, 07 |

**Angka terukur yang sudah diverifikasi:**

- Analisis K-Means 90 responden: **10,15 ms** (target ≤ 100 ms)
- Ukuran muat awal: **148 KB** tanpa kompresi (target ≤ 200 KB)
- Basis kode: **3.061 baris** (target ≤ 5.000 baris)
- Kualitas cluster: silhouette **0,355** (ambang > 0,25), SSE 162, stabil dalam 5 iterasi

→ [Baca selengkapnya](laporan/tahap-2-analisis-kebutuhan.md)

---

## Anggota kelompok

> **Perlu diisi.** Ganti bagian ini dengan nama dan NIM sebenarnya sebelum dikumpulkan.
> Sesuaikan juga kolom FR dengan hasil pembagian tugas yang disepakati.

| Anggota | Nama | NIM | Tanggung jawab (FR) | Diagram |
|:-------:|------|-----|---------------------|---------|
| 1 | _(isi nama)_ | _(isi NIM)_ | FR-01, FR-02 — pencatatan & pengelolaan sesi | 1 Activity + 1 Sequence |
| 2 | _(isi nama)_ | _(isi NIM)_ | FR-03, FR-08 — dasbor & laporan | 1 Activity + 1 Sequence |
| 3 | _(isi nama)_ | _(isi NIM)_ | FR-04, FR-05, FR-06 — mesin K-Means & penempatan | 1 Activity + 1 Sequence |
| 4 | _(isi nama)_ | _(isi NIM)_ | FR-07, FR-09 — dataset & pengaturan | 1 Activity + 1 Sequence |
| 5 | _(isi nama)_ | _(isi NIM)_ | FR-10, FR-11 — panduan awal & saran kontekstual | 1 Activity + 1 Sequence |

Use Case Diagram dan Class Diagram dikerjakan kolaboratif oleh seluruh anggota (Tahap 3).

---

## Cara membaca dokumen

- Setiap laporan tahap diawali **identitas tahap** dan **keluaran yang diminta** sesuai spesifikasi,
  sehingga mudah dicocokkan dengan ketentuan dosen.
- Bagian akhir setiap laporan memuat **daftar periksa keluaran** — semua butir yang diminta
  spesifikasi ditandai selesai.
- Diagram alur ditulis dengan **Mermaid** sehingga langsung tampil saat dibuka di GitHub.
- Setiap kebutuhan fungsional memiliki **kriteria penerimaan**, bukan hanya deskripsi, agar dapat
  diuji pada Tahap 6.
- Angka yang diklaim selalu disertai **cara memperolehnya** (diukur, dihitung, atau diuji), bukan
  perkiraan.

---

## Catatan kejujuran data

Dataset yang dipakai saat ini **sintetis** (90 responden yang dibangkitkan dari tiga arketipe +
derau normal). Data ini dipakai agar seluruh alur sistem dapat diuji dan didemokan sebelum survei
lapangan terkumpul. Seluruh angka pada laporan akan diperbarui setelah data survei asli masuk;
struktur variabel dan metode analisis tidak berubah. Rincian ada di
[`lampiran/dataset.md`](lampiran/dataset.md).

---

## Riwayat dokumen

| Tanggal | Versi | Perubahan |
|---------|-------|-----------|
| 21 November 2026 | v1.0 | Laporan Tahap 1 dan Tahap 2 disusun; lampiran dataset ditambahkan |
