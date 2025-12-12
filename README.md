# Final Project: Hotels

------------------------------------------------------------------------

## Anggota Kelompok

| NRP        | Nama            |
|------------|-----------------|
| 5052241005 | Ghisele Valerin |
| 5052241014 | Kiranna Indy    |
| 5052241022 | Elena Miska     |
| 5052241037 | Inessa Regina   |

------------------------------------------------------------------------

## Deskripsi Proyek
Proyek ini akan berisi pipeline pembersihan data dari awal hingga akhir
dan notebook analisis utama termasuk Exploratory Data Analysis (EDA)
dari dataset Hotels.

## Deskripsi Dataset
Dataset ini berisi informasi pemesanan hotel yang dikumpulkan dari dua
properti berbeda, yaitu City Hotel dan Resort Hotel. Setiap baris
mewakili satu pemesanan (booking) yang mencakup karakteristik tamu,
rincian periode menginap, metode pemesanan, status pembayaran, serta
status pembatalan. Dataset ini umum digunakan untuk analisis perilaku
pelanggan, prediksi pembatalan, serta evaluasi pola pemesanan
berdasarkan segmen pasar dan kanal distribusi. Dataset terdiri dari
berbagai tipe variabel, termasuk numerik (misal: jumlah tamu, jumlah
malam menginap, nilai tarif harian), kategorikal (hotel, jenis makanan,
negara asal, segmen pasar, kanal distribusi), serta tanggal (tanggal
kedatangan dan tanggal status reservasi). Total observasi cukup besar
sehingga memungkinkan analisis statistik, pembersihan data, serta
pembuatan model prediksi yang komprehensif.

## Pipeline's Summary
Dataset pemesanan hotel dari City Hotel dan Resort Hotel dibersihkan
melalui beberapa tahapan utama agar siap dianalisis. Proses dimulai
dengan memuat data dan memeriksa struktur awal untuk mengidentifikasi
tipe variabel, potensi missing value, dan inkonsistensi. Missing value
kemudian ditangani secara terarah: children diimputasi median, country
diberi label “UNKNOWN”, agent diisi 0 untuk direct booking, dan company
diisi “Individual” karena sebagian besar pemesanan tidak melalui
perusahaan. Setelah itu dilakukan penyesuaian tipe data dengan
mengonversi variabel numerik menjadi integer, variabel kategorikal
menjadi category, dan variabel tanggal menjadi datetime. Validasi logika
pemesanan dilakukan untuk memastikan tidak ada kasus yang secara bisnis
tidak masuk akal, seperti jumlah tamu nol atau total malam menginap nol.
Outlier hanya diperiksa pada variabel yang esensial dan rawan error,
yaitu ADR dan lead_time, masing-masing ditangani dengan winsorizing dan
filtering berbasis IQR. Duplikasi kemudian dihapus menggunakan kombinasi
variabel yang merepresentasikan identitas unik suatu pemesanan. Tahap
akhir adalah mengekspor dataset bersih tersebut ke dalam file
hotels_cleaned.csv untuk digunakan dalam analisis lebih lanjut.

Pada bagian standarisasi dan transformasi, dilakukan feature engineering
untuk menambah kolom arrival_date, reservation_year, reservation_month,
dan reservation_day.

## Tujuan Analisis
Memahami pola permintaan dan perilaku pelanggan secara menyeluruh agar hotel dapat mengoptimalkan pendapatan melalui strategi harga, kapasitas, dan pemasaran yang lebih tepat.

------------------------------------------------------------------------

## 📁 Struktur File

```         
finalproject/
│
├── README.md                    # Dokumentasi proyek
├── requirements.txt             # Dependencies Python
│
├── data/
│   ├── raw/                     # Dataset mentah
│   │   ├── attendance.csv
│   │   ├── standings.csv
│   │   └── games.csv
│   │
│   └── processed/               # Dataset yang sudah diproses
│
└── notebooks/
    └── final_project.ipynb      # Jupyter notebook analisis utama
```

------------------------------------------------------------------------

## Cara Menjalankan Ulang Proyek

### 1. Prerequisites

Installs: - Python 3.8 atau lebih baru - pip
(Python package manager) - Jupyter Notebook atau Positron/VS Code dengan
extension Jupyter

### 2. Clone Repository

``` bash
git clone <repository-url>
cd finalproject
```

### 3. Setup Environment

#### A: Virtual Environment

``` bash
# Virtual Environment
python -m venv venv

# Aktifkan
# 1. Windows:
venv\Scripts\activate
# 2. Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### B: Install Langsung

``` bash
pip install -r requirements.txt
```

### 4. Jalankan Jupyter Notebook

``` bash
jupyter notebook
```

Selanjutnya akses `notebooks/final_project.ipynb` dan run
secara berurutan cell-cell yang ada.

------------------------------------------------------------------------

## Dependencies
Package yang digunakan dalam proyek ini:

| Package         | Versi Minimum | Fungsi                                  |
|-----------------|---------------|-----------------------------------------|
| numpy           | 1.21.0        | Operasi numerik dan statistik           |
| pandas          | 1.3.0         | Manipulasi dan analisis data            |
| matplotlib      | 3.4.0         | Visualisasi data basic                  |
| seaborn         | 0.11.0        | Visualisasi data statistik (advanced)   |
| scikit-learn    | 0.11.0        | Visualisasi data statistik (advanced)   |

Untuk melihat detail lengkap, lihat file `requirements.txt`.

------------------------------------------------------------------------

## 📊 Hasil Analisis

Setelah dilakukan EDA, ditemukan bahwa permintaan hotel meningkat dari 2015 ke 2016 sebelum cenderung stabil pada 2017, dengan pola musiman yang jelas terutama pada Resort Hotel yang sangat dipengaruhi periode liburan, sementara City Hotel lebih stabil karena banyak melayani tamu bisnis. Pemesanan dengan lead time panjang lebih sering dibatalkan, dan sebagian besar tamu memesan melalui platform online, meskipun pemesanan langsung serta melalui GDS memberikan pendapatan per malam yang lebih tinggi. Namun, analisis masih terbatas pada data historis tiga tahun dan belum memperhitungkan faktor eksternal maupun biaya komisi tiap channel. Berdasarkan temuan tersebut, hotel dapat meningkatkan kinerja bisnis dengan menyesuaikan harga dan penawaran sesuai musim, memperkuat kerja sama dengan perusahaan untuk City Hotel, mendorong lebih banyak pemesanan langsung, serta menerapkan aturan pemesanan yang lebih mengurangi risiko pembatalan jauh hari.
