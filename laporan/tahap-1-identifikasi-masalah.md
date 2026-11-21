# Laporan Tahap 1 — Identifikasi Masalah

| | |
|---|---|
| **Proyek** | StudyTrack — Aplikasi Analisis Kebiasaan Belajar Mahasiswa dengan K-Means Clustering |
| **Mata kuliah** | Rekayasa Perangkat Lunak (SSD30) |
| **Program studi** | Data Sains · Fakultas Sains dan Teknologi |
| **Institusi** | UIN K.H. Abdurrahman Wahid Pekalongan |

| | |
|---|---|
| Tahap | 1 dari 8 — Identifikasi Masalah |
| Keluaran yang diminta | Deskripsi masalah dan gambaran solusi aplikasi |
| Status | Selesai |
| Komponen Data Sains | *Clustering* (K-Means) + regresi linear sederhana |

---

## 1. Latar Belakang Permasalahan

Belajar bukan kegiatan tunggal. Ia tersusun dari beberapa variabel yang saling mempengaruhi: berapa lama seseorang belajar, seberapa sering, seberapa cukup tidurnya, berapa tugas yang benar-benar selesai, seberapa besar gangguan ponsel saat belajar, dan seberapa besar inisiatif belajar atas kemauan sendiri. Variabel-variabel ini bergerak bersama — menambah durasi belajar sambil mengurangi jam tidur, misalnya, sering tidak menghasilkan perbaikan apa pun karena sesi berikutnya berjalan dalam kondisi tidak segar.

Persoalannya, mahasiswa hampir tidak pernah menilai variabel-variabel itu secara terpisah. Yang tersisa di ingatan biasanya hanya dua label kasar: **"rajin"** atau **"malas"**. Label seperti ini tidak bisa ditindaklanjuti. Ia tidak menunjukkan bagian mana yang bermasalah, seberapa jauh dari kondisi ideal, dan perubahan kecil apa yang paling berpengaruh.

Akibatnya muncul dua pola yang sering berulang:

1. **Perbaikan yang salah sasaran.** Mahasiswa yang merasa kurang rajin menambah durasi belajar, padahal masalah sebenarnya ada pada frekuensi yang tidak teratur atau tidur yang kurang dari enam jam. Usaha ditambah, hasil tidak berubah, lalu muncul kesimpulan bahwa "belajarnya memang tidak cukup" — padahal variabel yang diperbaiki bukan variabel yang menahan.
2. **Penilaian yang tidak punya pembanding.** Tanpa acuan, mahasiswa tidak tahu apakah kebiasaannya sudah tergolong baik atau baru di bawah rata-rata. Angka "3 jam per hari" tidak berarti apa-apa sebelum dibandingkan dengan pola mahasiswa lain yang punya beban akademik serupa.

Di sisi lain, pembimbing akademik menghadapi keterbatasan yang berbeda. Dosen pembimbing biasanya hanya bertemu mahasiswa pada momen-momen formal — bimbingan awal semester, konsultasi masalah nilai, atau saat nilai sudah keluar. Pada titik itu, kebiasaan belajar sudah terbentuk dan sulit diubah. Tidak ada data antara yang bisa dipakai untuk mengenali mahasiswa yang mulai tergelincir sebelum nilainya jatuh.

Persoalan ini pada dasarnya adalah persoalan **pengukuran dan pengelompokan**, bukan persoalan motivasi. Karena itu ia cocok diselesaikan dengan pendekatan Data Sains: mengubah kebiasaan belajar yang abstrak menjadi enam variabel terukur, lalu mengelompokkan pola yang muncul sehingga tiap mahasiswa tahu persis di mana posisinya dan apa yang perlu diubah.

> **Catatan metodologis.** Dataset yang dipakai pada versi aplikasi saat ini masih **sintetis** — 90 responden yang dibangkitkan dari tiga arketipe kebiasaan dengan derau normal, lihat [`lampiran/dataset.md`](../lampiran/dataset.md). Data ini dipakai agar seluruh alur sistem dapat diuji dan didemokan sebelum survei lapangan terkumpul. Seluruh angka pada laporan tahap ini dan tahap berikutnya akan diperbarui setelah data survei asli masuk; struktur variabel dan metode analisisnya tidak berubah.

