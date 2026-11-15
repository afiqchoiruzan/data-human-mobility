# Naskah Video 5 Menit — Human Mobility JogjaPulse
Target: 35–37 detik per orang (±95 kata, kecepatan bicara santai). Tinggal disesuaikan dengan lidah masing-masing.
Urutan sesuai pembagian tugas (Anggota 1–8).

---

## 1. Anggota 1 — Ritme 24 Jam
Halo semuanya, kami dari kelompok Human Mobility. Dataset yang kami pakai namanya JogjaPulse, yaitu data lokasi anonim di Yogyakarta dari Desember 2021 sampai April 2022. Aku bagian ritme harian. Kalau dilihat per jam, Sleman paling ramai, puncaknya jam 12 siang lalu naik lagi sekitar jam 7 malam. Semua wilayah paling sepi di jam 3 sampai 4 pagi. Rasio siang banding malam tertinggi ada di Kulon Progo, sekitar 2,3 kali. Yang terendah Kota Yogyakarta, 1,4 kali, karena malam hari di pusat kota tetap hidup.

## 2. Anggota 2 — Hari Kerja vs Akhir Pekan
Lanjut ke pola mingguan. Lima kapanewon terpadat adalah Depok, Ngaglik, Banguntapan, Gamping, dan Kasihan, yang kebanyakan kawasan kampus dan perkantoran. Hampir di semua kapanewon utama, jumlah perangkat di hari kerja lebih tinggi daripada Sabtu dan Minggu. Dari heatmap hari dan jam, puncak aktivitas ada di Senin sampai Jumat, sekitar jam 11 siang sampai jam 8 malam. Kalau akhir pekan, paginya lebih pelan, aktivitas baru naik belakangan dibanding hari kerja, dan secara keseluruhan lebih landai.

## 3. Anggota 3 (Aufa) — Tren 151 Hari & Ramadhan
Aku bagian tren selama 151 hari. Di grafik harian, aktivitas tinggi dari Desember sampai pertengahan Februari, dan sempat turun waktu Tahun Baru. Lalu sekitar 16 Februari, angkanya anjlok tajam. Ini kemungkinan besar karena jumlah sampel datanya berkurang, bukan karena orang tiba-tiba berhenti bergerak. Terus saat Ramadhan, kalau kita bandingkan bentuk kurvanya, porsi aktivitas jam 3 sampai 4 pagi naik sekitar dua kali lipat, kemungkinan karena sahur. Sementara jam 5 sore dan jam 7 malam sedikit lebih rendah dibanding bulan normal.

## 4. Anggota 4 — Intensitas Sinyal
Aku membahas intensitas sinyal GPS, yaitu seberapa sering satu perangkat mengirim lokasi per jam. Jumlah perangkat dan jumlah sinyal punya hubungan linear yang kuat di seluruh kapanewon. Rata-rata ping per perangkat paling tinggi di Yogyakarta, 2,65, dan Sleman, 2,64. Bantul paling rendah, 2,50, tapi selisihnya kecil. Pada jam sibuk, yaitu jam 8 pagi sampai 5 sore, mediannya sedikit lebih tinggi. Artinya perangkat lebih sering mengirim sinyal saat orang banyak bergerak, dan pola ini konsisten di kelima kabupaten dan kota.

## 5. Anggota 5 — Matriks OD Kabupaten
Sekarang masuk ke data kedua, yaitu pergerakan dari tempat tinggal ke tujuan di siang hari. Ternyata sebagian besar perjalanan terjadi di dalam kabupaten yang sama, sekitar 63 sampai 74 persen. Yang terbesar adalah intra-Sleman, lebih dari 230 ribu, lalu intra-Bantul. Kalau lintas kabupaten, arus terbesar dari Sleman ke Kota Yogyakarta, sekitar 38 ribu. Jadi kebanyakan orang Jogja beraktivitas tidak jauh dari tempat tinggalnya, dan perjalanan lintas kabupaten paling banyak mengarah ke pusat kota.

## 6. Anggota 6 — Koridor Komuter
Aku bahas rute komuter antar-kapanewon. Rute tersibuk adalah Ngaglik ke Depok, dengan volume lebih dari 3.600 perangkat. Disusul Banguntapan ke Umbulharjo dan Ngaglik ke Pakem. Dari 20 rute teratas, banyak yang bolak-balik di sekitar Depok. Depok juga nomor satu, baik sebagai asal maupun tujuan, sekitar 32 ribu keluar dan 29 ribu masuk. Banguntapan, Ngaglik, dan Gamping punya peran ganda, yaitu sebagai kawasan hunian sekaligus tujuan aktivitas.

## 7. Anggota 7 — Jaringan Graf
Aku memodelkan pergerakan ini sebagai graf berarah memakai NetworkX, di mana kapanewon jadi simpul dan jumlah perangkat jadi bobot garis. Dari skor PageRank, Depok paling tinggi, yaitu 0,064, jadi bisa dibilang Depok adalah pusat gravitasi pergerakan di DIY. Urutan berikutnya Banguntapan 0,045 dan Ngaglik 0,041, lalu Umbulharjo dan Gamping. Di visualisasi graf juga kelihatan panah timbal balik yang padat di sekitar Depok dan Ngaglik, jadi arusnya memang dua arah.

## 8. Anggota 8 — Kualitas Data & Penutup
Terakhir, soal kualitas data. Volume aliran bulanan turun bertahap dari Desember ke Februari, lalu jatuh tajam di Maret dan April. Itu bertepatan dengan penanda reduced_quality, di mana jumlah rute aktif dan rata-rata perangkat per rute menyusut drastis. Jadi tren Maret sampai April harus dibaca hati-hati. Kesimpulannya, aktivitas DIY terpusat di Sleman dan koridor Depok, Ngaglik, Banguntapan, dan Depok menjadi pusat jaringannya. Terima kasih sudah menonton.
