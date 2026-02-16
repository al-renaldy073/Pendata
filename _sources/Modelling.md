---
title: Modelling

---

## Modelling
### Pengertian Modelling
Modelling adalah tahap dalam proses Data Mining di mana data yang sudah dibersihkan dan dipersiapkan digunakan untuk membangun model analisis atau prediksi menggunakan algoritma tertentu.

Jika pada tahap sebelumnya kita menyiapkan data, maka pada tahap ini kita:

    Membangun model untuk menemukan pola atau membuat prediksi berdasarkan data.

Model ini nantinya akan digunakan untuk membantu pengambilan keputusan.

### Tujuan Modelling
Tujuan utama tahap modelling adalah:
1. Membuat model yang dapat menjawab masalah bisnis
1. Menemukan pola tersembunyi dalam data
1. Melakukan prediksi atau klasifikasi
1. Menguji performa model

### Jenis-Jenis Teknik Modelling dalam Data Mining
Teknik modelling dipilih sesuai dengan tujuan analisis.

---

1. Classification (Klasifikasi)
Digunakan untuk memprediksi kategori.

    Contoh:
    * Prediksi pelanggan churn atau tidak
    * Prediksi email spam atau tidak

    Algoritma yang sering digunakan:
    * Decision Tree
    * Logistic Regression
    * K-Nearest Neighbor (KNN)
    * Random Forest
    * Support Vector Machine (SVM)

1. Regression (Regresi)
Digunakan untuk memprediksi nilai numerik.

    Contoh:
    * Prediksi harga rumah
    * Prediksi jumlah penjualan

    Algoritma yang sering digunakan:
    * Linear Regression
    * Polynomial Regression
    * Random Forest Regressor
    
1. Clustering (Pengelompokan)
Digunakan untuk mengelompokkan data tanpa label.

    Contoh:
    * Segmentasi pelanggan
    * Pengelompokan wilayah berdasarkan penjualan

    Algoritma yang sering digunakan:
    * K-Means
    * Hierarchical Clustering
    * DBSCAN

1. Association Rule (Aturan Asosiasi)
Digunakan untuk menemukan hubungan antar item.

    Contoh:
    * Market Basket Analysis
    * (Jika membeli roti $\rightarrow$ kemungkinan membeli susu)

    Algoritma:
    * Apriori
    * FP-Growth

### Tahapan dalam Modelling
1. Memilih Algoritma
Pemilihan algoritma tergantung pada:
    * Jenis masalah (klasifikasi, regresi, dll.)
    * Ukuran data
    * Kompleksitas masalah
    * Interpretasi yang dibutuhkan
1. Melatih Model (Training)
Model dilatih menggunakan data training.

    Tujuannya:
Agar model belajar mengenali pola dalam data.
1. Menguji Model (Testing)
Model diuji menggunakan data testing untuk melihat seberapa baik performanya.
1. Evaluasi Model
Beberapa metrik evaluasi:

    **Untuk Klasifikasi:**
    * Accuracy
    * Precision
    * Recall
    * F1-Score
    * Confusion Matrix

    **Untuk Regresi:**
    * Mean Absolute Error (MAE)
    * Mean Squared Error (MSE)
    * R-Square

### Contoh Sederhana
Misalnya kita ingin memprediksi churn pelanggan.

Langkah modelling:
1. Pilih algoritma (misalnya Decision Tree)
1. Latih model dengan data training
1. Uji model dengan data testing
1. Hitung akurasi

Jika akurasi 85%, berarti model cukup baik dalam memprediksi pelanggan yang akan churn.

### Hyperparameter Tuning
Model memiliki parameter yang bisa disesuaikan.

Contoh:
* Jumlah pohon pada Random Forest
* Nilai k pada KNN

Tujuan tuning:
Meningkatkan performa model.

Metode:
* Grid Search
* Cross Validation

### Hubungan dengan Tahap Lain
Alur lengkapnya:

Business Understanding
$\downarrow$
Data Understanding
$\downarrow$
Data Preparation
$\downarrow$
Modelling
$\downarrow$
Deployment

Jika model tidak memberikan hasil yang memuaskan, maka kita bisa kembali ke:
* Data Preparation (perbaiki fitur)
* Data Understanding (analisis ulang data)
* Bahkan Business Understanding (revisi tujuan)

Proses ini bersifat iteratif.

### Kesalahan Umum dalam Modelling
1. Menggunakan algoritma tanpa memahami cara kerjanya
1. Tidak membagi data training dan testing
1. Overfitting (model terlalu cocok pada data training)
1. Tidak mengevaluasi model dengan metrik yang tepat

### Ringkasan
| Aspek | Penjelasan |
| -------- | -------- | 
|Fokus	|Membangun dan menguji model|
|Tujuan	|Menemukan pola atau membuat prediksi|
|Output	|Model dengan performa terukur|
|Tantangan	|Overfitting, pemilihan algoritma|

### Kesimpulan
Modelling adalah tahap inti dalam Data Mining di mana data yang telah dipersiapkan digunakan untuk membangun model analisis atau prediksi. Tahap ini menentukan seberapa baik sistem dapat membantu dalam pengambilan keputusan bisnis.
