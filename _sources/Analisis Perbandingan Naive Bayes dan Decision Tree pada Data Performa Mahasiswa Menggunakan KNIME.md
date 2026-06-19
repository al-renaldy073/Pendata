---
title: Analisis Perbandingan Naive Bayes dan Decision Tree pada Data Performa Mahasiswa Menggunakan KNIME

---

# Analisis Perbandingan Naive Bayes dan Decision Tree pada Data Performa Mahasiswa Menggunakan KNIME

## 1. Pendahuluan

Data mining merupakan proses penggalian informasi atau pola tersembunyi dari sekumpulan data dengan memanfaatkan teknik statistik, *machine learning*, dan kecerdasan buatan. Salah satu proses utama dalam data mining adalah klasifikasi, yaitu metode untuk memprediksi suatu kategori berdasarkan pola yang terdapat pada data.

Pada penelitian ini dilakukan analisis perbandingan dua algoritma klasifikasi, yaitu **Naive Bayes** dan **Decision Tree**, untuk memprediksi kategori nilai akhir mahasiswa (**GRADE**) berdasarkan faktor akademik dan non-akademik menggunakan aplikasi KNIME.

Dataset yang digunakan adalah *Higher Education Students Performance Evaluation* yang diperoleh dari UCI Machine Learning Repository. Kedua algoritma diterapkan pada dataset yang sama, kemudian hasil evaluasi dibandingkan menggunakan metrik klasifikasi untuk mengetahui algoritma yang memiliki performa terbaik dalam melakukan prediksi kategori nilai mahasiswa.

---

## 2. Dataset

**Nama Dataset:** *Higher Education Students Performance Evaluation*

**Sumber Dataset:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/856/higher+education+students+performance+evaluation)

**Jumlah baris data:** 145 Record

**Jumlah kolom:** 33 AZtribut

### 2.1 Atribut dan Tipe Data

| Atribut    | Tipe Data Asli | Tipe Data Konseptual |
|------------|----------------|------------------------|
| STUDENT ID | String         | Identifier             |
| COURSE ID  | Integer        | Nominal                |
| Q1–Q30     | Integer        | Nominal                |
| GRADE      | Integer        | Nominal (Target)       |

### 2.2 Karakteristik Dataset

Dataset terdiri atas atribut berikut:

- STUDENT ID
- COURSE ID
- Q1 sampai Q30
- GRADE

Target yang diprediksi adalah atribut **GRADE**, sedangkan atribut **STUDENT ID** hanya berfungsi sebagai identitas mahasiswa dan tidak digunakan dalam proses klasifikasi.

---

## 3. Algoritma Klasifikasi

### 3.1 Naive Bayes

#### Pengertian

Naive Bayes merupakan algoritma klasifikasi berbasis probabilitas yang menggunakan Teorema Bayes. Algoritma ini mengasumsikan bahwa setiap atribut bersifat independen terhadap atribut lainnya.

#### Teorema Bayes

$$
P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}
$$

Keterangan:

- $P(A \mid B)$ : probabilitas terjadinya $A$ jika $B$ diketahui
- $P(B \mid A)$ : probabilitas terjadinya $B$ jika $A$ diketahui
- $P(A)$ : probabilitas awal (*prior*) dari $A$
- $P(B)$ : probabilitas terjadinya $B$

#### Kelebihan

- Mudah diimplementasikan
- Cepat dalam proses pelatihan
- Cocok untuk data kategorikal
- Efektif pada dataset berukuran kecil

#### Kekurangan

- Mengasumsikan atribut saling independen
- Sensitif terhadap atribut yang saling berkorelasi
- Performa dapat menurun pada data yang kompleks

---

### 3.2 Decision Tree

#### Pengertian

Decision Tree merupakan algoritma klasifikasi yang membentuk struktur pohon keputusan untuk menentukan kelas suatu data berdasarkan atribut yang paling berpengaruh. Setiap *node* pada pohon mewakili atribut, setiap cabang mewakili nilai atribut, dan setiap daun (*leaf*) mewakili hasil klasifikasi.

