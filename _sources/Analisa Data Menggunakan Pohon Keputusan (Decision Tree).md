---
title: Analisa Data Menggunakan Pohon Keputusan (Decision Tree)

---

# Analisa Data Menggunakan Pohon Keputusan (Decision Tree)
# Deskripsi Proyek
Proyek ini bertujuan untuk melakukan klasifikasi ketersediaan stok smartphone menggunakan metode Decision Tree. Dataset yang digunakan berasal dari Kaggle dengan nama Penjualan dan Spesifikasi Datasets Handphone yang berisi 1000 data smartphone beserta spesifikasi dan informasi penjualannya.

Pada penelitian ini, atribut seperti brand, harga, RAM, memori internal, ukuran layar, resolusi kamera, kapasitas baterai, sistem operasi, rating pengguna, dan tahun rilis digunakan sebagai fitur untuk memprediksi variabel target yaitu Stok_tersedia dengan kelas TRUE dan FALSE.

Metode Decision Tree digunakan untuk mengetahui pola dan hubungan antara spesifikasi smartphone dengan ketersediaan stok sehingga dapat membantu proses analisis dan pengambilan keputusan berdasarkan data yang tersedia.


# Dataset
**Nama dataset**: penjualan dan spesifikasi datasets handphone
**Sumber**: Kaggle (https://www.kaggle.com/datasets/funnn28/penjualan-dan-spesifikasi-datasets-handphone)
**Jumlah data**: 1000 baris (records)
**Fitur**:
1. Id_hp
1. Nama_hp
1. Brand
1. Harga
1. Ram
1. Memori
1. Ukuran_layar
1. Resolusi_kamera
1. Kapasitas_baterai
1. Os
1. Rating_pengguna
1. Tahun_rilis
1. Stok_tersedia = (target/class)

Target klasifikasi yang digunakan adalah:

`Stok_tersedia`

dengan class:

* TRUE = Stok tersedia
* FALSE = stok tidak tersedia 


# Pohon Keputusan (Decision Tree)
## Pengertian Decision Tree
Decision Tree adalah metode klasifikasi dalam data mining yang digunakan untuk memprediksi atau mengambil keputusan berdasarkan atribut tertentu dalam bentuk struktur pohon. Metode ini bekerja dengan membagi data ke dalam beberapa cabang berdasarkan kondisi tertentu hingga menghasilkan suatu keputusan atau class.

## Konsep dasar Decision Tree
Decision Tree bekerja dengan memilih atribut terbaik untuk membagi data menjadi beberapa kelompok berdasarkan class tertentu.

Proses pembentukan Decision Tree dilakukan dengan langkah berikut:

1. Sistem membaca data training.
1. Sistem menghitung nilai setiap atribut untuk menentukan atribut terbaik.
1. Atribut terbaik dipilih sebagai root node.
1. Data dibagi menjadi beberapa cabang berdasarkan nilai atribut.
1. Proses pembagian dilakukan terus menerus sampai data pada setiap cabang memiliki class yang homogen atau tidak dapat dibagi lagi.

Pada penelitian ini digunakan metode Gain Ratio untuk memilih atribut terbaik dalam proses pembentukan pohon keputusan.
## Struktur Decision Tree


### Root Node
Root node merupakan simpul utama atau titik awal pada pohon keputusan yang digunakan sebagai dasar pengambilan keputusan pertama.

Pada penelitian ini, atribut yang berpotensi menjadi root node adalah:

`Harga`

Atribut tersebut dipilih karena memiliki kemampuan terbaik dalam membagi data berdasarkan nilai Gain Ratio pada proses pembentukan Decision Tree.

### Internal Node
Internal node adalah simpul percabangan yang berada setelah root node dan digunakan untuk menentukan keputusan berikutnya berdasarkan atribut tertentu.

Contoh atribut yang dapat menjadi internal node:

* `Ram`
* `Kapasitas_baterai`
* `Rating_pengguna`
* `Os`
* `Resolusi_kamera`

### Branch (Cabang)
Branch atau cabang merupakan jalur keputusan yang terbentuk dari nilai suatu atribut.

Contoh cabang pada dataset:

* `Harga > 10.000.000`
* `Harga ≤ 10.000.000`
* `Android`
* `iOS`
* `Rating tinggi`
* `Rating rendah`

### Leaf Node
Leaf node merupakan hasil akhir dari proses klasifikasi pada Decision Tree.
Pada penelitian ini, leaf node terdiri dari:
* `TRUE` = stok tersedia
* `FALSE` = stok tidak tersedia



## Istilah Penting Decision Tree
### 1. Kedalaman Pohon (Tree Depth)

Kedalaman pohon merupakan jumlah level dari root node hingga leaf node pada struktur Decision Tree.

Semakin dalam pohon keputusan:

* model menjadi lebih kompleks,
* proses klasifikasi semakin detail,
* dan risiko overfitting dapat meningkat.

### 2. Panjang Lintasan (Path Length)

Panjang lintasan adalah jumlah tahapan keputusan dari root node menuju leaf node.

Contoh lintasan pada dataset smartphone:

`Harga → Ram → Rating_pengguna → Stok_tersedia`

Semakin panjang lintasan, maka aturan klasifikasi yang dihasilkan menjadi semakin spesifik.

### 3. Overfitting

Overfitting terjadi ketika model terlalu menyesuaikan data training sehingga performa model pada data baru menjadi kurang optimal.

Ciri-ciri overfitting:

* pohon terlalu besar,
* jumlah cabang terlalu banyak,
* dan aturan keputusan terlalu detail.

Untuk mengurangi overfitting, pada penelitian ini digunakan parameter:

`Minimum number of records per node = 10`

### 4. Pruning

Pruning adalah proses penyederhanaan pohon keputusan dengan mengurangi cabang yang kurang penting.

Tujuan pruning:

* mengurangi overfitting,
* menyederhanakan struktur pohon,
* serta mempermudah interpretasi hasil klasifikasi.

Pada penelitian ini digunakan metode:

`MDL Pruning`

## Entropy

Entropy digunakan untuk mengukur tingkat ketidakpastian atau ketidakteraturan data pada proses klasifikasi.

Jika data masih terdiri dari beberapa class yang bercampur, maka nilai entropy akan tinggi. Sebaliknya, jika data didominasi oleh satu class tertentu, maka nilai entropy akan rendah.

Rumus entropy:

$$Entropy(S) = -\sum_{i=1}^{n} p_i \log_2 p_i$$

Keterangan:
$S$ = himpunan data
$n$ = jumlah class
$p_i$ = proporsi data pada class ke-i
$log_2$ = logaritma basis 2

Pada penelitian ini terdapat dua class, yaitu:

* `TRUE` = stok tersedia
* `FALSE` = stok tidak tersedia

Jika seluruh data berada pada satu class yang sama, maka entropy bernilai rendah atau mendekati 0 karena data sudah homogen.

Contoh:

    Semua data = TRUE

Sebaliknya, entropy menjadi tinggi apabila jumlah data TRUE dan FALSE relatif seimbang.

Contoh:

    50% TRUE
    50% FALSE


Kondisi tersebut menunjukkan data masih bercampur sehingga tingkat ketidakpastiannya tinggi.

## Information Gain
Information Gain digunakan untuk mengetahui seberapa baik suatu atribut dalam membagi data menjadi kelompok yang lebih teratur atau lebih homogen.

Semakin besar nilai Information Gain, maka semakin baik atribut tersebut dalam mengurangi ketidakpastian data.

Contoh pada dataset smartphone:

Jika atribut `Harga` mampu membagi data Stok_tersedia menjadi kelompok `TRUE` dan `FALSE` dengan lebih jelas, maka atribut tersebut akan memiliki nilai Information Gain yang tinggi.

Namun, Information Gain memiliki kelemahan, yaitu cenderung memberikan nilai tinggi pada atribut yang memiliki banyak kategori. Oleh karena itu, pada penelitian ini digunakan metode Gain Ratio untuk memperoleh hasil klasifikasi yang lebih optimal.

Rumus Information Gain:

$$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} Entropy(S_v)$$

