---
title: Analisa Data Menggunakan Naive Bayes

---

# Analisa Data Menggunakan Naive Bayes
# Deskripsi Proyek
Proyek ini bertujuan untuk melakukan analisis dan klasifikasi data menggunakan metode Naive Bayes. Proses pemodelan dilakukan melalui Python Script dengan memanfaatkan library Scikit-learn, tanpa menggunakan node classifier bawaan KNIME.

# Dataset
**Nama dataset**: Bank Marketing Dataset
**Sumber**: Kaggle (https://www.kaggle.com/datasets/janiobachmann/bank-marketing-dataset)
**Jumlah data**: 11.162 baris (records)
**Fitur**: age, job, marital, education, default, balance, housing, loan, contact, day, month, duration, campaign, pdays, previous, poutcome, dan y sebagai label klasifikasi


# Metode Naive Bayes
## Pengertian Naive Bayes
Metode yang diterapkan dalam analisis ini adalah Naive Bayes, yaitu suatu teknik klasifikasi berbasis probabilitas. Secara umum, metode ini digunakan untuk memperkirakan kemungkinan suatu data termasuk ke dalam kelas tertentu dengan mempertimbangkan nilai dari setiap fitur yang dimiliki. Setelah seluruh probabilitas dihitung, sistem akan menentukan kelas dengan nilai peluang paling tinggi sebagai hasil prediksi.

Pendekatan ini mengacu pada Teorema Bayes, yang secara matematis dapat dinyatakan sebagai berikut:

$$P(C|X) = \frac{P(X|C) \cdot P(C)}{P(X)}$$

Dalam implementasinya, nilai $P(X)$ bersifat konstan untuk setiap kelas, sehingga tidak memengaruhi proses perbandingan. Oleh karena itu, perhitungan dapat disederhanakan menjadi:

$$P(C|X) = P(C) \cdot P(X|C)$$

Apabila data memiliki lebih dari satu fitur, maka perhitungan probabilitas dilakukan dengan mengalikan seluruh peluang dari masing-masing fitur terhadap kelas yang diuji.

$$P(C|X) = P(C) \cdot P(x_1|C) \cdot P(x_2|C) \cdot \dots \cdot P(x_n|C)$$



## Asumsi Naive Bayes
Naive Bayes mengasumsikan bahwa setiap fitur bersifat independen (tidak saling bergantung).

Contoh pada dataset Bank Marketing:

* age dianggap tidak bergantung pada balance
* balance dianggap tidak bergantung pada duration
* duration dianggap tidak bergantung pada campaign

Walaupun dalam kenyataannya beberapa fitur bisa saling berkaitan (misalnya usia bisa mempengaruhi saldo), asumsi ini tetap digunakan agar perhitungan probabilitas menjadi lebih sederhana dan efisien.

## Gaussian Naive Bayes
Metode yang digunakan adalah Gaussian Naive Bayes yang diimplementasikan melalui Python Script menggunakan scikit-learn.

Metode ini digunakan karena:

* Dataset memiliki fitur numerik seperti age, balance, duration
* Data kategorikal telah diubah menjadi numerik melalui encoding

Rumus distribusi Gaussian:

$$P(x|c)=\frac{1}{\sqrt{2\pi\sigma^2}} \, e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$

Model akan menghitung probabilitas untuk menentukan apakah nasabah akan berlangganan deposito (deposit) atau tidak.

# Preprocessing Data
Sebelum data digunakan dalam model, dilakukan beberapa tahap preprocessing agar data siap diproses dengan baik.
## Missing Value
Data yang kosong perlu ditangani karena tidak bisa langsung diproses oleh model.

Pada dataset Bank Marketing:

* Data numerik seperti:
    * age, balance, duration, campaign
        * diisi menggunakan mean
* Data kategorikal seperti:
    * job, marital, education, contact
        * diisi dengan nilai yang paling sering muncul
* Kolom target:
    * y (deposit)
        * tidak diubah sembarangan

## Encoding (Internal Scripting)
Meskipun KNIME menyediakan node One to Many, pada workflow ini saya melakukan proses encoding langsung di dalam script Python menggunakan teknik One-Hot Encoding melalui fungsi `pd.get_dummies(X)`.

* Fungsi: Mengubah data kategorikal (seperti job, marital, dan education) menjadi kolom numerik biner ($0$ dan $1$).
* Keunggulan: Pendekatan ini menjaga nilai biner tetap murni dan terbukti menghasilkan akurasi yang lebih baik dibandingkan menggunakan node eksternal yang kemudian dinormalisasi.
* Target Mapping: Kolom target deposit secara manual dipetakan menggunakan fungsi .map({"yes": 1, "no": 0}) agar sesuai dengan format yang dibutuhkan model klasifikasi.

## Normalisasi
Normalisasi dilakukan untuk menyamakan skala antar fitur numerik.

Pada dataset ini:

* balance bisa sangat besar
* age relatif kecil
* duration bervariasi

Jika tidak dinormalisasi, model bisa bias terhadap fitur tertentu.

Rumus Min-Max Normalization:
$$x' = \frac{x - x_{min}}{x_{max} - x_{min}}x`$$

Dengan normalisasi:

* Semua fitur berada pada skala yang sama (0–1)
* Model dapat bekerja lebih optimal

## Data Splitting (Stratification)
Tahap akhir preprocessing adalah pembagian data menjadi $70\%$ data latih dan $30\%$ data uji dengan parameter `stratify=y`.
* Signifikansi: Teknik stratifikasi memastikan bahwa proporsi kelas "yes" dan "no" pada data uji tetap mewakili distribusi asli dari total $11.162$ baris dataset, sehingga hasil evaluasi pada Confusion Matrix menjadi valid.

# Tahapan Analisis
## Workflow KNIME
![image](https://hackmd.io/_uploads/BJvgEQDRZe.png)

## Penjelasan Node
### A. CSV Reader
Node CSV Reader digunakan untuk membaca dataset dari file berformat CSV ke dalam workflow.

Pada node ini:

* File dataset dipilih dari direktori penyimpanan
* Delimiter (pemisah, biasanya koma) disesuaikan
* Tipe data tiap kolom dapat dideteksi otomatis atau diatur manual

![image](https://hackmd.io/_uploads/Bkxm4Qv0Wg.png)

### B. Mising Value
Node Missing Value digunakan untuk menangani data kosong. Nilai kosong perlu ditangani karena dapat menyebabkan error pada proses berikutnya, terutama saat normalisasi.

Pada node ini:

* Kolom numerik diisi menggunakan Mean agar distribusi data tetap stabil
* Kolom kategorikal diisi menggunakan Most Frequent Value (modus) agar tetap representatif
* Kolom target (deposit) tidak diubah sembarangan agar tidak merusak label asli

![image](https://hackmd.io/_uploads/HJoXkNL0-l.png)

### C. Color Manager
Node Color Manager hanya digunakan untuk membedakan kelas target deposit.

Pada node ini:
* y = yes (deposit) → misalnya hijau
* y = no (tidak deposit) → misalnya merah

![image](https://hackmd.io/_uploads/SJnvNXP0Wl.png)


### D. Table View
Node Table View digunakan untuk menampilkan isi data yang telah dibaca.
![image](https://hackmd.io/_uploads/S1NGb4URbg.png)

### E. Normalizer
Node Normalizer digunakan untuk menyamakan skala nilai numerik.

Pada dataset bank:

* Nilai seperti:
* balance (bisa ribuan)
* age (puluhan)
* credit_score (ratusan)
* memiliki skala yang berbeda

Pada node ini:

* Digunakan metode seperti:
    * Min-Max (0–1) atau
    * Z-score
* Semua fitur numerik disetarakan skalanya

![image](https://hackmd.io/_uploads/ryPvmE80Zx.png)


### F. Python Script
Node Python Script digunakan untuk membangun model Gaussian Naive Bayes dengan memanfaatkan library scikit-learn. Pada tahap ini, data yang telah diproses di KNIME akan diimpor ke lingkungan Python, kemudian digunakan untuk melakukan proses pelatihan model (training), melakukan prediksi, serta menghitung nilai probabilitas dari hasil prediksi tersebut.

![image](https://hackmd.io/_uploads/Hkzpg4wRWg.png)


Kode yang digunakan:
```
import knime.scripting.io as knio
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB

# ambil data
df = knio.input_tables[0].to_pandas()

# pisahkan target
X = df.drop("deposit", axis=1)
y = df["deposit"]

# encoding
X = pd.get_dummies(X)

# target jdi angka
y = y.astype(str).str.strip().str.lower().map({"yes": 1, "no": 0})

# handle mising value
X = X.fillna(0)
y = y.fillna(0)

#split data
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.3,
    random_state=42,
    stratify=y
)

# model naive bayes
model = GaussianNB()
model.fit(X_train, y_train)

# prediksi
prediction = model.predict(X_test)
probability = model.predict_proba(X_test)

# output (scorer + probabilitas)\
output = pd.DataFrame({
    "Actual": y_test.astype(int).values,
    "Prediction": prediction.astype(int),
    "Prob_No": probability[:, 0],
    "Prob_Yes": probability[:, 1]
})

# kirim ke knime
knio.output_tables[0] = knio.Table.from_pandas(output)
```

#### Penjelasan Kode
**1. Import library**

```
import knime.scripting.io as knio
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
```

Penjelasan:

* `knio` untuk mengambil dan mengirim data dari/ke KNIME
* `pandas` untuk mengolah data dalam bentuk tabel
* `train_test_split` untuk membagi data training dan testing
* `GaussianNB` algoritma Naive Bayes untuk data numerik

**2. Ambil data**

```
df = knio.input_tables[0].to_pandas()
```

Penjelasan:

* Mengambil data dari KNIME lalu diubah menjadi DataFrame agar bisa diolah di Python

**3. Pisahkan fitur dan target**

```
X = df.drop("deposit", axis=1)
y = df["deposit"]
```

Penjelasan:

* `X` berisi semua data selain target
* `y` berisi target (deposit) yang akan diprediksi



**4. Encoding data kategori**

```
X = pd.get_dummies(X)
```

Penjelasan:

* Mengubah data kategori (teks) menjadi angka
* Contoh: `job = admin` jadi kolom baru seperti `job_admin = 1`
* Hal ini penting karena model tidak bisa membaca teks

Contoh isalnya:
```
job = admin.
job = technician
job = services
```

Setelah encoding jadi:
| job_admin. | job_technician | job_services |
| ---------- | -------------- | ------------ |
| 1          | 0              | 0            |
| 0          | 1              | 0            |
| 0          | 0              | 1            |




**5. Mengubah target menjadi angka**

```
y = y.astype(str).str.strip().str.lower().map({"yes": 1, "no": 0})
```

Penjelasan:

* Mengubah nilai target:
    * `yes` = 1
    * `no` = 0
* Supaya bisa diproses oleh model

**6. Menangani missing value**

```
X = X.fillna(0)
y = y.fillna(0)
```

Penjelasan:

* Mengisi nilai kosong dengan 0
* Agar tidak terjadi error saat proses training

**7. Membagi data** 

```
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.3,
    random_state=42,
    stratify=y
)
```

Penjelasan:

* Data dibagi menjadi:
    * 70% training
    * 30% testing
* `random_state=42` supaya hasil konsisten
* `stratify=y` menjaga proporsi data tetap seimbang

**8. Membuat model**

```
model = GaussianNB()
model.fit(X_train, y_train)
```

Penjelasan:

* Membuat model Naive Bayes
* Melatih model menggunakan data training

**9. Prediksi**

```
prediction = model.predict(X_test)
probability = model.predict_proba(X_test)
```

Penjelasan:

* `prediction` Kode ini digunakan untuk memprediksi data testing yang sudah dipisahkan sebelumnya.
Hasil dari prediksi ini berupa kelas akhir, yaitu 0 atau 1.
    * 0 : tidak melakukan deposit
    * 1 : melakukan deposit
* `probability` Kode ini digunakan untuk menghitung probabilitas dari setiap kelas. Artinya, model tidak hanya memberikan hasil prediksi, tetapi juga tingkat keyakinannya. peluang masing-masing kelas (no / yes)

Contoh hasil:
| Prob_No | Prob_Yes | Prediction |
| ------- | -------- | ---------- |
| 0.034   | 0.966    | 1          |
| 1.000   | 0.000    | 0          |


**10. Menyusun output**

```
output = pd.DataFrame({
    "Actual": y_test.astype(int).values,
    "Prediction": prediction.astype(int),
    "Prob_No": probability[:, 0],
    "Prob_Yes": probability[:, 1]
})
```

Penjelasan:

* Menggabungkan:
    * nilai asli
    * hasil prediksi
    * probabilitas
* Supaya mudah dianalisis

**11. Kirim hasil ke KNIME**

```
knio.output_tables[0] = knio.Table.from_pandas(output)
```

Penjelasan:

* Mengirim hasil kembali ke KNIME untuk ditampilkan di node berikutnya

Program ini digunakan untuk melakukan klasifikasi data menggunakan algoritma Naive Bayes. Data terlebih dahulu diproses melalui tahap encoding dan pembersihan, kemudian dibagi menjadi data training dan testing. Model dilatih menggunakan data training, lalu digunakan untuk memprediksi data testing. Hasil akhir berupa nilai prediksi dan probabilitas yang kemudian ditampilkan di KNIME.

#### Hasil Akhir/Output
![image](https://hackmd.io/_uploads/HJZ-r4vR-l.png)




### G. Scorer
Node Scorer digunakan untuk mengevaluasi model dalam memprediksi apakah nasabah akan berlangganan deposito.

Pada node ini:

* Membandingkan:
    * Prediksi model
    * Nilai asli (y: yes/no)
* Menghasilkan:
    * Accuracy
    * Precision
    * Recall
    * Confusion Matrix

![image](https://hackmd.io/_uploads/r1q4VEIAbl.png)

![image](https://hackmd.io/_uploads/Sy_vSVP0Wl.png)

![image](https://hackmd.io/_uploads/Sk_HjEDRWe.png)




# Hasil
## Hasil Prediksi Model
Contoh hasil:


| RowID | Actual | Prediction | Prob_No | Prob_Yes |
| ----- | ------ | ---------- | ------- | -------- |
| Row0  | 1      | 1          | 0       | 1        |
| Row1  | 1      | 0          | 0.997   | 0.003    |

## Confusion Matrix
| Actual \ Predicted | 1   | 0    |
| ------------------ | --- | ---- |
| 1                  | 901 | 686  |
| 0                  | 256 | 1506 |


# Perhitungan Evaluasi
Setelah model selesai melakukan prediksi, langkah berikutnya adalah mengevaluasi seberapa baik performa model tersebut. Evaluasi ini penting untuk mengetahui apakah model mampu melakukan klasifikasi dengan baik, bukan hanya sekadar menghasilkan prediksi.

Untuk itu digunakan beberapa metrik evaluasi, yaitu Accuracy, Precision, dan Recall. Masing-masing metrik memiliki fungsi yang berbeda sehingga perlu dianalisis secara bersama.



## Accuracy
**Rumus:**
$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$

**Perhitungan:**
$$Accuracy = \frac{901 + 1506}{901 + 1506 + 256 + 686}$$$$Accuracy = \frac{2407}{3349} = 0.719 (\approx 71.9\%)$$

**Hasil:**
$$0.719 (71.9\%)$$

**Penjelasan:**.
Accuracy digunakan untuk mengukur tingkat ketepatan model secara keseluruhan dengan membandingkan jumlah prediksi yang benar terhadap total seluruh data yang diuji. Nilai 71.9% menunjukkan bahwa dari 3.349 data testing, terdapat 2.407 data yang berhasil diklasifikasikan dengan benar oleh model.


## Precision
**Rumus:**
$$Precision = \frac{TP}{TP + FP}$$

**Perhitungan:**
$$Precision = \frac{901}{901 + 256}$$$$Precision = \frac{901}{1157} = 0.779 (\approx 77.9\%)$$

**Hasil:**

$$Precision (kelas 1) = 0.779 (77.9\%)$$

**Penjelasan:**
Precision mengukur seberapa tepat prediksi model ketika menyatakan seorang nasabah akan melakukan deposit. Nilai 77.9% berarti dari seluruh nasabah yang diprediksi akan deposit (kelas 1), sekitar 77.9% di antaranya memang benar-benar melakukan deposit secara aktual. Hal ini penting untuk efisiensi biaya pemasaran agar promo tidak salah sasaran kepada nasabah yang sebenarnya tidak berminat.

## Recall
**Rumus:**
$$Recall = \frac{TP}{TP + FN}$$

**Perhitungan:**
$$Recall = \frac{901}{901 + 686}$$$$Recall = \frac{901}{1587} = 0.568 (\approx 56.8\%)$$

**Hasil:**
$$Recall (kelas 1) = 0.568 (56.8\%)$$

**Penjelasan:**
Recall menunjukkan kemampuan model dalam mendeteksi seluruh nasabah yang benar-benar melakukan deposit. Nilai 56,8% berarti model hanya berhasil menemukan sekitar setengah dari nasabah yang seharusnya deposit. Dalam konteks perbankan, hal ini menunjukkan masih banyak nasabah potensial yang terlewat oleh model.

## Kesimpulan Evaluasi
Berdasarkan hasil di atas, dapat disimpulkan bahwa:

* `Accuracy (71.9%)` menunjukkan model Naive Bayes memiliki performa yang cukup stabil dalam mengklasifikasikan data bank marketing secara umum.
* `Precision (77.9%)` menunjukkan tingkat kepercayaan yang tinggi saat model menebak nasabah akan deposit.
* `Recall (56.8%)` menjadi poin yang perlu ditingkatkan, karena model masih sering melewatkan nasabah yang sebenarnya berpotensi deposit (banyak False Negative).

Secara keseluruhan, model ini sudah layak digunakan sebagai dasar analisis awal, namun perlu pengembangan lebih lanjut pada fitur-fitur tertentu untuk meningkatkan sensitivitas (recall) agar tidak banyak peluang nasabah yang hilang.

# Analisis
Model Naive Bayes ini memiliki accuracy 71,9% yang menunjukkan performa cukup baik dalam mengklasifikasikan nasabah. Precision sebesar 77,9% berarti prediksi nasabah yang akan deposit cukup akurat.

Namun, recall hanya 56,8% sehingga masih banyak nasabah potensial yang tidak terdeteksi (false negative). Hal ini wajar karena Naive Bayes mengasumsikan setiap fitur saling independen.

Secara keseluruhan, model ini cukup layak digunakan sebagai dasar analisis awal target pemasaran bank.

# Kesimpulan
Berdasarkan hasil analisis dan pengujian yang telah dilakukan, dapat disimpulkan bahwa metode Naive Bayes dapat diimplementasikan untuk memprediksi minat nasabah terhadap produk deposit dengan hasil yang cukup stabil. Model ini menunjukkan keunggulan sebagai algoritma yang sederhana, cepat dalam proses komputasi, dan tidak membutuhkan arsitektur yang terlalu kompleks untuk dijalankan pada dataset perbankan.

Meskipun memiliki keterbatasan pada asumsi independensi fitur di mana model menganggap setiap informasi nasabah tidak saling berhubungan denganhasil akurasi sebesar 71.9% menunjukkan bahwa model ini tetap layak digunakan sebagai instrumen analisis awal. Dengan tingkat presisi yang mencapai 77.9%, bank dapat lebih efektif dalam menentukan target nasabah, sehingga strategi pemasaran menjadi lebih tepat sasaran dan efisien dalam penggunaan sumber daya.