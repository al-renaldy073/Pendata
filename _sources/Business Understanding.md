---
title: Business Understanding

---

## Data Mining
### Pengertian Data Mining
Data Mining adalah proses mengekstraksi pola, hubungan, atau informasi yang bernilai dari kumpulan data dalam jumlah besar menggunakan teknik statistik, machine learning, dan basis data.

Secara sederhana:

    Data Mining adalah proses menemukan pengetahuan tersembunyi di dalam data.

Data Mining merupakan bagian dari proses yang lebih besar yaitu Knowledge Discovery in Databases (KDD).

### Tujuan Data Mining
Tujuan utama Data Mining adalah:
1. Mengidentifikasi pola tersembunyi
1. Membuat prediksi
1. Mengelompokkan data
1. Mendukung pengambilan keputusan
1. Mengoptimalkan strategi bisnis

Contoh:
* Memprediksi pelanggan yang akan berhenti berlangganan
* Mengelompokkan pelanggan berdasarkan perilaku belanja
* Mendeteksi transaksi penipuan

### Mengapa Data Mining Penting?
Di era digital, organisasi memiliki data dalam jumlah besar (big data). Tanpa teknik analisis yang tepat, data tersebut hanya menjadi arsip.

Data Mining membantu:
* Mengubah data menjadi informasi
* Mengubah informasi menjadi pengetahuan
* Mengubah pengetahuan menjadi keputusan

### Proses Data Mining
Proses Data Mining umumnya mengikuti metodologi CRISP-DM (Cross Industry Standard Process for Data Mining) yang terdiri dari:
1. Business Understanding
1. Data Understanding
1. Data Preparation
1. Modelling
1. Evaluation
1. Deployment

