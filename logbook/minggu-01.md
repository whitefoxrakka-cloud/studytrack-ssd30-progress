# LOGBOOK PEKAN 1 — 16 s.d. 22 November 2026

**Fokus pekan:** Tahap 1 (identifikasi masalah), Tahap 2 (analisis kebutuhan), dan versi web pertama
**Tahap proyek:** 1 dan 2 selesai, Tahap 5 dimulai lebih awal (versi web)
**Keluaran:** dua dokumen laporan, aplikasi web berjalan, repositori kode dan repositori dokumen

---

## 1. Rekap pekan

| Anggota | Fokus pekan ini | FR | Keluaran | Jam |
|:-------:|-----------------|----|----------|:---:|
| Yuniar Zahra Wiyani | Latar belakang, identifikasi masalah, modul pencatatan sesi | FR-01, FR-02 | Bab I bagian masalah; `vJurnal`, `formSesi` | 6 |
| Aninda Rizqi Amelia | Rumusan masalah, tujuan, dasbor, laporan | FR-03, FR-08 | Bab I bagian tujuan; `vDasbor`, `vLaporan` | 6 |
| Maheswari Pasa Putri Syamsudar | Metode K-Means, mesin clustering, grafik | FR-04, FR-05 | `kmeans.js`, `grafik.js`, `vAnalisis` | 9 |
| Hasan | Dataset 90 responden, pengelolaan data | FR-06, FR-07 | `dataset.js`, `survei.csv`, `vDataset`, `imporCsv` | 7 |
| Sifa Sabrina | NFR, proses bisnis, animasi, onboarding, saran | FR-09, FR-10, FR-11 | Bab II bagian NFR; `animasi.js`, `bukaKenalan`, `wawasan` | 7 |

## 2. Rincian harian

### 2.1 Yuniar Zahra Wiyani — 60124004 · FR-01, FR-02

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 17 Nov | Menulis latar belakang dari 12 keluhan yang terkumpul pekan lalu | Draf 900 kata | `laporan/tahap-1` §2 |
| 18 Nov | Merumuskan lima masalah turunan (P-01…P-05) beserta akar masalahnya | Tabel P-01…P-05 | `laporan/tahap-1` §3 |
| 19 Nov | Menyusun pernyataan masalah dan empat rumusan masalah | Draf rumusan | `laporan/tahap-1` §4 |
| 20 Nov | Membangun formulir pencatatan sesi: tanggal, durasi, jenis | `formSesi()` | commit `9d5ac4d` |
| 21 Nov | Menambahkan validasi (durasi 1–1440 menit, tanggal tidak melebihi hari ini) dan riwayat sesi | `vJurnal()`, `csvSesi()` | commit `9d5ac4d` |

**Keputusan yang diambil.** Validasi diletakkan **sebelum** penyimpanan, bukan sesudah. Alasannya
muncul saat pengujian: satu salah ketik "240" pada kolom durasi (maksudnya 240 menit, tertulis 240 jam)
menggeser seluruh centroid. Setelah validasi dipindah ke depan, data cacat tidak pernah masuk state.

**Kendala.** Konfirmasi hapus sempat memakai `confirm()` bawaan peramban yang tampilannya berbeda di
tiap peramban. Diganti lembar bawah agar seragam.

### 2.2 Aninda Rizqi Amelia — 60124009 · FR-03, FR-08

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 17 Nov | Menyusun tujuan dan manfaat (bagi mahasiswa, dosen PA, pengelola data) | Draf 4 butir manfaat | `laporan/tahap-1` §6 |
| 18 Nov | Menulis gambaran solusi aplikasi dan batas ruang lingkup | Draf ruang lingkup | `laporan/tahap-1` §7 |
| 19 Nov | Merancang dasbor: urutan kartu, pemilihan angka utama | Sketsa dasbor | Catatan rancangan |
| 20 Nov | Membangun ringkasan pekan dan kartu statistik | `vDasbor()`, `stat()` | commit `9d5ac4d` |
| 21 Nov | Membangun tab laporan: rekap pekan, proyeksi, tombol cetak | `vLaporan()`, `K.regresi()` | commit `9d5ac4d` |