---

## 2. Identifikasi Permasalahan Utama

Dari latar belakang di atas, masalah dapat dipecah menjadi lima butir yang lebih spesifik.

| Kode | Permasalahan | Akar masalah | Dampak |
|------|--------------|--------------|--------|
| **P-01** | Kebiasaan belajar tidak terukur | Tidak ada pencatatan harian; penilaian hanya berdasarkan ingatan | Mahasiswa tidak bisa membandingkan kondisi minggu ini dengan minggu lalu |
| **P-02** | Penilaian diri bersifat dikotomis | Hanya ada label "rajin/malas", tidak ada dimensi yang bisa diperbaiki | Saran perbaikan menjadi terlalu umum untuk dijalankan |
| **P-03** | Tidak ada acuan pembanding | Tidak ada data agregat kebiasaan mahasiswa lain | Mahasiswa tidak tahu apakah kondisinya sudah baik atau belum |
| **P-04** | Intervensi datang terlambat | Pembimbing hanya melihat hasil akhir (nilai), bukan proses harian | Mahasiswa baru diketahui bermasalah setelah nilainya turun |
| **P-05** | Saran yang diberikan tidak spesifik | Tidak ada analisis variabel mana yang paling menahan | Usaha perbaikan salah sasaran dan cepat berhenti |

**Pernyataan masalah (problem statement):**

> Mahasiswa tidak memiliki cara yang objektif dan terukur untuk mengetahui pola kebiasaan belajarnya, sehingga tidak dapat mengenali variabel mana yang perlu diperbaiki dan seberapa jauh kondisinya dari kebiasaan yang sehat.

---

## 3. Rumusan Masalah

1. Bagaimana mengubah kebiasaan belajar harian yang bersifat kualitatif menjadi variabel yang dapat diukur dan dibandingkan?
2. Bagaimana mengelompokkan pola kebiasaan belajar mahasiswa sehingga terbentuk tingkatan yang bermakna, bukan sekadar label "rajin/malas"?
3. Bagaimana menempatkan kebiasaan seorang mahasiswa ke dalam kelompok yang sudah terbentuk, sehingga ia tahu posisinya di antara mahasiswa lain?
4. Bagaimana menerjemahkan hasil pengelompokan itu menjadi saran perbaikan yang spesifik dan dapat dijalankan?

---

## 4. Solusi yang Diusulkan

**StudyTrack** — aplikasi pencatatan sesi belajar yang mengubah catatan harian menjadi enam variabel terukur, lalu mengelompokkannya dengan **K-Means clustering**.

### 4.1 Alur penyelesaian masalah

```
Catat sesi harian  →  Bentuk vektor 6 fitur  →  Standardisasi z-score
        ↓                                              ↓
  Riwayat & rekap                          K-Means (k=3) pada 90 responden
        ↓                                              ↓
  Posisi pengguna  ←  Tempatkan ke centroid terdekat  ←  Profil tiap cluster
        ↓
  Saran perbaikan yang spesifik
```

### 4.2 Cara solusi menjawab setiap masalah

| Masalah | Dijawab oleh | Bentuk konkret di aplikasi |
|---------|--------------|----------------------------|
| P-01 | Pencatatan sesi harian | Formulir sesi: tanggal, mata kuliah, jenis, durasi, fokus 1–5, menit main HP, tugas selesai, jam tidur, catatan |
| P-02 | Enam variabel terpisah | Setiap variabel ditampilkan sendiri-sendiri beserta selisihnya terhadap rata-rata kelompok |
| P-03 | Clustering 90 responden | Tiga kelompok terbentuk dari data, lalu posisi pengguna ditempatkan di antaranya |
| P-04 | Riwayat & proyeksi | Rekap 7/30 hari dan regresi linear atas empat pekan terakhir untuk memperkirakan pekan berikutnya |
| P-05 | Saran berbasis variabel | Perbandingan per variabel (mis. "HP 2,7 jam vs 1,1 jam rata-rata kelompok") dan catatan kontekstual |

### 4.3 Komponen Data Sains

