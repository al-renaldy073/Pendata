---
title: Ujian Tengah Semester Pendata

---

# Analisa Data Kesuburan Tanah
Analisis dilakukan menggunakan algoritma K-Nearest Neighbor (KNN), yaitu metode klasifikasi berbasis jarak yang menentukan kelas suatu data berdasarkan kedekatan dengan data lain.

Hasil workflow KNIME
![image](https://hackmd.io/_uploads/BJJSK6Bpbl.png)


## 1. Analisis data dengan menggunakan K-Nearest Neighbors (KNN)
Pada tahap ini dilakukan proses klasifikasi data kesuburan tanah menggunakan metode K-Nearest Neighbors (KNN).

KNN merupakan algoritma berbasis jarak yang bekerja dengan cara menentukan kelas suatu data berdasarkan kedekatan dengan data lain yang sudah memiliki label.

KNN bekerja dengan cara:
* menghitung jarak antar data
* mencari K tetangga terdekat
* menentukan kelas berdasarkan mayoritas tetangga

Dalam penelitian ini, KNN digunakan untuk mengklasifikasikan tanah menjadi dua kelas:

* Subur
* Tidak Subur

Parameter yang digunakan:

* K = 5
* Distance = Euclidean

Kondigurasi 

![image](https://hackmd.io/_uploads/Synl56BTbe.png)

Hasilnya ketika saya jalannkan:
![image](https://hackmd.io/_uploads/SyAw6TH6be.png)



## 2. Pemrosesan Data
Sebelum data digunakan, dilakukan tahap preprocessing untuk meningkatkan kualitas data.

Tahapan preprocessing yang dilakukan:

### a. Missing Value
Mengisi data kosong menggunakan:

* Mean (untuk numerik)
* Most Frequent (untuk kategori)

![image](https://hackmd.io/_uploads/SkjuXara-e.png)

Sebelum proses mising value:
![image](https://hackmd.io/_uploads/BkPkETSaZl.png)

Sesudah proses mising value:
![image](https://hackmd.io/_uploads/rJDOEaHpZl.png)

### b. One to Many
Mengubah data kategori Tekstur Tanah menjadi bentuk numerik (one-hot encoding).

Contoh:

* Lempung
* Pasir
* Liat

![image](https://hackmd.io/_uploads/HJmcB6S6Wl.png)



### c. Normalizer
Melakukan normalisasi data agar semua fitur berada pada skala yang sama (0–1).

Parameter:

* Method: Min-Max
* Minimum: 0
* Maximum: 1

![image](https://hackmd.io/_uploads/SkthraBabe.png)


### d. Table Partitioning
Membagi dataset menjadi:

* 80% data training
* 20% data testing

![image](https://hackmd.io/_uploads/HJq6R6rpWx.png)




## 3. Hitung Metrik Evaluasi


| Metrik | Keterangan | 
| -------- | -------- | 
| Accuracy     | Persentase prediksi benar dari total data     |
| Precision     | Ketepatan prediksi kelas positif     |
| Recall     | Kemampuan mendeteksi seluruh kelas positif     |
| F1-Score     | Harmonic mean antara Precision dan Recall 

Setelah model KNN dijalankan, dilakukan evaluasi menggunakan Scorer.

Evaluasi dilakukan untuk mengetahui performa model berdasarkan data aktual dan prediksi, Menggunakan:

Scorer
![image](https://hackmd.io/_uploads/r16s0pr6-e.png)

1. Accuracy
    Accuracy menunjukkan tingkat keberhasilan model dalam memprediksi data dengan benar dibandingkan seluruh data yang diuji.

    Hasil accuracy menunjukkan bahwa model KNN mampu mengklasifikasikan data kesuburan tanah dengan tingkat ketepatan yang baik.

    Semakin tinggi nilai accuracy, semakin baik kemampuan model dalam melakukan klasifikasi secara keseluruhan.

2. Precision

    Precision menunjukkan tingkat ketepatan prediksi terhadap kelas positif (misalnya “Subur”).

    Artinya, precision mengukur seberapa banyak data yang diprediksi sebagai Subur memang benar-benar Subur.

    Nilai precision yang tinggi menunjukkan bahwa model jarang melakukan kesalahan dalam memprediksi kelas positif.

3. Recall

    Recall menunjukkan kemampuan model dalam mendeteksi seluruh data pada kelas positif.

    Dalam konteks ini, recall mengukur seberapa banyak data Subur yang berhasil dikenali dengan benar oleh model.

    Nilai recall yang tinggi berarti model tidak banyak melewatkan data Subur.

4. F1-Score

    F1-Score merupakan nilai rata-rata harmonis antara Precision dan Recall.

    Metrik ini digunakan untuk memberikan keseimbangan antara ketepatan dan kemampuan deteksi model.

    F1-Score yang tinggi menunjukkan model memiliki performa yang seimbang dalam memprediksi kelas Subur dan Tidak Subur.
    
    
Berdasarkan hasil pengujian menggunakan Scorer, diperoleh:

![image](https://hackmd.io/_uploads/HkCWeArTZe.png)


* Accuracy: 54%, Model mampu memprediksi dengan benar sebanyak 216 sampel dari total 400 data uji.
* Correct Classified: 216, Jumlah total prediksi yang sesuai dengan data asli.
* Wrong Classified: 184, Jumlah total prediksi yang meleset dari data asli.
* Error Rate: 46%, Tingkat kesalahan model dalam melakukan klasifikasi.


