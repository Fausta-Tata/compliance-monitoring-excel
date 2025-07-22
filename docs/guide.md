## Analisis Pemantauan Kepatuhan

Dataset: dummy data fiktif  
Periode: 2023 - 2025  
Tools: Microsoft Excel Office 2019  
Tahapan: Cleaning, Pivot Table, Dashboard(Visualization)  

### 1. Tahap Cleaning  
Proses data dimulai dengan pembersihan dan persiapan untuk memastikan akurasi dan konsistensi sebelum dianalisis. Langkah-langkah utamanya adalah sebagai berikut:

#### A. Pemuatan & Penggabungan Data:
Data mentah dari beberapa file .csv diambil dan digabungkan secara otomatis menggunakan Power Query (From Folder). Proses ini juga mencakup pemfilteran untuk memastikan hanya file dengan ekstensi .csv yang diproses dan menggabungkan header yang relevan.

#### B. Pembersihan & Transformasi Data:
- Duplikasi Data: Duplikasi data dihilangkan berdasarkan kolom unik ID_Pesanan untuk memastikan setiap transaksi hanya dihitung satu kali.
- Standarisasi Kurir: Inkonsistensi nama kurir (misalnya, "JNE" vs. "JNE Express" dan "Sicepat" vs. "SiCepat") distandarkan menggunakan tabel referensi (kamus data) dan fungsi VLOOKUP.
- Penanganan Data Kosong: Nilai yang kosong (null) pada kolom-kolom penting seperti Kurir dan Status Pesanan ditangani dengan memberikan label yang jelas (misal: "Kurir Tidak Diisi"), mengubahnya dari data hilang menjadi sebuah kategori yang bisa dianalisis.

#### C. Pembuatan Kolom Analisis (Feature Engineering)
Beberapa kolom baru dibuat untuk memfasilitasi analisis kepatuhan berdasarkan aturan bisnis yang telah ditetapkan:
- Waktu Proses Pengiriman: Dibuat kolom baru Waktu_Proses (Hari) dengan menghitung selisih antara Tgl_Diserahkan_Kurir dan Tgl_Pembayaran.
- Status Kepatuhan Waktu: Dibuat kolom status berdasarkan SLA 5 hari. Pesanan dengan Waktu_Proses lebih dari 5 hari diberi label "Tidak Patuh". Pesanan dengan data tanggal tidak lengkap diberi label "Data Tidak Lengkap".
- Status Validitas Resi: Dibuat kolom status berdasarkan aturan: panjang 11 karakter dan diawali "RESI". Resi yang tidak memenuhi syarat diberi label "Tidak Valid".
- Status Kelengkapan Tgl Pembayaran, Tgl Diserahkan Kurir dan Kurir: Dibuat kolom untuk memberi label pada baris yang memiliki nilai null atau " ".
- Status Kebersihan Data (Final): Dibuat satu kolom kesimpulan Status_Kebersihan_Data. Sebuah baris data diberi label "Data Tidak Bersih" jika salah satu dari kolom status sebelumnya menunjukkan adanya masalah (misalnya "Tidak Patuh", "Tidak Valid", atau "Data Tidak Lengkap").

### 2. Tahap Analisis (Pivot Table)
Setelah data bersih, beberapa PivotTable dibuat untuk mengagregasi dan meringkas data guna menjawab pertanyaan bisnis utama. Analisis utama yang dilakukan adalah:
- Mengukur Kualitas Data Keseluruhan:
Dibuat PivotTable untuk menghitung jumlah (Count) pesanan berdasarkan Status_Kebersihan_Data. Tujuannya adalah untuk mendapatkan distribusi keseluruhan data yang "Bersih" versus "Tidak Bersih" dan memahami skala masalah kualitas data.
- Menganalisis Kepatuhan Waktu per Kurir:
Dibuat PivotTable untuk menghitung jumlah status kepatuhan waktu untuk setiap kurir. Tujuannya adalah untuk mengidentifikasi apakah ada kurir tertentu yang lebih sering terlibat dalam keterlambatan proses.
- Mengukur Validitas Nomor Resi:
Dibuat PivotTable untuk menghitung jumlah (Count) nomor resi berdasarkan statusnya ("Valid", "Tidak Valid"). Tujuannya adalah untuk mengetahui persentase data resi yang bermasalah dan berisiko bagi pengalaman pelanggan.
- Membandingkan Kinerja Kecepatan Kurir:
Dibuat PivotTable untuk menghitung rata-rata (Average) dari Waktu_Diserahkan_Kurir(Hari) untuk setiap kurir. Tujuannya adalah untuk membandingkan kecepatan proses internal sebelum paket diserahkan ke masing-masing kurir.


### 3. Tahap Visualisasi (Dashboard)  

Hasil dari PivotTable kemudian divisualisasikan dalam sebuah dashboard interaktif untuk memudahkan pemahaman. Komponen utama dashboard terdiri dari:

- Scorecards: untuk menampilkan total data yang digunakan.
- Grafik Donut: digunakan pada hasil validasi resi dan distribusi data.
- Grafik Batang: digunakan pada perhitungan rata rata waktu pada setiap kurir.
- Grafik Bar: digunakan pada kepatuhan waktu setiap kurir.
- Slicers & Timeline: untuk memberikan interaktivitas, memungkinkan pengguna memfilter keseluruhan dashboard berdasarkan Periode Waktu, Kurir, Status Pesanan, dan Status Kepatuhan Data.