Komponen utama yang dipakai adalah **clustering dengan algoritma K-Means**, dijalankan langsung di dalam aplikasi (bukan di notebook terpisah), dengan tahapan:

1. **Preprocessing** — enam fitur distandarkan *z-score* (`z = (x − μ) / σ`) agar jam, hari, dan jumlah tugas bisa dibandingkan.
2. **Inisialisasi** — *k-means++* dengan pembangkit acak ber-bibit tetap (bibit 42), sehingga hasil dapat diulang persis saat didemokan.
3. **Iterasi** — penetapan titik ke centroid terdekat dan pembaruan centroid, berhenti bila pergeseran < 1e-6 atau 300 iterasi.
4. **Evaluasi** — *silhouette score* untuk kualitas pemisahan dan *elbow method* untuk memilih jumlah cluster.
5. **Pelabelan** — cluster diberi peringkat memakai skor komposit berbobot (penggunaan HP sebagai fitur negatif), lalu dinamai **Kebiasaan Tinggi / Sedang / Perlu Ditingkatkan**.
6. **Penempatan** — vektor fitur pengguna distandarkan dengan μ dan σ dataset, lalu ditempatkan ke centroid terdekat.

Hasil pada dataset bawaan: **k = 3, silhouette = 0,355, SSE = 162, stabil dalam 5 iterasi**, dengan komposisi 30 / 28 / 32 responden.

### 4.4 Yang membedakan dari aplikasi pencatat biasa

- **Bukan sekadar *habit tracker*.** Aplikasi pencatat biasa berhenti pada grafik dan runtutan hari. StudyTrack melanjutkan sampai pengelompokan dan penempatan posisi.
- **Bukan demonstrasi model terpisah.** Komponen Data Sains melekat pada alur bisnis: hasil clustering dipakai untuk memberi label pada dasbor, bukan ditampilkan sebagai halaman terpisah yang hanya bisa dibuka saat presentasi.
- **Hasilnya dapat dipertanggungjawabkan.** Nilai silhouette, SSE, jumlah iterasi, dan grafik elbow ditampilkan terbuka agar kualitas pengelompokan bisa diperiksa, bukan hanya dipercaya.

---

## 5. Calon Pengguna Aplikasi

### 5.1 Pengguna utama — Mahasiswa

| Aspek | Keterangan |
|-------|------------|
| Peran | Pencatat sekaligus pembaca hasil analisis |
| Kondisi | Aktif kuliah, beban 5–7 mata kuliah, mengerjakan tugas sambil bekerja sampingan pada sebagian kasus |
| Kebiasaan digital | Terbiasa aplikasi ponsel; tidak sabar pada formulir panjang |
| Kebutuhan | Cara cepat mencatat sesi, gambaran pola yang mudah dibaca, saran yang bisa langsung dijalankan |
| Kendala | Malas mencatat bila prosesnya lebih dari satu menit; mudah berhenti bila tidak melihat kemajuan |
| Implikasi desain | Formulir satu layar dengan nilai bawaan, pencatatan selesai di bawah 30 detik, grafik dan ringkasan tampil lebih dulu sebelum tabel |

### 5.2 Pengguna sekunder — Dosen Pembimbing Akademik

| Aspek | Keterangan |
|-------|------------|
| Peran | Melihat gambaran kebiasaan belajar mahasiswa bimbingannya |
| Kebutuhan | Ringkasan kondisi per mahasiswa, penanda siapa yang perlu ditegur lebih awal |
| Kendala | Waktu terbatas; tidak mungkin memeriksa catatan satu per satu |
| Implikasi desain | Ringkasan per pekan dan label cluster yang bisa dibaca sekilas; laporan dapat dicetak menjadi PDF |

### 5.3 Pengguna tersier — Peneliti / pengelola data

| Aspek | Keterangan |
|-------|------------|
| Peran | Mengelola dataset responden yang menjadi dasar clustering |
| Kebutuhan | Impor CSV hasil survei, periksa statistik deskriptif, ekspor kembali untuk diolah di luar |
| Implikasi desain | Tab Dataset dengan pencarian, filter prodi, pengurutan kolom, impor CSV, ekspor CSV, dan reset ke data bawaan |

