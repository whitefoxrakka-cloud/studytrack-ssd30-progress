# LOGBOOK PEKAN 0 — 9 s.d. 15 November 2026

**Fokus pekan:** pembentukan kelompok, pemilihan tema, dan pengajuan judul
**Tahap proyek:** persiapan (belum masuk Tahap 1)
**Keluaran:** kelompok terbentuk, tema disepakati, formulir pengajuan terisi

---

## 1. Rekap pekan

| Anggota | Fokus pekan ini | FR | Keluaran | Jam |
|:-------:|-----------------|----|----------|:---:|
| Yuniar Zahra Wiyani | Observasi kebiasaan belajar di lingkungan sendiri | — | Daftar 12 keluhan mahasiswa | 3 |
| Aninda Rizqi Amelia | Studi pustaka aplikasi pencatat kebiasaan | — | Ringkasan 5 aplikasi pembanding | 3 |
| Maheswari Pasa Putri Syamsudar | Studi pustaka K-Means dan validasi cluster | — | Catatan 4 sumber | 4 |
| Hasan | Survei kecil kebutuhan data | — | 23 tanggapan awal | 3 |
| Sifa Sabrina | Penyusunan usulan tema dan judul | — | 5 calon judul | 3 |

## 2. Rincian harian

### 2.1 Yuniar Zahra Wiyani — 60124004

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 10 Nov | Diskusi kelompok: menentukan lingkup proyek | Kesepakatan lingkup: mahasiswa, kebiasaan belajar | Catatan rapat 10 Nov |
| 12 Nov | Mengamati dan menanyakan kebiasaan belajar 12 teman sekelas | Daftar 12 keluhan, dikelompokkan menjadi 4 pola | Lampiran wawancara |
| 14 Nov | Merumuskan dugaan awal: masalahnya bukan malas, tetapi tidak tahu pola sendiri | Catatan dugaan awal | Catatan pribadi |

**Catatan.** Temuan yang paling sering muncul: mahasiswa merasa "sudah belajar banyak" tetapi tidak
tahu berapa jam sebenarnya, dan tidak menyadari hubungan antara jam tidur dan hasil belajarnya.
Temuan ini menjadi benih rumusan masalah pada Tahap 1.

### 2.2 Aninda Rizqi Amelia — 60124009

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 11 Nov | Mencari aplikasi pembanding (Forest, Toggl, Study Bunny, Notion, spreadsheet) | Tabel 5 aplikasi: fitur, kekurangan | Tabel pembanding |
| 13 Nov | Menelaah mengapa aplikasi pencatat biasa tidak cukup | Catatan: pencatatan tanpa analisis tidak mengubah perilaku | Catatan pribadi |
| 15 Nov | Menyusun kerangka manfaat bagi pengguna | Draf 4 butir manfaat | Draf Bab I |

**Catatan.** Semua aplikasi pembanding berhenti pada pencatatan dan pengingat. Tidak ada yang
mengelompokkan pengguna berdasarkan pola dan membandingkannya dengan pengguna lain. Di situlah celah
yang akan diisi.

### 2.3 Maheswari Pasa Putri Syamsudar — 60124010

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 11 Nov | Membaca dasar K-Means, inisialisasi k-means++, dan pemilihan k | Catatan 4 sumber | Catatan pustaka |
| 13 Nov | Mempelajari silhouette score dan elbow method | Catatan rumus dan ambang | Catatan pustaka |
| 15 Nov | Menguji K-Means pada data mainan 30 titik | Hasil: 3 cluster terbentuk benar | Skrip uji coba |

**Catatan.** Uji coba pada data mainan menunjukkan satu masalah yang kemudian menjadi keputusan
perancangan: tanpa standardisasi, fitur dengan satuan terbesar mendominasi jarak. Pada data mainan,
fitur berskala 0–24 menenggelamkan fitur berskala 0–7.

### 2.4 Hasan — 60124013

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 12 Nov | Menyusun daftar variabel yang mungkin diukur | 9 calon variabel | Draf instrumen |
| 14 Nov | Menyebar survei singkat ke 23 responden | 23 tanggapan | Rekap survei |
| 15 Nov | Menyaring variabel yang dapat diukur konsisten | 6 variabel final | Draf instrumen |

**Catatan.** Tiga variabel dibuang karena terlalu kabur untuk diukur ("motivasi", "fokus",
"suasana hati"). Yang bertahan adalah yang bisa dijawab dengan angka: durasi, frekuensi, tidur, tugas
selesai, jam HP saat belajar, dan jumlah sesi mandiri.

### 2.5 Sifa Sabrina — 60124023

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 10 Nov | Menyusun lima calon judul sesuai tema Data Sains | 5 judul dengan alasan | Draf judul |
| 13 Nov | Menyiapkan isi formulir pengajuan tema dan anggota | Formulir terisi | Formulir pengajuan |
| 15 Nov | Menyusun jadwal kerja tiga pekan | Jadwal pekan 1–3 | Jadwal kelompok |

## 3. Keluaran pekan

| No | Keluaran | Keterangan |
|:--:|----------|------------|
| 1 | Kelompok 5 orang terbentuk | Yuniar, Aninda, Maheswari, Hasan, Sifa |
| 2 | Tema disepakati | Analisis kebiasaan belajar dengan clustering |
| 3 | Enam variabel final | Disaring dari 9 calon |
| 4 | Formulir pengajuan tema terisi | Dikirim melalui formulir yang disediakan dosen |
| 5 | Jadwal kerja tiga pekan | Acuan logbook pekan 1–3 |

## 4. Kendala

| Kendala | Dampak | Cara diselesaikan |
|---------|--------|-------------------|
| Tiga variabel tidak dapat diukur secara konsisten | Instrumen tidak dapat dipakai | Dibuang, diganti variabel yang terukur |
| Aplikasi pembanding tidak ada yang melakukan clustering | Tidak ada acuan rupa | Menjadi peluang: celah itulah yang diisi |
| Anggota belum sepakat soal lingkup (semua mahasiswa atau satu prodi) | Arah data belum jelas | Diputuskan: dataset acuan lintas prodi, data pribadi per mahasiswa |

## 5. Rencana pekan berikutnya

| Anggota | Rencana | FR |
|:-------:|---------|----|
| Yuniar | Menulis latar belakang dan identifikasi masalah | FR-01, FR-02 |
| Aninda | Menyusun rumusan masalah, tujuan, dan manfaat | FR-03, FR-08 |
| Maheswari | Menulis metode K-Means untuk dokumen | FR-04, FR-05 |
| Hasan | Membangun dataset 90 responden dan skema datanya | FR-06, FR-07 |
| Sifa | Menyusun NFR dan proses bisnis | FR-09, FR-10, FR-11 |