**Keputusan yang diambil.** Laporan **tidak menghitung ulang** apa pun; ia membaca hasil yang sama
dengan dasbor. Sempat ada versi yang menghitung sendiri, dan hasilnya berbeda 0,4 jam dari dasbor
karena pembulatan dilakukan di dua tempat.

**Kendala.** Regresi dengan satu titik data menghasilkan kemiringan `NaN`. Ditangani dengan menyatakan
bahwa proyeksi belum dapat dihitung, bukan menampilkan garis datar.

### 2.3 Maheswari Pasa Putri Syamsudar — 60124010 · FR-04, FR-05

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 17 Nov | Menulis ulang metode: standardisasi, k-means++, kriteria berhenti | `docs/METODE.md` | commit `9d5ac4d` |
| 18 Nov | Mengimplementasikan standardisasi z-score dan k-means++ dengan bibit tetap | `standardisasi()`, `kmeans()` | commit `9d5ac4d` |
| 19 Nov | Menambahkan penanganan centroid kosong | Cabang pemulihan di `kmeans()` | commit `9d5ac4d` |
| 20 Nov | Mengimplementasikan silhouette dan elbow | `silhouette()`, `elbow()` | commit `9d5ac4d` |
| 21 Nov | Membangun empat grafik SVG: scatter, radar, batang, elbow | `grafik.js` | commit `9d5ac4d` |

**Keputusan yang diambil.** Bibit acak dikunci pada angka 42. Tanpa itu, dua kali menjalankan analisis
pada data yang sama bisa memberi cluster berbeda, dan demonstrasi di kelas tidak akan cocok dengan
angka di laporan.

**Kendala.** Centroid bisa kosong ketika semua anggota berpindah ke centroid lain, sehingga pembagian
rata-rata menjadi `0/0` dan menghasilkan `NaN` yang menyebar ke seluruh hasil. Ditangani dengan
memindahkan centroid tersebut ke titik terjauh — cara yang menjaga jumlah cluster tanpa menambah `k`.

### 2.4 Hasan — 60124013 · FR-06, FR-07

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 17 Nov | Merancang skema dataset: 6 fitur, 3 atribut identitas | Skema 9 kolom | `lampiran/dataset.md` |
| 18 Nov | Membangkitkan 90 responden sintetis dari 3 arketipe (tinggi, sedang, rendah) | `survei.csv`, `dataset.js` | commit `9d5ac4d` |
| 19 Nov | Membangun tabel dataset: cari, filter prodi, urut kolom, hapus baris | `vDataset()` | commit `9d5ac4d` |
| 20 Nov | Membangun impor CSV dengan validasi header dan jumlah baris | `imporCsv()` | commit `9d5ac4d` |
| 21 Nov | Membangun penempatan posisi pengguna ke centroid terdekat | `K.tempatkan()` | commit `9d5ac4d` |

**Keputusan yang diambil.** Data acuan (90 responden) dipisahkan dari data pribadi (sesi belajar).
Sempat digabung dalam satu array, dan akibatnya tombol "hapus semua sesi" ikut menghapus dataset —
kesalahan yang langsung diperbaiki.

**Catatan jujur.** Dataset **sintetis**, dibangkitkan dengan bibit tetap dari tiga arketipe. Ini
disebutkan terbuka di laporan dan tidak diklaim sebagai hasil survei lapangan. Alasannya: kelompok
belum menyebar kuesioner sungguhan dalam waktu yang tersedia, dan data karangan yang disamarkan
sebagai data nyata akan merusak seluruh kesimpulan.

### 2.5 Sifa Sabrina — 60124023 · FR-09, FR-10, FR-11

