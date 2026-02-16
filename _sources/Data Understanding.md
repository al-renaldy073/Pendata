---
title: Data Understanding

---

## Data Understanding
### Pengertian Data Understanding
Data Understanding adalah tahap dalam proses Data Mining yang bertujuan untuk memahami karakteristik, struktur, dan kualitas data yang akan digunakan dalam analisis.

Setelah pada tahap sebelumnya kita memahami masalah bisnis, maka pada tahap ini kita mulai memahami:

    Data apa yang tersedia dan apakah data tersebut mampu menjawab masalah bisnis?
    
Tahap ini menjadi jembatan antara kebutuhan bisnis dan proses teknis analisis data.

### Tujuan Data Understanding
Tujuan utama tahap ini adalah:
1. Mengumpulkan data yang relevan
1. Mengenali struktur dan tipe data
1. Menilai kualitas data
1. Mengidentifikasi pola awal
1. Menemukan potensi masalah dalam data

Tahap ini membantu memastikan bahwa data benar-benar sesuai dengan tujuan proyek.

### Mengapa Data Understanding Penting?
Tanpa memahami data dengan baik:
* Model bisa dibangun dari data yang salah
* Analisis menjadi tidak akurat
* Kesimpulan bisa menyesatkan

Contoh:
Jika ingin memprediksi churn pelanggan tetapi data tidak memiliki informasi riwayat transaksi, maka prediksi menjadi kurang akurat.

### Tahapan dalam Data Understanding
1. Pengumpulan Data (Data Collection)
Data dapat berasal dari berbagai sumber, seperti:
    * Database internal perusahaan
    * File CSV atau Excel
    * API
    * Data publik
    * Sistem transaksi
    
    Pada tahap ini, penting untuk memastikan bahwa data yang dikumpulkan relevan dengan tujuan bisnis.
1. Deskripsi Data (Describing Data)
Langkah berikutnya adalah memahami struktur data.

    Hal-hal yang diperiksa:
    * Jumlah baris dan kolom
    * Nama variabel
    * Tipe data (numerik, kategorikal, teks, tanggal)
    * Rentang nilai setiap variabel

    Contoh:
    * Kolom "Umur" bertipe numerik
    * Kolom "Jenis Kelamin" bertipe kategorikal
    * Kolom "Tanggal Transaksi" bertipe datetime

1. Exploratory Data Analysis (EDA)
Exploratory Data Analysis (EDA) bertujuan untuk menemukan pola awal dalam data.

    Kegiatan yang dilakukan:
    * Menghitung statistik deskriptif (mean, median, standar deviasi)
    * Melihat distribusi data (histogram)
    * Menganalisis hubungan antar variabel (korelasi)
    * Mengidentifikasi outlier

    EDA membantu memahami karakteristik data sebelum masuk ke tahap pembersihan dan pemodelan.
1. Evaluasi Kualitas Data
Data dunia nyata sering memiliki masalah, seperti:
    * Missing values (nilai kosong)
    * Duplikasi data
    * Kesalahan input
    * Outlier ekstrem
    * Inkonsistensi format

    Pada tahap ini, semua potensi masalah tersebut diidentifikasi untuk diperbaiki pada tahap Data Preparation.

### Contoh Sederhana
Misalkan kita memiliki data pelanggan dengan kolom:
* ID Pelanggan
* Umur
* Pendapatan
* Jumlah Transaksi
* Status Churn

Pada tahap Data Understanding, kita:
1. Menghitung rata-rata umur
1. Melihat distribusi pendapatan
1. Mengecek apakah ada nilai kosong
1. Melihat hubungan antara jumlah transaksi dan status churn

Dari sini kita mulai mendapatkan insight awal.

### Hubungan dengan Tahap Lain
Data Understanding berada di antara:

Business Understanding $\rightarrow$ Data Understanding $\rightarrow$ Data Preparation

Jika pada tahap ini ditemukan bahwa data tidak lengkap atau tidak relevan, maka kita mungkin perlu:
* Mengumpulkan data tambahan
* Mengubah tujuan analisis
* Kembali ke tahap Business Understanding

Proses ini bersifat iteratif.

### Kesalahan Umum dalam Data Understanding
1. Tidak melakukan eksplorasi data secara menyeluruh
1. Langsung masuk ke modelling tanpa EDA
1. Mengabaikan missing values
1. Tidak memeriksa distribusi data

### Ringkasan
| Aspek | Penjelasan |
| -------- | -------- | 
|Fokus	|Memahami karakteristik data|
|Tujuan	|Menilai kualitas dan relevansi data|
|Kegiatan|	EDA, statistik deskriptif, evaluasi kualitas|
|Output	| Insight awal & identifikasi masalah data |

### Kesimpulan
Data Understanding adalah tahap penting dalam proses Data Mining yang bertujuan untuk memahami struktur, kualitas, dan pola dalam data. Tahap ini memastikan bahwa data yang digunakan benar-benar sesuai untuk menjawab masalah bisnis dan siap untuk diproses lebih lanjut pada tahap Data Preparation.