#### Kelebihan

- Mudah dipahami dan divisualisasikan
- Tidak memerlukan asumsi independensi antar atribut
- Mampu menangani hubungan kompleks antar atribut

#### Kekurangan

- Rentan terhadap *overfitting*
- Performa dapat berubah signifikan jika data berubah sedikit
- Pohon yang terlalu besar sulit untuk diinterpretasikan

---

### 3.3 Alasan Pemilihan Metode Klasifikasi

Penelitian ini menggunakan dua algoritma klasifikasi, yaitu **Naive Bayes** dan **Decision Tree**, untuk membandingkan performa dalam memprediksi kategori nilai akhir mahasiswa (**GRADE**).

**Naive Bayes** dipilih karena merupakan algoritma berbasis probabilitas yang sederhana, cepat, dan sesuai untuk dataset berukuran kecil dengan atribut kategorikal.

**Decision Tree** dipilih karena mampu membentuk aturan keputusan berdasarkan atribut yang berpengaruh terhadap hasil klasifikasi serta menghasilkan model yang mudah dipahami.

Perbandingan kedua algoritma dilakukan untuk mengetahui metode yang memiliki performa terbaik berdasarkan hasil evaluasi menggunakan **Accuracy**, **Precision**, **Recall**, **F-Measure**, dan **Cohen's Kappa**.

---

## 4. Workflow KNIME

Workflow yang digunakan dalam penelitian ini ditunjukkan pada gambar berikut.

