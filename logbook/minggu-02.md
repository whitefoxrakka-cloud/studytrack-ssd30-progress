# LOGBOOK PEKAN 2 — 23 s.d. 29 November 2026

**Fokus pekan:** Tahap 3 (UML), Tahap 4 (arsitektur dan basis data), laporan Bab I–IV, dan presentasi
**Tahap proyek:** 3 dan 4 selesai
**Keluaran:** dokumen UML, dokumen perancangan teknis, laporan Bab I–IV (DOCX + PDF), PPT Tahap 1–4

---

## 1. Rekap pekan

| Anggota | Fokus pekan ini | FR | Keluaran | Jam |
|:-------:|-----------------|----|----------|:---:|
| Yuniar Zahra Wiyani | AD-01, SD-01, Bab III bagian pencatatan | FR-01, FR-02 | 2 diagram, 1 subbab | 7 |
| Aninda Rizqi Amelia | AD-02, SD-02, Bab IV bagian antarmuka | FR-03, FR-08 | 2 diagram, 1 subbab | 7 |
| Maheswari Pasa Putri Syamsudar | Class diagram, AD-03, SD-03, Bab IV Data Sains | FR-04, FR-05 | 3 diagram, 1 subbab | 9 |
| Hasan | ERD, DDL, AD-04, SD-04 | FR-06, FR-07 | 2 diagram, skema basis data | 8 |
| Sifa Sabrina | Use case, rancangan antarmuka, AD-05, SD-05, PPT | FR-09, FR-10, FR-11 | 3 diagram, PPT | 9 |

## 2. Rincian harian

### 2.1 Yuniar Zahra Wiyani — 60124004 · FR-01, FR-02

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 24 Nov | Menyusun AD-01: alur mencatat dan mengelola sesi | AD-01 | `laporan/tahap-3` §3.1 |
| 25 Nov | Menyusun SD-01: pesan antaroobjek saat menyimpan dan menghapus sesi | SD-01 | `laporan/tahap-3` §4.1 |
| 26 Nov | Menulis penjelasan AD-01 dan SD-01, termasuk alasan validasi di lapisan UI | 2 subbab | `laporan/tahap-3` |
| 27 Nov | Menyusun Bab III bagian pencatatan sesi untuk laporan | Draf subbab | `laporan/study-track-bab-1-4.docx` |

**Keputusan yang diambil.** Pada SD-01, blok `alt` hanya mengizinkan cabang valid yang menyentuh
penyimpanan. Ini konsekuensi dari sifat `localStorage` yang tidak punya transaksi — data cacat yang
sudah tertulis tidak dapat dibatalkan, jadi pencegahannya harus di depan.

### 2.2 Aninda Rizqi Amelia — 60124009 · FR-03, FR-08

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 24 Nov | Menyusun AD-02: alur dasbor dan laporan, termasuk dua cabang pengaman | AD-02 | `laporan/tahap-3` §3.2 |
| 25 Nov | Menyusun SD-02: pemanggilan `regresi()` dan pembuatan grafik | SD-02 | `laporan/tahap-3` §4.2 |
| 26 Nov | Menulis Bab IV bagian implementasi antarmuka | Draf subbab | `laporan/study-track-bab-1-4.docx` |
| 27 Nov | Memeriksa ulang tangkapan layar untuk bagian rancangan antarmuka | 10 tangkapan layar | `laporan/img/` |

**Keputusan yang diambil.** Dua cabang pengaman pada AD-02 dipertahankan meski terlihat seperti
"kasus pinggiran": keadaan kosong dan data kurang dari dua titik. Keduanya adalah keadaan yang
**pasti** dialami pengguna baru, bukan kemungkinan langka.

### 2.3 Maheswari Pasa Putri Syamsudar — 60124010 · FR-04, FR-05

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 24 Nov | Menyusun class diagram kolaboratif: 10 kelas dan hubungannya | Class diagram | `laporan/tahap-3` §5.1 |
| 25 Nov | Menyusun AD-03: alur K-Means lengkap dengan gerbang mutu | AD-03 | `laporan/tahap-3` §3.3 |
| 26 Nov | Menyusun SD-03: urutan pemanggilan di dalam mesin | SD-03 | `laporan/tahap-3` §4.3 |
| 26 Nov | Menulis Bab IV bagian implementasi dan integrasi Data Sains | Draf subbab | `laporan/study-track-bab-1-4.docx` |
| 27 Nov | Menjalankan ulang uji unit setelah penomoran FR diseragamkan | 8/8 lulus | `tests/kmeans.test.mjs` |

**Keputusan yang diambil.** `elbow()` dipanggil untuk k = 2 sampai 6 sekaligus, bukan hanya untuk k
terpilih. Alasannya: grafik elbow adalah **pembenaran** pemilihan k; menjalankannya untuk satu nilai
saja menghilangkan gunanya.

### 2.4 Hasan — 60124013 · FR-06, FR-07

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 24 Nov | Menyusun ERD: 8 tabel, relasi, dan kardinalitasnya | ERD | `laporan/tahap-4` §3.2 |
| 25 Nov | Menulis DDL SQLite lengkap dengan `CHECK`, indeks, dan satu view | DDL | `laporan/tahap-4` §3.4 |
| 25 Nov | Menguji DDL di SQLite: `CHECK`, `RESTRICT`, `CASCADE`, `SET NULL` | Hasil uji constraint | Catatan uji |
| 26 Nov | Menyusun AD-04 dan SD-04 | 2 diagram | `laporan/tahap-3` §3.4, §4.4 |
| 27 Nov | Menulis bagian normalisasi dan pemetaan state ke tabel | Subbab §3.5–§3.6 | `laporan/tahap-4` |