| Tanggal | Kegiatan | Keluaran | Bukti |
|---------|----------|----------|-------|
| 17 Nov | Menyusun 17 NFR dengan tolok ukur yang dapat diuji | Tabel NFR-01…NFR-17 | `laporan/tahap-2` §5 |
| 18 Nov | Menggambar empat alur proses bisnis | Diagram Mermaid | `laporan/tahap-2` §6 |
| 19 Nov | Membangun lembar pengaturan (nama, target, k, tema) | `bukaAtur()` | commit `c00fbb0` |
| 20 Nov | Membangun panduan tiga langkah dan penanda `sudahKenal` | `bukaKenalan()` | commit `c00fbb0` |
| 21 Nov | Membangun aturan saran berprioritas dan gelembung Nora | `wawasan()` | commit `c00fbb0` |

**Keputusan yang diambil.** Aturan saran dijalankan **berurutan dan berhenti pada yang pertama cocok**,
bukan menampilkan semua. Tidur diperiksa lebih dulu karena menyarankan "perbanyak belajar" kepada orang
yang tidur lima jam justru memperburuk keadaannya.

**Kendala.** Panduan sempat muncul setiap muat ulang karena penanda tidak tersimpan. Diperbaiki dengan
menyimpan `sudahKenal` di preferensi.

## 3. Keluaran pekan

| No | Keluaran | Berkas / bukti |
|:--:|----------|----------------|
| 1 | Laporan Tahap 1 — identifikasi masalah | `laporan/tahap-1-identifikasi-masalah.md` (commit `f8f454a`) |
| 2 | Laporan Tahap 2 — analisis kebutuhan (11 FR, 17 NFR) | `laporan/tahap-2-analisis-kebutuhan.md` (commit `f8f454a`) |
| 3 | Lampiran dataset dan statistik deskriptif | `lampiran/dataset.md` (commit `f8f454a`) |
| 4 | Mesin K-Means yang dapat diuji | `assets/js/kmeans.js` (commit `9d5ac4d`) |
| 5 | Delapan uji unit, semuanya lulus | `tests/kmeans.test.mjs` |
| 6 | Aplikasi web berjalan dan terpasang di GitHub Pages | commit `9d5ac4d`, `296ab56` |
| 7 | Sistem desain dan animasi | commit `c00fbb0`, `0361dcc` |
| 8 | Identitas kelompok dan penanggung jawab FR | commit `d0b6498` |

**Angka yang terukur pada akhir pekan ini:**

| Ukuran | Hasil | Cara memperoleh |
|--------|-------|-----------------|
| Waktu analisis K-Means (90 baris, k = 3) | ± 11 ms | 30 kali jalan di Node, dirata-rata |
| Silhouette pada dataset acuan | 0,355 | keluaran `analisis()` |
| Ukuran muat awal | 148 KB | jumlah ukuran aset inti |
| Uji unit | 8/8 lulus | `node --test tests/kmeans.test.mjs` |

## 4. Kendala pekan ini

| Kendala | Dampak | Penyelesaian |
|---------|--------|--------------|
| Centroid kosong menghasilkan `NaN` | Seluruh hasil analisis rusak | Pemulihan dengan memindahkan centroid ke titik terjauh |
| Dataset dan sesi pribadi tercampur | Hapus riwayat ikut menghapus dataset | Dipisah menjadi dua koleksi |
| Angka dasbor dan laporan berbeda 0,4 jam | Laporan tidak dapat dipercaya | Satu sumber perhitungan untuk keduanya |
| Panduan muncul berulang | Mengganggu | Penanda `sudahKenal` disimpan |
| Nomor FR berbeda antara README dan laporan | Rujukan silang menjadi kacau | Penomoran diseragamkan ke dokumen Tahap 2 (commit `3f81cec`) |

## 5. Rencana pekan berikutnya

| Anggota | Rencana | Diagram |
|:-------:|---------|---------|
| Yuniar | Use case diagram (kolaboratif), AD-01, SD-01 | AD-01, SD-01 |
| Aninda | AD-02, SD-02, Bab IV bagian antarmuka | AD-02, SD-02 |
| Maheswari | Class diagram (kolaboratif), AD-03, SD-03 | AD-03, SD-03 |
| Hasan | ERD dan DDL basis data, AD-04, SD-04 | AD-04, SD-04 |
| Sifa | Rancangan antarmuka, AD-05, SD-05, PPT | AD-05, SD-05 |
