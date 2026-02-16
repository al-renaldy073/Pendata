---
title: Data Preparation

---

## Data Preparation
### Pengertian Data Preparation
Data Preparation adalah tahap dalam proses Data Mining yang bertujuan untuk membersihkan, memperbaiki, dan mengubah data mentah menjadi data yang siap digunakan untuk proses pemodelan (Modelling).

Jika pada tahap Data Understanding kita memahami data, maka pada tahap ini kita:

    Memperbaiki dan menyiapkan data agar bisa digunakan oleh algoritma machine learning
    
Tahap ini sering menjadi tahap yang paling memakan waktu (sekitar 60–80% waktu proyek data mining).

### Tujuan Data Preparation
Tujuan utama tahap ini adalah:
1. Membersihkan data dari kesalahan
1. Mengatasi missing values
1. Menghilangkan duplikasi
1. Menangani outlier
1. Mengubah format data agar sesuai untuk pemodelan
1. Membuat fitur baru (feature engineering)

### Proses dalam Data Preparation
1. Data Cleaning (Pembersihan Data)
Ini adalah langkah paling penting.
    * Mengatasi Missing Values
    Contoh masalah:
        * Kolom "Pendapatan" kosong
        * Kolom "Umur" tidak terisi

        Solusi:
        * Menghapus baris yang kosong
        * Mengisi dengan mean/median
        * Mengisi dengan nilai tertentu (misalnya 0 atau "Unknown")

    * Menghapus Data Duplikat
    Data yang sama bisa tercatat lebih dari satu kali.
    Duplikasi dapat menyebabkan hasil analisis menjadi bias.

    * Menangani Outlier
    Outlier adalah nilai yang terlalu jauh dari distribusi normal.
    
        Contoh:
        Jika rata-rata umur pelanggan 30–40 tahun, tetapi ada umur 150 tahun, itu kemungkinan kesalahan input.

        Outlier bisa:
        * Dihapus
        * Diubah
        * Dibiarkan jika memang valid
        
1. Data Transformation (Transformasi Data)
    Data sering perlu diubah agar sesuai dengan algoritma.
    * Normalisasi / Standardisasi
        Beberapa algoritma sensitif terhadap skala data.
        Contoh:
        * Pendapatan: 1.000.000 – 100.000.000
        * Jumlah transaksi: 1 – 50
        
        Jika tidak dinormalisasi, model bisa bias pada variabel dengan nilai besar.
    * Encoding Data Kategorikal
    Algoritma machine learning tidak bisa membaca teks.
        
        Contoh:
        Jenis Kelamin:
        * Laki-laki
        * Perempuan
        
        Diubah menjadi:
        * 0 dan 1
        
        Teknik:
        * Label Encoding
        * One Hot Encoding
        
1. Feature Engineering
Feature Engineering adalah proses membuat variabel baru yang lebih informatif.

    Contoh:
    * Dari "Tanggal Transaksi" dibuat:
        * Hari
        * Bulan
        * Tahun
    * Dari "Total Belanja" dibuat:
        * Rata-rata belanja per bulan

        Fitur yang baik akan meningkatkan akurasi model.
        
1. Feature Selection
    Tidak semua variabel perlu digunakan.

    Tujuannya:
    * Mengurangi kompleksitas model
    * Menghindari overfitting
    * Mempercepat proses training

    Contoh:
    Kolom ID biasanya tidak perlu digunakan dalam model prediksi.

1. Data Splitting
    Sebelum masuk ke tahap modelling, data dibagi menjadi:
    * Training set (untuk melatih model)
    * Testing set (untuk menguji model)

    Contoh umum:
    * 80% training
    * 20% testing

### Hubungan dengan Tahap Lain
Alur prosesnya:

Business Understanding
$\downarrow$
Data Understanding
$\downarrow$
Data Preparation
$\downarrow$
Modelling

Jika pada tahap modelling hasilnya kurang baik, sering kali kita kembali ke tahap Data Preparation untuk memperbaiki fitur atau membersihkan data lebih lanjut.

Proses ini bersifat iteratif.

### Contoh Sederhana
Misalnya kita ingin memprediksi churn pelanggan.

Data mentah memiliki:
* Umur (ada yang kosong)
* Pendapatan (format berbeda-beda)
* Status pelanggan (aktif/tidak aktif)

Pada tahap Data Preparation kita:
* Mengisi umur yang kosong dengan median
* Mengubah format pendapatan menjadi numerik
* Mengubah status menjadi 0 dan 1
* Menghapus data duplikat
* Membagi data menjadi training dan testing

Setelah itu, data siap digunakan untuk modelling.

### Kesalahan Umum dalam Data Preparation
1. Menghapus terlalu banyak data tanpa analisis
1. Mengabaikan outlier
1. Tidak melakukan normalisasi saat diperlukan
1. Data leakage (mencampur data testing saat training)

### Ringkasan
| Aspek | Penjelasan |
| -------- | -------- | 
|Fokus|	Menyiapkan data agar siap diproses|
|Kegiatan|	Cleaning, transformasi, feature engineering|
|Output	|Dataset bersih dan siap modelling|
|Tantangan|	Missing values, outlier, inkonsistensi|

### Kesimpulan
Data Preparation adalah tahap penting dalam Data Mining yang bertujuan untuk membersihkan dan mengubah data mentah menjadi data yang siap digunakan oleh algoritma machine learning. Tanpa tahap ini, model yang dihasilkan bisa tidak akurat atau bahkan salah.