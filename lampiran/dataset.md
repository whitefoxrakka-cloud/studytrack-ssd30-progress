# Lampiran — Dataset

Berkas ini menjelaskan dataset yang dipakai sebagai dasar *clustering* pada aplikasi StudyTrack.

| | |
|---|---|
| Berkas | `data/survei.csv` (sumber baca: `assets/js/dataset.js`) |
| Jumlah baris | 90 responden |
| Jumlah kolom | 9 |
| Status | **Sintetis** — bukan hasil survei lapangan |
| Pembangkit | `tools/buat-dataset.mjs`, bibit tetap `20261121` |

---

## 1. Skema

| Kolom | Tipe | Keterangan | Contoh |
|-------|------|-----------|--------|
| `id` | string | Pengenal responden, unik | `R01` |
| `prodi` | string | Program studi | `Data Sains` |
| `angkatan` | integer | Tahun masuk | `2024` |
| `durasi` | decimal | Jam belajar per hari | `3.4` |
| `frekuensi` | integer | Hari belajar per minggu (0–7) | `5` |
| `tidur` | decimal | Jam tidur per hari | `7.2` |
| `tugas` | integer | Tugas selesai per minggu | `6` |
| `hp` | decimal | Jam main HP saat belajar per hari | `1.8` |
| `mandiri` | integer | Sesi belajar mandiri per minggu | `3` |

---

## 2. Cara dataset dibangkitkan

Dataset disusun dari **tiga arketipe kebiasaan**, masing-masing 30 responden, lalu diberi derau normal agar tidak membentuk kelompok yang sempurna:

| Arketipe | Durasi (jam) | Frekuensi (hari) | Tidur (jam) | Tugas | HP (jam) | Mandiri |
|----------|--------------|------------------|-------------|-------|----------|---------|
| Kebiasaan tinggi | ± 4,5 | ± 6 | ± 7,3 | ± 8 | ± 1,2 | ± 5 |
| Kebiasaan sedang | ± 2,6 | ± 4 | ± 6,4 | ± 6 | ± 2,7 | ± 3 |
| Kebiasaan rendah | ± 1,4 | ± 2 | ± 5,6 | ± 3 | ± 4,1 | ± 1 |

Derau ditambahkan dengan metode Box–Muller, dan seluruh proses memakai pembangkit acak ber-bibit sehingga hasilnya identik setiap kali dibangkitkan ulang.

**Mengapa diberi derau?** Bila ketiga kelompok dibangkitkan tanpa derau, K-Means akan mendapat cluster yang terlalu mudah dipisahkan dan silhouette mendekati 1. Angka itu tidak realistis dan tidak menguji algoritma. Dengan derau, batas antarkelompok menjadi kabur seperti data lapangan sesungguhnya.

---

## 3. Statistik deskriptif

Dihitung langsung dari 90 baris dataset bawaan:

| Fitur | Satuan | Rata-rata | Simpangan baku | Min | Maks |
|-------|--------|-----------|----------------|-----|------|
| Durasi belajar | jam/hari | 2,84 | 1,53 | 0,4 | 6,2 |
| Frekuensi belajar | hari/minggu | 4,16 | 1,64 | 1 | 7 |
| Durasi tidur | jam/hari | 6,49 | 0,99 | 4,2 | 8,5 |
| Tugas selesai | tugas/minggu | 5,71 | 2,91 | 0 | 11 |
| HP saat belajar | jam/hari | 2,67 | 1,46 | 0,1 | 6,2 |
| Belajar mandiri | sesi/minggu | 3,09 | 1,82 | 0 | 7 |

**Sebaran program studi:**

| Prodi | Jumlah |
|-------|--------|
| Data Sains | 22 |
| Informatika | 21 |
| Matematika | 19 |
| Statistika | 14 |
| Sistem Informasi | 14 |

**Sebaran angkatan:**

| Angkatan | Jumlah |
|----------|--------|
| 2022 | 20 |
| 2023 | 23 |
| 2024 | 15 |
| 2025 | 32 |

---

## 4. Hasil clustering pada dataset ini

| Parameter | Nilai |
|-----------|-------|
| Jumlah cluster (k) | 3 |
| Silhouette score | 0,355 |
| SSE | 162 |
| Iterasi sampai stabil | 5 |

| Cluster | Anggota | Porsi | Durasi | Tidur | HP |
|---------|---------|-------|--------|-------|-----|
| Kebiasaan Tinggi | 30 | 33% | 4,7 jam/hari | 7,4 jam | 1,1 jam |
| Kebiasaan Sedang | 28 | 31% | 2,6 jam/hari | 6,4 jam | 2,7 jam |
| Perlu Ditingkatkan | 32 | 36% | 1,4 jam/hari | 5,7 jam | 4,1 jam |

Silhouette 0,355 berarti cluster terpisah dengan cukup baik (di atas ambang 0,25) namun tidak terlalu sempurna — konsisten dengan data yang diberi derau.

---

## 5. Mengganti dengan data survei asli

1. Susun kuesioner dengan pertanyaan yang memetakan langsung ke enam variabel.
2. Ekspor jawaban ke CSV dengan nama kolom **persis** seperti skema di bagian 1.
3. Buka aplikasi → tab **Dataset** → **Impor CSV**.
4. Validasi otomatis: enam kolom wajib harus ada dan minimal 10 baris.
5. Setelah impor, statistik deskriptif, clustering, dasbor, dan laporan otomatis dihitung ulang.

**Alternatif (mengganti data bawaan):** timpa `data/survei.csv`, sesuaikan sumber pada `tools/buat-dataset.mjs`, lalu jalankan:

```bash
node tools/buat-dataset.mjs
```

---

## 6. Etika dan keterbatasan

- Data saat ini **sintetis** dan **tidak mewakili populasi nyata**. Angka apa pun dari dataset ini tidak boleh dipakai sebagai klaim penelitian.
- Saat survei asli dilakukan, responden harus memberi persetujuan (informed consent) dan data disimpan tanpa nama (cukup ID dan prodi).
- Ukuran sampel 90 responden hanya cukup untuk menggambarkan kecenderungan, bukan untuk generalisasi tingkat prodi atau fakultas.
