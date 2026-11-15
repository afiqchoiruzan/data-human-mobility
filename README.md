# Analisis Pola Mobilitas Manusia di D.I. Yogyakarta (JogjaPulse)

Repository ini berisi analisis spasial-temporal dan pemodelan jaringan *Origin-Destination* (OD) mobilitas masyarakat di Daerah Istimewa Yogyakarta (78 Kapanewon / 5 Kabupaten–Kota) menggunakan dataset **JogjaPulse** selama 151 hari (**1 Desember 2021 – 30 April 2022**).

Proyek ini disusun untuk memenuhi tugas **Rekayasa Data (08.1 Group Project: Human Mobility)**.

---

## Sumber Dataset

Dataset berasal dari **JogjaPulse** ([Zenodo Record 23157460](https://zenodo.org/records/23157460)) yang mencakup dua tabel utama:
1. **`presence_kapanewon_hourly.csv`** — Data kehadiran perangkat unik (`n_maids`) dan total sinyal GPS (`n_pings`) per jam di 78 Kapanewon dan 5 Kabupaten/Kota.
2. **`od_home_visits_kapanewon_monthly.csv`** — Matriks aliran perjalanan *Origin-Destination* (OD) bulanan dari lokasi tempat tinggal ke lokasi kunjungan siang hari (`08:00–17:59 WIB`) beserta penanda kualitas data (`reduced_quality`).

---

## Ruang Lingkup Analisis (8 Bagian)

Seluruh tahapan pengolahan, analisis, dan visualisasi diimplementasikan di dalam notebook `Human_Mobility_JogjaPulse_Lengkap.ipynb`:

### A. Dinamika Kehadiran Temporal & Intensitas Sinyal (`presence_kapanewon_hourly.csv`)
1. **Bagian 1 — Ritme Sirkadian 24 Jam & Jam Puncak:** Kurva kehadiran perangkat per jam (`0–23 WIB`) dan rasio aktivitas siang (`08:00–16:00`) vs malam (`00:00–05:00`) antar Kabupaten/Kota.
2. **Bagian 2 — Komparasi Hari Kerja vs Akhir Pekan:** Perbandingan 15 Kapanewon terpadat pada *weekday* vs *weekend* serta heatmap aktivitas mingguan (7 hari × 24 jam).
3. **Bagian 3 — Tren Longitudinal 151 Hari & Pergeseran Ramadhan:** Dinamika kehadiran harian selama 151 hari, anomali libur Tahun Baru 2022, dan pergeseran jam aktif selama Ramadhan 1443 H (April 2022).
4. **Bagian 4 — Intensitas Sinyal GPS (`pings_per_maid`):** Analisis rasio pengiriman sinyal per perangkat antar Kabupaten/Kota serta komparasi jam sibuk (`08:00–17:00`) vs luar jam sibuk.

### B. Aliran Origin-Destination (OD) & Pemodelan Graf (`od_home_visits_kapanewon_monthly.csv`)
5. **Bagian 5 — Matriks OD Makro Antar-Kabupaten/Kota:** Heatmap matriks OD 5×5 serta proporsi hitungan OD intra-kabupaten/kota vs lintas kabupaten/kota pada Desember 2021–Februari 2022.
6. **Bagian 6 — Pasangan OD Mikro Lintas-Kapanewon:** Top 20 pasangan OD serta Top 10 wilayah asal dan tujuan lintas-kapanewon pada Desember 2021–Februari 2022, dengan 78 wilayah terdisambiguasi.
7. **Bagian 7 — Pemodelan Jaringan Graf (Network Centrality):** Graf berarah berbobot (`networkx`) tepat 78 kapanewon tanpa *self-loop* pada Desember 2021–Februari 2022. Weighted In-Degree, Weighted Out-Degree, dan PageRank dihitung dari graf lengkap; visualisasi jaringan menampilkan 15 koridor utama.
8. **Bagian 8 — Tren OD Bulanan & Evaluasi Kualitas Data (`reduced_quality`):** Tren aliran kunjungan bulanan (`2021-12` s.d. `2022-04`) dan evaluasi dampak penurunan kualitas data pada periode Maret–April 2022 yang dinormalisasi per bulan.

`n_maids` menghitung perangkat berbeda untuk satu pasangan OD dalam satu bulan; lokasi tujuan adalah lokasi siang hari yang teramati. Grafik bagian 5–7 menjumlahkan hitungan tersebut selama tiga bulan.

---

## Catatan Metodologis & Temuan Utama (Tervalidasi)

Analisis di dalam notebook menerapkan kontrol kualitas data berikut untuk mencegah *false insight*:
1. **Disambiguasi 78 Wilayah (`JETIS`):** Memisahkan **Kapanewon Jetis, Bantul (`34.02.09`)** dan **Kemantren Jetis, Kota Yogyakarta (`34.71.02`)** sehingga graf tetap berjumlah tepat **78 simpul** dengan **0 *self-loop***. Keduanya tidak masuk Top 10 wilayah tujuan periode utama; Ngemplak menempati peringkat ke-10 dengan 11.612 hitungan perangkat-bulanan.
2. **Penanganan *Survivorship Bias* & *Outlier Centroid* (Bagian 1):** Rekonstruksi grid penuh (`78 kapanewon × 151 hari × 24 jam`, *zero-filled*) terhadap sensor $k$-anonymity (`n_maids < 5`) dan penggunaan median pada kurva sirkadian menghasilkan rasio siang/malam yang bebas bias: Gunungkidul (`4,03x`), Kulon Progo (`3,28x`), Bantul (`2,58x`), Sleman (`2,40x`), dan Kota Yogyakarta (`1,80x`).
3. **Normalisasi Proporsi Jam Ramadhan (Bagian 3):** Penurunan volume harian sejak `16 Februari 2022` merupakan penyusutan cakupan sampel data. Setelah dinormalisasi ke proporsi harian per jam (`%`), Ramadhan (Apr 2022) menunjukkan lonjakan aktivitas Sahur (`03:00–04:00 WIB`) dari `1,44%–1,67%` menjadi `3,48%–3,98%` serta penurunan singkat pada jam berbuka (`17:00 WIB`, `4,77%`) dan Tarawih (`19:00 WIB`, `4,80%`).
4. **Rasio Tertimbang & Periode OD (Bagian 4–7):** Intensitas sinyal tertimbang (`total_pings / total_maids`) tertinggi berada di Kota Yogyakarta (`2,84`) dan Sleman (`2,73`). Periode utama OD adalah Desember 2021–Februari 2022. Maret–April berstatus `reduced_quality` dan tetap dianalisis di bagian 8. Februari tidak ditandai reduced_quality, tetapi cakupan perangkat mulai turun pada 16 Februari. Penjumlahan `n_maids` antarbulan adalah akumulasi hitungan perangkat-bulanan, bukan jumlah perjalanan atau perangkat unik sepanjang periode. Proporsi intra-kabupaten mencakup pasangan dalam kapanewon yang sama maupun berbeda, dan tidak membuktikan perangkat diam. Lokasi tujuan siang hari tidak menentukan tujuan bekerja/kuliah; total sisi asal dan tujuan tidak digunakan untuk menyatakan arus bersih.
5. **Normalisasi Durasi `reduced_quality` (Bagian 8):** Pada Maret–April 2022 (2 bulan vs 3 bulan periode utama), rata-rata pasangan OD terpublikasi turun dari `2.624` menjadi `1.011` pasangan/bulan (`-61,5%`) dan rata-rata `n_maids` per baris OD bulanan turun dari `74,9` menjadi `26,0` (`-65,3%`). Pasangan yang tidak muncul dapat tersupresi dan tidak otomatis nol; penurunan angka mentah tidak cukup untuk menyimpulkan penurunan mobilitas masyarakat.

---

## Struktur Repository

```text
├── data/
│   ├── presence_kapanewon_hourly.csv          # Dataset kehadiran per jam (Zenodo)
│   └── od_home_visits_kapanewon_monthly.csv   # Dataset Origin-Destination bulanan (Zenodo)
├── figures/                                   # Output 16 grafik beresolusi tinggi (300 DPI)
├── Human_Mobility_JogjaPulse_Lengkap.ipynb    # Notebook analisis lengkap (Bagian 1–8)
├── requirements.txt                           # Daftar dependensi pustaka Python
├── .gitignore                                 # Daftar file yang diabaikan Git
└── README.md                                  # Dokumentasi utama proyek
```

---

## Cara Menjalankan

1. **Clone repository ini:**
   ```bash
   git clone https://github.com/afiqchoiruzan/data-human-mobility.git
   cd data-human-mobility
   ```

2. **Instal pustaka Python yang dibutuhkan:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Siapkan dataset:**
   Pastikan file `presence_kapanewon_hourly.csv` dan `od_home_visits_kapanewon_monthly.csv` dari [Zenodo Record 23157460](https://zenodo.org/records/23157460) berada di dalam folder `data/`.

4. **Jalankan Jupyter Notebook:**
   ```bash
   jupyter notebook Human_Mobility_JogjaPulse_Lengkap.ipynb
   ```
   Seluruh grafik hasil eksekusi akan otomatis tersimpan ke dalam folder `figures/`.