Keterangan:

* $S$ = seluruh data
* $A$ = atribut yang diuji
* $Values(A)$ = seluruh nilai yang dimiliki atribut 
* $A$$S_v$ = subset data berdasarkan nilai atribut 
* $v$$|S_v|$ = jumlah data pada subset 
* $S_v$$|S|$ = jumlah seluruh data
* $Entropy(S_v)$ = nilai entropy pada subset data

## Split Information

Split Information digunakan untuk menghitung seberapa besar distribusi atau penyebaran data pada setiap cabang hasil pembagian atribut.

Jika suatu atribut membagi data menjadi terlalu banyak cabang kecil, maka nilai Split Information akan meningkat dan memengaruhi nilai Gain Ratio.

Pada dataset smartphone, atribut seperti `Brand` dapat memiliki banyak kategori sehingga menghasilkan banyak cabang. Oleh karena itu, Split Information digunakan agar atribut dengan kategori yang terlalu banyak tidak langsung dianggap sebagai atribut terbaik dalam pembentukan Decision Tree.

$$SplitInfo(S,A) = - \sum_{i=1}^{n} \frac{|S_i|}{|S|} \log_2 \left( \frac{|S_i|}{|S|} \right)$$

Keterangan:
* $A$ = atribut yang diuji
* $S_i$ = subset data ke-i setelah pembagian atribut
* $|S_i|$ = jumlah data pada subset ke-i
* $|S|$ = jumlah seluruh data
* $n$ = jumlah cabang atau jumlah nilai atribut

