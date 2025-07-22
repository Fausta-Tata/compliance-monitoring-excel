## Laporan Analisis Pemantauan Kepatuhan

Dataset: dummy data fiktif  
Periode: 2023 - 2025  
Tools: Microsoft Excel Office 2019  

### Tujuan
Tujuan dari analisis ini adalah untuk mengevaluasi tingkat kepatuhan (compliance) proses pemenuhan pesanan terhadap standar perusahaan (SLA), mengidentifikasi area inefisiensi, dan menemukan akar masalah dari isu kualitas data untuk memberikan rekomendasi perbaikan.

### Ringkasan Temuan
Analisis terhadap 500 data pesanan dari periode 2023-2025 mengungkapkan beberapa temuan krusial yang memerlukan perhatian segera:

#### 1. Kualitas Data yang Masih Buruk
- Temuan: Ditemukan banyak masalah pada data mentah, seperti tanggal dan nama kurir yang tercampur dalam satu kolom, data tanggal yang hilang, inkonsistensi penulisan nama kurir (misalnya "Sicepat" vs. "SiCepat"), dan data yang tidak logis (tanggal kirim lebih awal dari tanggal bayar atau tanggal kirim di masa depan yang tidak masuk akal).
- Dampak: Kualitas data yang buruk ini menghalangi kemampuan untuk mengukur kinerja kepatuhan secara akurat dan berisiko menyebabkan pengambilan keputusan yang salah.

#### 2. Tingkat Kepatuhan Waktu Belum Optimal
- Temuan: Bahkan setelah data dibersihkan, masih ditemukan sejumlah besar pesanan yang berstatus "Tidak Patuh", artinya waktu proses dari pembayaran hingga diserahkan ke kurir melebihi SLA yang ditetapkan yaitu 5 hari.
- Dampak: Keterlambatan ini secara langsung mempengaruhi kepuasan pelanggan dan dapat merusak reputasi perusahaan.

#### 3. Kelengkapan Data Krusial Rendah
- Temuan: Sejumlah pesanan tidak memiliki data Tgl_Diserahkan_Kurir atau Kurir, sehingga status kepatuhannya tidak dapat diukur dan diberi label "Data Tidak Lengkap".
- Dampak: Ini menunjukkan adanya celah dalam proses input data yang perlu segera ditangani untuk memastikan semua pesanan dapat dilacak dan dievaluasi.

### Rekomendasi
Berdasarkan temuan di atas, direkomendasikan tiga tindakan utama:

#### 1. Perbaikan Sistem Input Data (Prioritas Utama):
- Aksi: Mengajukan perubahan pada sistem input data agar memisahkan field untuk Tanggal dan Kurir. Terapkan juga validasi "wajib diisi" (mandatory field) untuk kolom-kolom krusial ini.
- Tujuan: Mencegah masalah kualitas data yang sama terulang di masa depan.

#### 2. Investigasi Keterlambatan Operasional:
- Aksi: Melakukan analisis lebih dalam pada pesanan-pesanan yang berstatus "Tidak Patuh" untuk menemukan penyebab utama keterlambatan (misalnya: masalah pada gudang, proses serah terima dengan kurir tertentu, dll.).
- Tujuan: Mengidentifikasi dan memperbaiki inefisiensi dalam alur kerja operasional.

#### 3. Inisiatif Pembersihan Data Historis:
- Aksi: Membentuk tim untuk membersihkan dan memvalidasi data pengiriman historis.
- Tujuan: Membangun satu sumber data yang akurat (single source of truth) untuk analisis tren jangka panjang yang lebih andal.