> Pada versi web saat ini, peran dosen dan peneliti belum dipisahkan dengan hak akses; keduanya memakai antarmuka yang sama. Pemisahan hak akses direncanakan pada versi final bersama basis data terpusat.

---

## 6. Manfaat Penerapan Data Sains

| Manfaat | Penjelasan | Bukti di aplikasi |
|---------|-----------|-------------------|
| **Objektivitas** | Penilaian tidak lagi bergantung pada ingatan, melainkan pada enam variabel yang tercatat | Statistik pekan dan riwayat sesi |
| **Segmentasi bermakna** | K-Means menemukan kelompok alami tanpa label awal, sehingga tingkatan yang terbentuk berasal dari data | Tiga cluster dengan profil dan porsi anggota |
| **Personalisasi saran** | Saran disusun dari selisih variabel pengguna terhadap rata-rata kelompoknya, bukan saran umum | Perbandingan per variabel + catatan kontekstual |
| **Deteksi dini** | Pola yang memburuk terlihat dari pekan ke pekan sebelum berdampak ke nilai | Rekap pekan + proyeksi regresi linear |
| **Dasar evaluasi program** | Porsi mahasiswa per cluster bisa dipakai prodi untuk menilai efektivitas program belajar | Ringkasan cluster pada tab Laporan |
| **Transparansi metode** | Kualitas pengelompokan terbuka untuk diperiksa, bukan kotak hitam | Silhouette, SSE, iterasi, grafik elbow |

Nilai tambah terpenting bukan pada kecanggihan algoritmanya — K-Means tergolong sederhana — melainkan pada **penempatan hasilnya di dalam alur kerja pengguna**: hasil clustering dipakai untuk memberi label pada dasbor, menentukan saran, dan menyusun laporan. Model yang sederhana tetapi terpakai dinilai lebih baik daripada model rumit yang hanya bisa dilihat di notebook.

---

## 7. Ruang Lingkup dan Batasan

**Termasuk dalam lingkup:**

- Pencatatan dan pengelolaan sesi belajar (tambah, sunting, hapus, ulangi)
- Perhitungan enam fitur dan pengelompokan K-Means dengan k = 2..5
- Visualisasi hasil: scatter, radar, batang profil, elbow, ring progres
- Penempatan posisi pengguna dan perbandingan dengan kelompoknya
- Pengelolaan dataset responden dengan impor/ekspor CSV
- Laporan pekanan, proyeksi, dan cetak PDF
- Penyimpanan lokal di peramban serta mode luring (PWA)

**Di luar lingkup (versi ini):**

- Autentikasi dan multi-pengguna pada satu server
- Sinkronisasi data antarperangkat
- Notifikasi/pengingat otomatis
- Integrasi dengan sistem akademik kampus (SIAKAD)
- Prediksi nilai akhir — aplikasi ini mengelompokkan kebiasaan, bukan memprediksi prestasi

---

## 8. Kesimpulan Tahap 1

Permasalahan yang diangkat bukan "mahasiswa kurang rajin", melainkan **tidak adanya alat ukur yang membuat kebiasaan belajar bisa dinilai dan diperbaiki secara terarah**. Solusi yang diusulkan adalah aplikasi yang mencatat sesi belajar, mengubahnya menjadi enam variabel terukur, lalu mengelompokkannya dengan K-Means sehingga setiap mahasiswa mengetahui posisinya dan variabel mana yang paling menahan.

Rumusan masalah pada bagian 3 menjadi dasar penyusunan kebutuhan sistem pada Tahap 2, dan keenam variabel pada bagian 4.3 menjadi dasar kebutuhan data.

---

### Keluaran tahap ini

- [x] Latar belakang permasalahan
- [x] Identifikasi permasalahan utama (P-01 … P-05)
- [x] Rumusan masalah
- [x] Solusi yang diusulkan beserta komponen Data Sains
- [x] Identifikasi calon pengguna aplikasi
- [x] Manfaat penerapan Data Sains
- [x] Ruang lingkup dan batasan

**Tahap berikutnya:** [Tahap 2 — Analisis Kebutuhan Sistem](tahap-2-analisis-kebutuhan.md)
