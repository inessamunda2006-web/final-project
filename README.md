Anggota Kelompok:
1. Ghisele Valerin (5052241005)
2. Kiranna Indy (5052241014)
3. Elena Miska (5052241022)
4. Inessa Regina (5052241037)

Project Workflow & Data Processing Steps : 

0. Checking Data Type
Memeriksa data type awal untuk menentukan langkah lanjutan.

1. Missing value handling
Setelah memetakan jumlah dan distribusi nilai yang hilang, dilakukan imputasi sesuai karakteristik masing-masing variabel.
Children diisi median karena distribusinya skewed dan median lebih stabil.
Country diisi dengan kategori “Unknown” karena informasi ini bersifat opsional saat pengisian data.
Agent diisi 0 yang merepresentasikan direct booking.
Company diisi “Individual” untuk menandakan bahwa pemesanan tidak melibatkan perusahaan.
 Strategi ini dipilih agar imputasi tidak mengganggu distribusi asli dan tetap masuk akal secara bisnis.

2. Type casting
Setelah nilai kosong ditangani, variabel diubah ke tipe data yang sesuai untuk mempermudah analisis berikutnya. Variabel numerik dikonversi menjadi integer, sementara variabel kategorikal seperti hotel, meal, market_segment, atau reservation_status dikonversi menjadi category. Kolom tanggal seperti reservation_status_date dikonversi ke datetime untuk memungkinkan analisis berbasis waktu.

3. Validasi konsistensi booking
Validasi logika dilakukan untuk memastikan setiap pemesanan masuk akal secara bisnis. Tahap ini mencegah data tidak valid masuk ke tahap analisis.
Pemesanan dengan total tamu 0 diperiksa karena secara logis tidak mungkin ada reservasi tanpa tamu.
Durasi menginap (weekend + week nights) yang bernilai 0 dianalisis lebih lanjut; bila tidak dibatalkan, kemungkinan merupakan same-day stay, namun tetap dicatat sebagai potensi noise.

4. Outlier detection & treatment
Deteksi outlier difokuskan hanya pada variabel yang secara substantif rentan terhadap error, yaitu ADR dan lead_time.
ADR dianalisis menggunakan IQR dan outlier ditangani dengan winsorizing karena nilai ekstrem biasanya merupakan kesalahan input dan dapat merusak distribusi harga.
Lead_time juga diperiksa dengan IQR; nilai yang melebihi batas logis difilter karena booking dengan lead_time ratusan hari umumnya merupakan pencatatan yang keliru.

5. Duplicate handling
Penghapusan duplikasi dilakukan pada tahap akhir ketika data sudah bersih. Subset variabel yang digunakan mencakup elemen-identitas utama sebuah pemesanan seperti hotel, arrival_date, komposisi tamu, room type, agent, company, country, ADR, serta status pembatalan. Variabel-variabel ini memastikan bahwa hanya baris yang benar-benar identik yang dihapus, tanpa menghilangkan variasi booking yang valid.

6. Final export
Dataset yang telah melalui seluruh proses cleaning disimpan sebagai hotels_cleaned.csv agar dapat digunakan dalam analisis lanjutan, modelling, atau visualisasi.