Setiap tahap saling berhubungan dan bersifat iteratif.
![img_p31](https://hackmd.io/_uploads/ryrcU7gOZg.jpg)


### Teknik dalam Data Mining
Beberapa teknik utama dalam Data Mining:
1. Classification
Digunakan untuk memprediksi kategori/kelas.
Contoh:
Email spam atau bukan
Lulus atau tidak lulus
2. Regression
Digunakan untuk memprediksi nilai numerik.
Contoh:
Prediksi harga rumah
Prediksi penjualan
3. Clustering
Mengelompokkan data berdasarkan kemiripan.
Contoh:
Segmentasi pelanggan
4. Association Rule
Menemukan hubungan antar item.
Contoh:
Market basket analysis (roti sering dibeli bersama susu)
5. Anomaly Detection
Mendeteksi data yang menyimpang.
Contoh:
Deteksi fraud

## Business Understanding
Business Understanding adalah tahap pertama dalam proses Data Mining yang bertujuan untuk memahami permasalahan bisnis secara menyeluruh sebelum melakukan analisis data atau membangun model.
Tahap ini menekankan bahwa:
    
    Proyek data harus dimulai dari kebutuhan bisnis, bukan dari algoritma.
Business Understanding memastikan bahwa analisis yang dilakukan benar-benar menjawab masalah nyata dan memberikan nilai bagi organisasi.

### Tujuan Business Understanding
Tujuan utama tahap ini adalah:
1. Mengidentifikasi masalah bisnis secara jelas
1. Menentukan tujuan proyek
1. Memahami kebutuhan stakeholder
1. Menentukan kriteria keberhasilan (success criteria)
1. Menyusun rencana awal proyek

Dengan kata lain, tahap ini menjadi fondasi seluruh proses Data Mining.

### Mengapa Business Understanding Penting?
Banyak proyek data gagal karena:
* Tujuan tidak jelas
* Masalah bisnis tidak dipahami
* Model dibuat tanpa arah
* Hasil tidak bisa digunakan

Contoh kesalahan umum:

    Tim data membuat model klasifikasi dengan akurasi tinggi, tetapi model tersebut tidak menjawab kebutuhan manajemen.
    
Business Understanding mencegah kesalahan seperti itu.

### Langkah-Langkah dalam Business Understanding
1. Identifikasi Masalah Bisnis
Langkah pertama adalah mendefinisikan masalah secara spesifik.

    Pertanyaan yang perlu dijawab:
    * Masalah apa yang sedang terjadi?
    * Mengapa masalah tersebut penting?
    * Siapa yang terdampak?
    * Apa dampak finansial atau operasionalnya?

    Contoh:

        Tingkat churn pelanggan meningkat 20% dalam satu tahun terakhir.
    Masalah harus ditulis secara jelas dan terukur.
    
1. Menentukan Tujuan Bisnis (Business Objective)
Setelah masalah diidentifikasi, tentukan tujuan yang ingin dicapai.

    Tujuan harus:
    * Spesifik
    * Terukur
    * Realistis
    * Memiliki batas waktu*
    
    Contoh:
    * Mengurangi churn sebesar 10% dalam 6 bulan
    * Meningkatkan penjualan 15% dalam satu tahun
1. Menerjemahkan ke Tujuan Data Mining
Masalah bisnis perlu diterjemahkan menjadi tujuan analitis.

    Contoh:
Masalah bisnis:

        Banyak pelanggan berhenti berlangganan.
    Tujuan Data Mining:

        Membangun model klasifikasi untuk memprediksi pelanggan yang berpotensi churn.
    
    Tahap ini menghubungkan dunia bisnis dengan dunia teknis.
1. Menentukan KPI (Key Performance Indicator)
KPI digunakan untuk mengukur keberhasilan proyek.

    Contoh KPI:
    * Akurasi model minimal 85%
    * Penurunan churn sebesar 10%
    * Peningkatan ROI sebesar 5%
    
    Tanpa KPI, keberhasilan proyek sulit diukur.
1. Identifikasi Stakeholder
Stakeholder adalah pihak yang berkepentingan terhadap hasil proyek.

    Contoh:
    * Manajemen
    * Tim pemasaran
    * Tim IT
    * Pengguna sistem

    Pemahaman kebutuhan stakeholder penting agar solusi sesuai dengan kebutuhan mereka.
    
1. Identifikasi Batasan dan Risiko
Beberapa hal yang perlu dipertimbangkan:
    * Ketersediaan data
    * Kualitas data
    * Waktu pengerjaan
    * Anggaran
    * Risiko kesalahan model

    Contoh risiko:
    * Data tidak lengkap
    * Model bias
    * Sistem tidak siap menerima model

### Contoh Studi Kasus
**Kasus: Perusahaan Retail**
Masalah:
Penjualan menurun dalam 3 bulan terakhir.
Business Understanding:
1. Mengidentifikasi penyebab penurunan
1. Menentukan tujuan: meningkatkan repeat purchase
1. KPI: kenaikan penjualan 10%
1. Tujuan data mining: segmentasi pelanggan menggunakan clustering

Dengan pendekatan ini, proyek menjadi lebih terarah.

### Hubungan Business Understanding dengan Tahap Lain
Business Understanding menjadi dasar bagi:
* Data Understanding
* Data Preparation
* Modelling
* Deployment

Jika tahap pertama salah, maka seluruh proses berikutnya akan ikut salah.

Proses ini bersifat iteratif. Jika hasil modelling tidak sesuai, bisa jadi masalahnya ada pada tahap Business Understanding.

#### Kesalahan Umum dalam Business Understanding
1. Tujuan terlalu umum
1. Tidak melibatkan stakeholder
1. Tidak menetapkan KPI
1. Langsung membangun model tanpa memahami masalah

### Output dari Business Understanding
Di akhir tahap ini biasanya dihasilkan:
* Dokumen definisi masalah
* Tujuan bisnis
* Tujuan analitik
* KPI
* Rencana proyek awal

Dokumen ini menjadi panduan untuk tahap selanjutnya.

### Ringkasan
| Aspek | Penjelasan |
| -------- | -------- | 
| Fokus     | Memahami masalah bisnis     | 
| Tujuan     | Menentukan arah proyek     | 
| Output    | Business objective & KPI    | 
| Dampak     | Menentukan keberhasilan proyek     | 

### Kesimpulan
Business Understanding adalah tahap awal dan paling penting dalam proses Data Mining. Tahap ini memastikan bahwa seluruh analisis data dan pembangunan model dilakukan untuk menjawab kebutuhan bisnis yang nyata dan memberikan nilai strategis bagi organisasi.