## Gain Ratio

Gain Ratio merupakan pengembangan dari Information Gain yang digunakan untuk mengurangi bias terhadap atribut yang memiliki terlalu banyak kategori.

Atribut dengan nilai Gain Ratio terbesar akan dipilih sebagai node pada Decision Tree karena dianggap paling baik dalam membagi data.

Gain Ratio dinilai lebih baik dibandingkan Information Gain karena tidak hanya memperhatikan penurunan entropy, tetapi juga mempertimbangkan penyebaran data pada setiap cabang hasil pembagian atribut.

Pada penelitian ini, metode Gain Ratio digunakan untuk membangun model Decision Tree pada dataset penjualan dan spesifikasi smartphone karena mampu menghasilkan pembagian data yang lebih optimal dan mengurangi bias pada atribut yang memiliki banyak kategori seperti `Brand` atau `Nama_hp`.

Pada node Decision Tree Learner di KNIME, proses perhitungan Entropy, Information Gain, Split Information, dan Gain Ratio dilakukan secara otomatis oleh sistem untuk menentukan atribut terbaik dalam pembentukan pohon keputusan.

Rumus Gain Ratio:

$$GainRatio(S,A) = \frac{Gain(S,A)}{SplitInfo(S,A)}$$

Keterangan:
* $Gain(A)$ = nilai Information Gain dari atribut $A$
* $SplitInfo(A)$ = nilai Split Information dari atribut $A$
* $GainRatio(A)$ = nilai akhir yang digunakan untuk menentukan atribut terbaik