![image](https://hackmd.io/_uploads/ByUzaYMMGe.png)


### 4.1 Alur Workflow

```text
                        CSV Reader
                            │
                       Missing Value
                            │
                       Column Filter
                            │
                     Number to String
                            │
                     Table Partitioner
                       ┌────┴────┐
              Decision Tree   Naive Bayes
                 Learner         Learner
                    │               │
              Decision Tree   Naive Bayes
                Predictor       Predictor
                    │               │
                 Scorer          Scorer
```

### 4.2 Penjelasan Workflow

Dataset dibaca menggunakan node **CSV Reader**. Selanjutnya dilakukan penanganan nilai kosong menggunakan node **Missing Value**. Setelah itu dilakukan pemilihan atribut menggunakan **Column Filter** dan konversi tipe data menggunakan **Number to String**.

Dataset kemudian dibagi menjadi data *training* dan data *testing* menggunakan node **Table Partitioner**. Data *training* digunakan untuk membangun model klasifikasi Decision Tree dan Naive Bayes, sedangkan data *testing* digunakan untuk menguji performa kedua model. Hasil prediksi masing-masing algoritma selanjutnya dievaluasi menggunakan node **Scorer**.

---

## 5. Penjelasan Setiap Node

### 5.1 CSV Reader

![CSV Reader](https://hackmd.io/_uploads/rJYun9JzGg.png)

**Fungsi**
Digunakan untuk membaca file dataset berformat CSV ke dalam KNIME.

**Output**
Menghasilkan tabel yang berisi seluruh atribut dataset agar dapat diproses pada tahapan berikutnya.

---

### 5.2 Missing Value

![image](https://hackmd.io/_uploads/BJ3v6tGMzl.png)


**Fungsi**
Menangani nilai kosong (*missing value*) pada dataset sebelum diproses lebih lanjut, sehingga setiap atribut memiliki data yang lengkap pada tahap pemodelan.

**Konfigurasi**

| Tipe Data         | Treatment           | Keterangan                                                                                   |
|--------------------|----------------------|-------------------------------------------------------------------------------------------------|
| String              | Most Frequent Value  | Nilai kosong pada kolom bertipe string diisi menggunakan nilai yang paling sering muncul (mode) |
| Number (Integer)    | Mean                 | Nilai kosong pada kolom bertipe integer diisi menggunakan nilai rata-rata (*mean*) dari kolom tersebut |

**Input**
Tabel hasil pembacaan dataset dari node CSV Reader.

**Output**
Tabel dengan nilai kosong yang telah digantikan sesuai aturan *treatment* pada masing-masing tipe data.

**Alasan**
Penanganan nilai kosong dilakukan agar tidak terdapat data yang hilang pada saat proses pelatihan model. Atribut bertipe string ditangani dengan modus karena merepresentasikan kategori, sedangkan atribut bertipe integer ditangani dengan rata-rata karena bersifat numerik sebelum dikonversi menjadi nominal pada tahap berikutnya.

---

### 5.3 Column Filter

![Column Filter — Konfigurasi](https://hackmd.io/_uploads/ry3j3c1fzx.png)
![Column Filter — Hasil](https://hackmd.io/_uploads/rks6hqJzfe.png)

**Fungsi**
Memilih atribut yang digunakan dalam proses klasifikasi.

**Kolom yang dihapus:**

- STUDENT ID

**Kolom yang digunakan:**

- COURSE ID
- Q1–Q30
- GRADE

**Alasan**
STUDENT ID hanya merupakan identitas unik mahasiswa sehingga tidak memiliki pengaruh terhadap kategori nilai akhir.

---

### 5.4 Number to String

![Number to String — Konfigurasi](https://hackmd.io/_uploads/rJEkpqkzfe.png)
![Number to String — Hasil](https://hackmd.io/_uploads/HJDg65JMzx.png)

**Fungsi**
Mengubah tipe data numerik menjadi tipe string (nominal) agar setiap nilai diperlakukan sebagai kategori, bukan sebagai nilai yang memiliki makna perhitungan matematis.

**Konfigurasi**
Kolom yang dikonversi: COURSE ID, Q1–Q30, dan GRADE.

**Alasan**
Kolom COURSE ID, Q1–Q30, dan GRADE direpresentasikan dalam bentuk angka, namun nilai tersebut merupakan kode kategori atau skala penilaian, bukan nilai numerik kontinu. Sebagai contoh, skala penilaian berikut:

| Kode | Kategori      |
|------|---------------|
| 1    | Sangat Rendah |
| 2    | Rendah        |
| 3    | Sedang        |
| 4    | Tinggi        |
| 5    | Sangat Tinggi |

Karena merupakan kategori, atribut tersebut lebih sesuai diproses sebagai data nominal.

---

### 5.5 Table Partitioner

![Table Partitioner — Konfigurasi](https://hackmd.io/_uploads/SJ7Qa9kGMx.png)
![Table Partitioner — Hasil](https://hackmd.io/_uploads/rJ0mT9JzGl.png)

**Fungsi**
Membagi dataset menjadi data *training* dan data *testing*.

**Konfigurasi**

| Parameter           | Nilai          |
|---------------------|----------------|
| Training Data       | 70%            |
| Testing Data        | 30%            |
| Sampling Strategy   | Stratified     |
| Group Column        | GRADE          |

**Alasan**
*Stratified sampling* digunakan agar distribusi kelas GRADE tetap seimbang pada kedua kelompok data.

---

### 5.6 Decision Tree Learner

![Decision Tree Learner](https://hackmd.io/_uploads/rJgAVYbzGe.png)

**Fungsi**
Membangun model klasifikasi menggunakan algoritma Decision Tree berdasarkan data *training*.

**Konfigurasi**

| Parameter                                 | Nilai       | Keterangan                                                                                  |
|--------------------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| Class Column                               | GRADE       | Menentukan kolom target yang akan diprediksi oleh model                                       |
| Quality Measure                            | Gini Index  | Digunakan untuk memilih atribut terbaik pada setiap percabangan berdasarkan tingkat kemurnian |
| Pruning Method                             | No Pruning  | Tidak dilakukan pemangkasan pohon sehingga seluruh aturan hasil pelatihan tetap dipertahankan  |
| Minimum Number of Records per Node         | 2           | Jumlah minimum data yang harus terdapat pada setiap *node* agar dapat dilakukan pemisahan      |

**Input**
Data *training* hasil node Table Partitioner.

**Output**
Model Decision Tree. Struktur pohon keputusan yang terbentuk dapat divisualisasikan sebagai berikut.

![ttg](https://hackmd.io/_uploads/SJqflAzMMe.png)


Pohon keputusan yang terbentuk memiliki root node yang memisahkan data berdasarkan atribut COURSE ID. Selanjutnya, setiap cabang mengalami pemisahan berdasarkan atribut Q1–Q30 hingga mencapai leaf node sebagai hasil klasifikasi.

Setiap node pada pohon menampilkan distribusi kelas GRADE yang terdiri dari kolom Category, %, dan n, serta jumlah keseluruhan data (Total) pada node tersebut.

Konfigurasi Pruning Method yang menggunakan No Pruning dan nilai Minimum Number of Records per Node sebesar 2 menyebabkan pohon yang terbentuk memiliki struktur yang cukup kompleks, dengan banyak cabang dan leaf node yang hanya berisi satu atau dua data. Kondisi ini menunjukkan bahwa model memiliki potensi mengalami overfitting karena terlalu menyesuaikan pola pada data training dibandingkan pola umum dari data.

**Alasan**
Decision Tree digunakan untuk mempelajari pola hubungan antara atribut mahasiswa dan kategori nilai akhir (GRADE) melalui pembentukan pohon keputusan yang digunakan pada proses prediksi.

---

### 5.7 Decision Tree Predictor

![Decision Tree Predictor](https://hackmd.io/_uploads/SkUDrtbGzl.png)

**Fungsi**
Menggunakan model Decision Tree yang telah dibangun untuk memprediksi kategori nilai akhir (GRADE) pada data *testing*.

**Konfigurasi**

| Parameter                                              | Nilai           | Keterangan                                                                  |
|----------------------------------------------------------|-----------------|--------------------------------------------------------------------------------|
| Number of Patterns for Hiliting                          | 10.000          | Jumlah maksimum data yang dapat ditampilkan untuk proses visualisasi (*hiliting*) |
| Change Prediction Column Name                            | Tidak diaktifkan | Menggunakan nama kolom prediksi bawaan dari KNIME                              |
| Append Columns with Normalized Class Distribution        | Tidak diaktifkan | Tidak menambahkan informasi distribusi probabilitas tiap kelas pada hasil prediksi |

**Input**

- Model Decision Tree dari node Decision Tree Learner
- Data *testing* dari node Table Partitioner

**Output**

![Hasil Prediksi Decision Tree](https://hackmd.io/_uploads/HJYvBF-Mfg.png)

Kolom baru `Prediction (GRADE)` yang berisi hasil prediksi kategori nilai mahasiswa berdasarkan model Decision Tree.

**Alasan**
Node ini digunakan untuk menguji model yang telah dilatih dengan menerapkan aturan pohon keputusan pada data *testing* sehingga dapat dibandingkan dengan nilai aktual menggunakan node Scorer.

---

### 5.8 Naive Bayes Learner

![Naive Bayes Learner](https://hackmd.io/_uploads/S1-u6cyffl.png)

**Fungsi**
Membangun model klasifikasi menggunakan algoritma Naive Bayes berdasarkan data *training*.

**Konfigurasi**

| Parameter                                              | Nilai   | Keterangan                                                                          |
|----------------------------------------------------------|---------|----------------------------------------------------------------------------------------|
| Classification Column                                    | GRADE   | Menentukan kolom target yang akan diprediksi oleh model                                |
| Default Probability                                       | 0,0001  | Nilai probabilitas awal untuk menghindari probabilitas nol pada proses perhitungan      |
| Minimum Standard Deviation                                 | 0,0001  | Nilai minimum standar deviasi yang digunakan dalam perhitungan probabilitas             |
| Threshold Standard Deviation                               | 0       | Batas minimum standar deviasi yang digunakan dalam proses pembelajaran model            |
| Maximum Number of Unique Nominal Values per Attribute      | 20      | Jumlah maksimum kategori unik yang dapat diproses pada setiap atribut nominal           |
| Ignore Missing Values                                      | Tidak diaktifkan | Data dengan nilai kosong tetap diproses sesuai konfigurasi bawaan              |

**Input**
Data *training* hasil node Table Partitioner.

**Output**
Model Naive Bayes.

**Alasan**
Kolom GRADE digunakan sebagai target klasifikasi. Algoritma Naive Bayes mempelajari hubungan probabilistik antara atribut mahasiswa dan kategori nilai akhir untuk menghasilkan model yang digunakan pada tahap prediksi.


---

### 5.9 Naive Bayes Predictor

![Naive Bayes Predictor](https://hackmd.io/_uploads/S1zKUK-GGx.png)

**Fungsi**
Menggunakan model Naive Bayes yang telah dibangun untuk memprediksi kategori nilai akhir (GRADE) pada data *testing*.

**Input**

- Model Naive Bayes dari node Naive Bayes Learner
- Data *testing* dari node Table Partitioner

**Output**

![Hasil Prediksi Naive Bayes](https://hackmd.io/_uploads/B1s0691ffe.png)

Kolom baru `Prediction (GRADE)` yang berisi hasil prediksi kategori nilai mahasiswa berdasarkan model Naive Bayes.

---

### 5.10 Scorer

![Scorer](https://hackmd.io/_uploads/SkOZ05kzGg.png)

**Fungsi**
Mengevaluasi performa model klasifikasi.

**Output**

- Confusion Matrix
- Accuracy
- Precision
- Recall
- F-Measure
- Cohen's Kappa

---

## 6. Hasil Evaluasi

### 6.1 Hasil Naive Bayes

![Hasil Evaluasi Naive Bayes](https://hackmd.io/_uploads/BymYvFZzMg.png)

$$
\text{Accuracy} = 31{,}8\%, \qquad \text{Cohen's Kappa} = 0{,}162
$$

**Interpretasi**
Model Naive Bayes berhasil mengklasifikasikan sekitar 31,8% data uji dengan benar. Nilai Cohen's Kappa sebesar 0,162 menunjukkan bahwa tingkat kesesuaian antara prediksi dan data aktual masih tergolong rendah.

---

### 6.2 Hasil Decision Tree

![Hasil Evaluasi Decision Tree](https://hackmd.io/_uploads/r19LDtbffl.png)

$$
\text{Accuracy} = 27{,}3\%, \qquad \text{Cohen's Kappa} = 0{,}139
$$

**Interpretasi**
Model Decision Tree berhasil mengklasifikasikan sekitar 27,3% data uji dengan benar. Nilai Cohen's Kappa sebesar 0,139 menunjukkan bahwa tingkat kesesuaian antara prediksi dan data aktual masih tergolong rendah.

---

### 6.3 Perbandingan Hasil

| Algoritma     | Accuracy | Cohen's Kappa |
|---------------|----------|----------------|
| Naive Bayes   | 31,8%    | 0,162          |
| Decision Tree | 27,3%    | 0,139          |

Berdasarkan tabel di atas, algoritma Naive Bayes menghasilkan nilai *Accuracy* sebesar 31,8%, sedikit lebih tinggi dibandingkan Decision Tree yang memperoleh 27,3%. Selisih ini menunjukkan bahwa Naive Bayes mampu menebak kategori GRADE dengan benar pada proporsi data uji yang sedikit lebih besar dibandingkan Decision Tree.

Nilai *Cohen's Kappa* digunakan untuk mengukur tingkat kesesuaian antara hasil prediksi model dengan label aktual setelah memperhitungkan faktor kebetulan (*chance agreement*). Berdasarkan interpretasi umum nilai Kappa:

| Rentang Nilai Kappa | Tingkat Kesesuaian   |
|----------------------|----------------------|
| < 0,00               | Tidak ada kesesuaian |
| 0,00 – 0,20          | Sangat rendah        |
| 0,21 – 0,40          | Rendah               |
| 0,41 – 0,60          | Cukup                |
| 0,61 – 0,80          | Tinggi               |
| 0,81 – 1,00          | Sangat tinggi        |

Nilai Kappa Naive Bayes (0,162) dan Decision Tree (0,139) keduanya berada pada rentang *sangat rendah*. Hal ini mengindikasikan bahwa meskipun kedua model memiliki nilai *Accuracy* di atas tebakan acak murni, tingkat kesesuaian sebenarnya antara prediksi dan data aktual masih jauh dari memuaskan setelah faktor kebetulan diperhitungkan.

Secara keseluruhan, kedua metrik evaluasi tersebut konsisten menunjukkan keunggulan tipis Naive Bayes dibandingkan Decision Tree pada dataset ini. Namun, perbedaan nilai *Accuracy* (4,5 poin persen) dan *Cohen's Kappa* (0,023 poin) yang relatif kecil mengindikasikan bahwa kedua algoritma sama-sama belum mampu melakukan klasifikasi kategori GRADE dengan tingkat akurasi yang tinggi pada dataset ini.

---

## 7. Analisis Hasil

Berdasarkan hasil evaluasi, algoritma Naive Bayes memperoleh performa yang lebih baik dibandingkan Decision Tree. Hal ini terlihat dari nilai *Accuracy* dan *Cohen's Kappa* yang lebih tinggi pada Naive Bayes.

Beberapa faktor yang diduga mempengaruhi hasil tersebut antara lain:

1. Dataset hanya terdiri dari sekitar 145 data sehingga jumlah data pelatihan relatif sedikit.
2. Variabel target GRADE memiliki banyak kategori kelas.
3. Data akademik memiliki hubungan antar atribut yang cukup kompleks.
4. Decision Tree berpotensi mengalami *overfitting* pada dataset berukuran kecil.
5. Data yang telah dikonversi menjadi atribut nominal lebih sesuai untuk pendekatan probabilistik yang digunakan oleh Naive Bayes.

Meskipun demikian, kedua algoritma masih mampu melakukan klasifikasi terhadap kategori nilai mahasiswa dan menghasilkan prediksi yang dapat dievaluasi menggunakan *confusion matrix* serta metrik klasifikasi lainnya.

---

## 8. Kesimpulan

Penelitian ini membandingkan algoritma Naive Bayes dan Decision Tree pada dataset *Higher Education Students Performance Evaluation* menggunakan KNIME. Tahapan penelitian meliputi pembacaan data, seleksi atribut, konversi tipe data, pembagian data menjadi *training* dan *testing*, pembangunan model klasifikasi, serta evaluasi menggunakan node Scorer.

Berdasarkan hasil pengujian, diperoleh ringkasan sebagai berikut.

| Algoritma     | Accuracy | Cohen's Kappa |
|---------------|----------|----------------|
| Naive Bayes   | 31,8%    | 0,162          |
| Decision Tree | 27,3%    | 0,139          |

Hasil penelitian menunjukkan bahwa algoritma Naive Bayes memiliki performa yang lebih baik dibandingkan Decision Tree pada dataset *Higher Education Students Performance Evaluation*. Secara keseluruhan, *workflow* KNIME yang dibangun berhasil mengimplementasikan proses klasifikasi dan perbandingan dua algoritma data mining sehingga dapat digunakan untuk mengevaluasi performa metode klasifikasi pada data evaluasi mahasiswa.
