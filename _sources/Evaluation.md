---
title: Evaluation

---

## Evaluation
### Pengertian Evaluation
Evaluation adalah tahap untuk menilai apakah model yang telah dibuat benar-benar:
* Akurat
* Sesuai dengan tujuan bisnis
* Layak untuk digunakan (deploy)

Pada tahap ini kita menjawab pertanyaan:

    Apakah model sudah cukup baik untuk menyelesaikan masalah bisnis?
    
### Tujuan Evaluation
Tujuan utama tahap Evaluation adalah:
Mengukur performa model secara objektif
Membandingkan beberapa model
Memastikan model sesuai kebutuhan bisnis
Menghindari kesalahan sebelum deployment

### Perbedaan Modelling dan Evaluation
| Modelling         | Evaluation                    |
| ----------------- | ------------------------------|
| Membangun model   | Menilai model                 |
| Melatih algoritma | Mengukur performa             |
| Fokus teknis      | Fokus kualitas & tujuan bisnis|

Jadi Evaluation bukan sekadar melihat akurasi, tapi juga melihat apakah model benar-benar berguna.

### Metode Evaluasi Berdasarkan Jenis Masalah
#### A. Evaluation untuk Klasifikasi
Digunakan  untuk prediksi kategori (contoh: churn / tidak churn).
Metrik yang digunakan:
1. Accuracy
Persentase prediksi yang benar.
$$Accuracy = \frac{Prediksi\ Benar}{Total\ Data}$$​
1. Precision
Seberapa tepat model dalam memprediksi kelas positif.
1. Recall
Seberapa banyak kasus positif yang berhasil terdeteksi.
1. F1-Score
Gabungan precision dan recall.
1. Confusion Matrix
Tabel yang menunjukkan:
    * True Positive
    * False Positive
    * True Negative
    * False Negative

#### B. Evaluation untuk Regresi
Digunakan untuk prediksi angka (contoh: harga rumah).
Metrik:
* MAE (Mean Absolute Error)
Rata-rata selisih absolut antara prediksi dan nilai asli.
* MSE (Mean Squared Error)
Rata-rata kuadrat kesalahan.
* R-Square (R²)
Seberapa besar variasi data dapat dijelaskan oleh model.

#### C. Evaluation untuk Clustering
Karena tidak ada label, evaluasinya berbeda:
Silhouette Score
Davies-Bouldin Index
Evaluasi visualisasi cluster

### Evaluasi dari Sisi Bisnis
Evaluation tidak hanya teknis.

Contoh:
Model churn memiliki akurasi 85%.

Pertanyaannya:
* Apakah 85% cukup untuk keputusan bisnis?
* Apakah biaya kesalahan prediksi lebih besar dari manfaatnya?
* Apakah model membantu meningkatkan profit?

Kadang model dengan akurasi sedikit lebih rendah tetapi lebih stabil justru lebih baik untuk bisnis.

### Jika Model Tidak Memenuhi Target?
Maka bisa kembali ke:
* $\circlearrowleft$ Data Preparation (tambah fitur)
* $\circlearrowleft$ Data Understanding (analisis ulang data)
* $\circlearrowleft$ Modelling (ganti algoritma)

Proses ini disebut iteratif.

### Hubungan dengan Tahap Lain
Business Understanding
$\downarrow$
Data Understanding
$\downarrow$
Data Preparation
$\downarrow$
Modelling
$\downarrow$
Evaluation
$\downarrow$
Deployment

### Kesalahan Umum dalam Evaluation
Hanya melihat accuracy
Tidak menggunakan data testing
Data leakage (data testing ikut dilatih)
Tidak mempertimbangkan kebutuhan bisnis

### Ringkasan
| Aspek     | Penjelasan                       |
| --------- | -------------------------------- |
| Fokus     | Menilai kualitas model           |
| Tujuan    | Memastikan model layak digunakan |
| Output    | Model terbaik siap deployment    |
| Tantangan | Overfitting & salah interpretasi |


### Kesimpulan
Evaluation adalah tahap penting dalam Data Mining untuk memastikan bahwa model yang dibuat tidak hanya bekerja secara teknis, tetapi juga benar-benar sesuai dengan kebutuhan bisnis sebelum diterapkan ke dunia nyata.