# Workflow KNIME
![image](https://hackmd.io/_uploads/B13yBM1yGl.png)

| Tahapan         | Node                    | Fungsi Utama                                                                 |
|-----------------|-------------------------|--------------------------------------------------------------------------------|
| 1. Input        | CSV Reader              | Membaca dataset penjualan dan spesifikasi smartphone dari file CSV.           |
| 2. Persiapan    | Table Partitioner       | Membagi data menjadi data training (70%) dan data testing (30%).             |
| 3. Estetika     | Color Manager           | Memberikan warna pada class `TRUE` dan `FALSE` agar mudah dibedakan.         |
| 4. Estetika     | Color Appender          | Menerapkan warna ke data untuk memperjelas visualisasi Decision Tree.         |
| 5. Pembelajaran | Decision Tree Learner   | Membangun model Decision Tree menggunakan metode Gain Ratio.                  |
| 6. Prediksi     | Decision Tree Predictor | Melakukan prediksi `Stok_tersedia` pada data testing menggunakan model.       |
| 7. Output       | Model Writer            | Menyimpan model Decision Tree yang telah dibuat ke dalam file.                |
| 8. Evaluasi     | Scorer                  | Menghitung performa model seperti Accuracy dan Confusion Matrix.              |

## A. CSV Reader
Node CSV Reader digunakan untuk membaca dataset dari file berformat CSV ke dalam workflow.

Pada node ini:

* File dataset dipilih dari direktori penyimpanan
* Delimiter (pemisah,  koma) disesuaikan
* Tipe data tiap kolom dapat dideteksi otomatis atau diatur manual

![image](https://hackmd.io/_uploads/rywYHfyJze.png)

![image](https://hackmd.io/_uploads/H1NOHMkyMl.png)


## B. Table Partitioner
Node Table Partitioner digunakan untuk membagi dataset menjadi dua bagian, yaitu:

```
data training
data testing
```

Pada penelitian ini, pembagian data dilakukan dengan perbandingan:

```
70% data training
30% data testing
```

Metode sampling yang digunakan adalah:

    Stratified Sampling

Penggunaan Stratified Sampling bertujuan agar proporsi class TRUE dan FALSE pada atribut Stok_tersedia tetap seimbang pada data training maupun data testing.

![image](https://hackmd.io/_uploads/B10hSz1kfx.png)

![image](https://hackmd.io/_uploads/ByXG8G11fx.png)

![image](https://hackmd.io/_uploads/SkHxLGJJGe.png)

## C. Color Manager
Node Color Manager digunakan untuk memberikan warna pada class target agar hasil visualisasi lebih mudah dipahami.

Contoh pewarnaan pada penelitian ini:

```
TRUE = hijau
FALSE = merah
```

Pemberian warna dilakukan pada atribut `Stok_tersedia` sebagai target klasifikasi.

![image](https://hackmd.io/_uploads/B1GjIMk1fl.png)

![image](https://hackmd.io/_uploads/ByKc8fJ1Mx.png)

## D. Color Appender
Node Color Appender digunakan untuk menerapkan warna yang telah diatur pada node Color Manager ke dalam data.

Pada penelitian ini, warna diterapkan pada class `Stok_tersedia` sehingga hasil visualisasi Decision Tree menjadi lebih jelas dan mudah dibedakan antara class `TRUE` dan `FALSE`.

![image](https://hackmd.io/_uploads/Sy8evfykGl.png)



## E. Decision Tree Learner
Node Decision Tree Learner digunakan untuk membangun model klasifikasi menggunakan metode Decision Tree berdasarkan data training.

Konfigurasi yang digunakan pada penelitian ini yaitu:

    Quality Measure = Gain Ratio
    Minimum number of records per node = 10

Penjelasan:
* Gain Ratio digunakan untuk menentukan atribut terbaik dalam proses pembentukan pohon keputusan karena mampu mengurangi bias pada atribut yang memiliki banyak kategori.
* Minimum number of records per node digunakan untuk membatasi jumlah minimum data pada setiap node agar struktur pohon tidak terlalu kompleks.

Jika nilai minimum terlalu kecil:

* pohon keputusan menjadi terlalu besar,
* jumlah cabang terlalu banyak,
* dan risiko overfitting meningkat.

Sebaliknya, jika nilai minimum terlalu besar:

* pohon menjadi terlalu sederhana,
* sehingga beberapa pola penting pada data dapat tidak terbaca dengan baik.

![image](https://hackmd.io/_uploads/B197Dz1yfe.png)

![image](https://hackmd.io/_uploads/rJBVDG1yGe.png)


## F. Decision Tree Predictor
Node Decision Tree Predictor digunakan untuk menerapkan model Decision Tree yang telah dibuat ke data testing.

Node ini berfungsi untuk menghasilkan prediksi class berdasarkan model yang diperoleh dari proses training sebelumnya.

Pada penelitian ini, hasil prediksi yang dihasilkan adalah:

    TRUE = stok tersedia
    FALSE = stok tidak tersedia

Output dari node ini akan digunakan pada tahap evaluasi untuk mengukur performa model klasifikasi yang telah dibangun.

![image](https://hackmd.io/_uploads/Bk_YPGy1fx.png)


## G. Scorer
Node Scorer digunakan untuk mengevaluasi hasil prediksi dari model Decision Tree dengan membandingkan data prediksi dan data asli (actual class).

Node ini menghasilkan nilai performa klasifikasi seperti:

* Accuracy
* Precision
* Recall
* F-Measure
* Confusion Matrix

Pada penelitian ini, node Scorer digunakan untuk mengetahui tingkat akurasi model dalam memprediksi class Stok_tersedia dengan kategori `TRUE` dan `FALSE`.

![image](https://hackmd.io/_uploads/ryrCwfk1zx.png)

![image](https://hackmd.io/_uploads/S14ydMk1Gl.png)

![image](https://hackmd.io/_uploads/SJFkdf11Gl.png)


## H. Model Writer
Node Model Writer digunakan untuk menyimpan model Decision Tree yang telah dibuat ke dalam file sehingga model dapat digunakan kembali tanpa perlu melakukan proses training ulang.

![image](https://hackmd.io/_uploads/ByTZ_G1yMx.png)


# Hasil Decision Tree
Hasil Decision Tree menunjukkan aturan keputusan berdasarkan atribut smartphone yang digunakan pada proses klasifikasi.

Beberapa atribut yang sering muncul pada pohon keputusan antara lain:

* Harga
* Ram
* Rating_pengguna
* Kapasitas_baterai
* Os

Pohon keputusan membentuk beberapa lintasan keputusan berdasarkan kondisi tertentu dari spesifikasi smartphone.

Contoh lintasan keputusan:

`Harga → Ram → Rating_pengguna → Stok_tersedia`

Lintasan tersebut menunjukkan bahwa keputusan class TRUE atau FALSE pada atribut Stok_tersedia dipengaruhi oleh kombinasi beberapa atribut smartphone yang digunakan dalam proses klasifikasi.

![image](https://hackmd.io/_uploads/BkL1Y4yyMl.png)

![image](https://hackmd.io/_uploads/H11TF4kkfe.png)


![ss](https://hackmd.io/_uploads/H1oScSyJfe.png)


## Confusion Matrix
Confusion Matrix digunakan untuk membandingkan hasil prediksi model Decision Tree dengan data asli (actual class) pada atribut Stok_tersedia.

Tabel Confusion Matrix
| Aktual / Prediksi | TRUE | FALSE |
| ----------------- | ---- | ----- |
| **TRUE**          | 89   | 80    |
| **FALSE**         | 61   | 70    |

Penjelasan:
* True Positive (TP) = 89
Data TRUE yang berhasil diprediksi TRUE oleh model.
* False Negative (FN) = 80
Data TRUE tetapi diprediksi FALSE.
* False Positive (FP) = 61
Data FALSE tetapi diprediksi TRUE.
* True Negative (TN) = 70
Data FALSE yang berhasil diprediksi FALSE oleh model.

## Perhitungan Accuracy
Accuracy digunakan untuk mengukur tingkat ketepatan model Decision Tree dalam melakukan klasifikasi pada atribut `Stok_tersedia`.

Rumus accuracy:

$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$

Keterangan:

* $TP$ = True Positive
* $TN$ = True Negative
* $FP$ = False Positive
* $FN$ = False Negative

Substitusi nilai:

$$Accuracy = \frac{89 + 70}{89 + 70 + 61 + 80}$$

$$Accuracy = \frac{159}{300} = 0.53$$

Jika diubah ke bentuk persentase:

$$0.53 \times 100\% = 53\%$$

Hasil accuracy sebesar $53\%$ menunjukkan bahwa model Decision Tree mampu melakukan klasifikasi Stok_tersedia dengan tingkat ketepatan sebesar $53\%$ dari seluruh data testing yang digunakan.

# Analisis
Berdasarkan hasil pengujian, metode Decision Tree menggunakan Gain Ratio mampu membentuk model klasifikasi untuk memprediksi Stok_tersedia pada dataset smartphone.

Atribut yang sering muncul pada percabangan pohon keputusan menunjukkan bahwa atribut tersebut memiliki pengaruh terhadap hasil klasifikasi ketersediaan stok smartphone.

Beberapa atribut yang sering muncul pada proses klasifikasi antara lain:

* Harga
* Ram
* Rating_pengguna
* Kapasitas_baterai

Penggunaan parameter:

    Minimum number of records per node = 10

membantu mengurangi jumlah cabang yang terlalu kecil sehingga struktur pohon keputusan menjadi lebih sederhana dan lebih mudah dianalisis.

Selain itu, penggunaan metode Gain Ratio membantu dalam memilih atribut terbaik secara lebih seimbang, terutama pada atribut yang memiliki banyak kategori seperti `Brand` dan `Os`.

# Kesimpulan
Berdasarkan hasil penelitian, metode Decision Tree menggunakan Gain Ratio mampu digunakan untuk melakukan klasifikasi Stok_tersedia pada dataset penjualan dan spesifikasi smartphone.

Model berhasil membentuk aturan keputusan berdasarkan beberapa atribut penting seperti:

* Harga
* Ram
* Rating_pengguna
* Kapasitas_baterai
* Os

Hasil evaluasi menggunakan Confusion Matrix menunjukkan nilai accuracy sekitar $53\%$, sehingga model mampu melakukan klasifikasi data smartphone berdasarkan atribut yang digunakan, meskipun performa model masih dapat ditingkatkan untuk memperoleh hasil yang lebih optimal.
