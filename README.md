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
5. **Bagian 5 — Matriks OD Makro Antar-Kabupaten/Kota:** Heatmap matriks OD 5×5 serta proporsi pergerakan *intra-kabupaten* vs *lintas-kabupaten* (*inter-regency*).
6. **Bagian 6 — Koridor Komuter Mikro Lintas-Kapanewon:** Identifikasi 20 rute komuter lintas-kapanewon tersibuk serta 10 Kapanewon pengirim dan penerima komuter terbesar.
7. **Bagian 7 — Pemodelan Jaringan Graf (Network Centrality):** Pemodelan *directed weighted graph* (`networkx`) 78 Kapanewon menggunakan metrik *Weighted In-Degree*, *Weighted Out-Degree*, dan *PageRank Centrality*.
8. **Bagian 8 — Tren OD Bulanan & Evaluasi Kualitas Data (`reduced_quality`):** Tren aliran kunjungan bulanan (`2021-12` s.d. `2022-04`) dan evaluasi dampak penurunan kualitas data pada periode Maret–April 2022.

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