**Hasil uji basis data.** DDL dijalankan pada SQLite dan diuji dengan lima kasus:

| Kasus | Harapan | Hasil |
|-------|---------|-------|
| `durasi_menit` = 9999 | Ditolak | Ditolak: `CHECK constraint failed` |
| `tidur_jam` = 30 | Ditolak | Ditolak: `CHECK constraint failed` |
| Hapus `dataset` yang dipakai `analisis` | Ditolak | Ditolak: `FOREIGN KEY constraint failed` |
| Hapus `pengguna` | Sesi dan penempatan ikut terhapus | Terhapus; `analisis` tetap ada dengan `pengguna_id` menjadi `NULL` |
| `v_rekap_pekan` atas 2 sesi | Satu baris rekap | Benar: 2 sesi, 210 menit, rata-rata 105 menit |

**Keputusan yang diambil.** Relasi `pengguna → analisis` memakai `SET NULL`, sedangkan
`dataset → analisis` memakai `RESTRICT`. Keduanya sengaja berbeda: hasil analisis adalah bukti yang
tetap berguna meski akunnya dihapus, tetapi dataset yang menjadi bahan tidak boleh hilang diam-diam.

### 2.5 Sifa Sabrina — 60124023 · FR-09, FR-10, FR-11

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 24 Nov | Menyusun use case diagram: 3 aktor, 15 use case, relasi include/extend | Use case diagram | `laporan/tahap-3` §2.1 |
| 25 Nov | Merancang antarmuka: model navigasi, 8 layar, tata letak, token warna | Rancangan antarmuka | `laporan/tahap-4` §4 |
| 26 Nov | Menyusun AD-05 dan SD-05 | 2 diagram | `laporan/tahap-3` §3.5, §4.5 |
| 26 Nov | Menyusun kerangka PPT Tahap 1–4 | 18 slide | `presentasi/study-track-tahap-1-4.pptx` |
| 27 Nov | Menyusun bagian aksesibilitas dan daftar teknologi | Subbab §4.6, §5 | `laporan/tahap-4` |

**Keputusan yang diambil.** Tema, animasi, dan mode luring tidak dijadikan use case. Ketiganya tidak
menambah kemampuan bisnis dan sudah dibahas sebagai NFR pada Tahap 2. Memasukkannya ke diagram use
case akan mengaburkan fokus diagram.

## 3. Keluaran pekan

| No | Keluaran | Berkas | Bukti |
|:--:|----------|--------|-------|
| 1 | Dokumen perancangan UML | `laporan/tahap-3-perancangan-uml.md` | commit `f4a6369` |
| 2 | 1 use case, 5 activity, 5 sequence, 1 class diagram | — | `laporan/tahap-3` §2–§5 |
| 3 | Dokumen arsitektur, basis data, dan antarmuka | `laporan/tahap-4-arsitektur-basis-data.md` | commit `f4a6369` |
| 4 | ERD 8 tabel + DDL SQLite yang sudah diuji | — | `laporan/tahap-4` §3 |
| 5 | 10 tangkapan layar aplikasi | `laporan/img/` | commit `f4a6369` |
| 6 | Laporan Bab I–IV format DOCX | `laporan/study-track-bab-1-4.docx` | berkas laporan |
| 7 | Laporan Bab I–IV format PDF | `laporan/study-track-bab-1-4.pdf` | berkas laporan |
| 8 | Presentasi Tahap 1–4 | `presentasi/study-track-tahap-1-4.pptx` | berkas presentasi |
| 9 | Logbook tiga pekan | `logbook/` | commit logbook |

## 4. Kendala pekan ini

| Kendala | Dampak | Penyelesaian |
|---------|--------|--------------|
| Dua diagram Mermaid gagal dirender saat pertama dicoba | Diagram tidak tampil di GitHub | Penyebabnya batas laju layanan render, bukan kesalahan sintaks; diulang dan berhasil |
| Class diagram awal hanya 6 kelas dan beberapa kelas tidak punya berkas nyata | Diagram tidak dapat dicocokkan dengan kode | Ditambah menjadi 10 kelas, semuanya dipetakan ke berkas |
| Label diagram memuat tanda `<` dan `&` | Parser Mermaid menolak | Label ditulis ulang dengan kata ("di bawah 1e-6") |
| Skema basis data awal menggabungkan sesi dan responden | Normalisasi gagal, hapus data berisiko | Dipisah menjadi `sesi_belajar` dan `responden` |

## 5. Rencana pekan berikutnya

| Anggota | Rencana | Tahap |
|:-------:|---------|-------|
| Yuniar | Menyiapkan backend Flask untuk pencatatan sesi | Tahap 5 |
| Aninda | Menyiapkan autentikasi dan peran (mahasiswa, dosen) | Tahap 5 |
| Maheswari | Memindahkan perhitungan ke scikit-learn dan menguji kesetaraan hasil | Tahap 5 |
| Hasan | Menerapkan DDL ke SQLite dan menghubungkan dengan API | Tahap 5 |
| Sifa | Menyusun rencana pengujian dan kuesioner UAT | Tahap 6–7 |
