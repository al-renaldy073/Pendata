---
title: Analisa Data Menggunakan Random Forest

---

# Analisa Data Menggunakan Random Forest
# Deskripsi Proyek
Pada tugas ini dilakukan analisis perbandingan antara algoritma klasifikasi Decision Tree dan Random Forest menggunakan aplikasi KNIME Analytics Platform.

Dataset yang digunakan adalah dataset prediksi penyakit paru-paru yang diperoleh dari Kaggle. Dataset ini berisi data kesehatan dan gaya hidup seseorang seperti usia, jenis kelamin, kebiasaan merokok, olahraga, begadang, serta beberapa faktor lain yang dapat mempengaruhi risiko terkena penyakit paru-paru.

Target klasifikasi yang digunakan adalah:

`Hasil`

Keterangan:

```
Ya = terkena penyakit paru-paru
Tidak = tidak terkena penyakit paru-paru
```

Tujuan penelitian ini adalah:

* Membuat model klasifikasi menggunakan Decision Tree
* Membuat model klasifikasi menggunakan Random Forest
* Membandingkan performa kedua algoritma
* Mengevaluasi hasil prediksi menggunakan confusion matrix dan accuracy model

# Informasi Dataset


**Nama Dataset**: Dataset Prediksi Terkena Penyakit Paru-Paru
**Sumber**: Kaggle (https://www.kaggle.com/datasets/andot03bsrc/dataset-predic-terkena-penyakit-paruparu)
**Jumlah Data**: 30000 baris (records)
**Fitur Dataset**: 
| No | Nama Atribut     | Keterangan                            |
| -- | ---------------- | ------------------------------------- |
| 1  | Usia             | Umur responden                        |
| 2  | Jenis Kelamin    | Pria atau Wanita              |
| 3  | Merokok          | Kebiasaan merokok                     |
| 4  | Begadang         | Kebiasaan tidur larut malam           |
| 5  | Olahraga         | Intensitas olahraga                   |
| 6  | Penyakit Bawaan  | Riwayat penyakit sebelumnya           |
| 7  | Konsumsi Alkohol | Kebiasaan konsumsi alkohol            |
| 8  | Polusi Udara     | Tingkat paparan polusi                |
| 9  | Pekerjaan        | Jenis pekerjaan responden             |
| 10 | Hasil            | Terkena penyakit paru-paru atau tidak |

**Target Dataset**:
Target atau class pada dataset adalah:
| Target | Keterangan                       |
| ------ | -------------------------------- |
| Ya     | Terkena penyakit paru-paru       |
| Tidak  | Tidak terkena penyakit paru-paru |

Dataset ini digunakan untuk melakukan prediksi terhadap kemungkinan seseorang terkena penyakit paru-paru berdasarkan beberapa faktor kesehatan dan gaya hidup. Dataset termasuk ke dalam kategori klasifikasi karena memiliki target berupa status terkena penyakit paru-paru atau tidak.

Tujuan penggunaan dataset ini adalah:
1. Menganalisis faktor-faktor yang mempengaruhi penyakit paru-paru.
1. Melakukan klasifikasi terhadap kemungkinan terkena penyakit paru-paru.
1. Membandingkan performa algoritma Decision Tree dan Random Forest.
1. Menentukan algoritma dengan tingkat akurasi terbaik.
Dataset ini digunakan untuk melakukan prediksi terhadap kemungkinan seseorang terkena penyakit paru-paru berdasarkan beberapa faktor kesehatan dan gaya hidup. Dataset termasuk ke dalam kategori klasifikasi karena memiliki target berupa status terkena penyakit paru-paru atau tidak.

Tujuan penggunaan dataset ini adalah:
1. Menganalisis faktor-faktor yang mempengaruhi penyakit paru-paru.
1. Melakukan klasifikasi terhadap kemungkinan terkena penyakit paru-paru.
1. Membandingkan performa algoritma Decision Tree dan Random Forest.
1. Menentukan algoritma dengan tingkat akurasi terbaik.

# Metode Random Forest
Random Forest merupakan metode machine learning yang dikembangkan dari Decision Tree dengan menggunakan banyak pohon keputusan (tree) untuk menghasilkan prediksi yang lebih akurat dan stabil. Setiap tree akan melakukan klasifikasi data, kemudian hasil akhir ditentukan berdasarkan voting terbanyak dari seluruh tree.

Pada penelitian ini Random Forest digunakan untuk memprediksi kemungkinan seseorang terkena penyakit paru-paru berdasarkan data kesehatan dan gaya hidup seperti usia, jenis kelamin, kebiasaan merokok, aktivitas olahraga, begadang, asuransi, dan penyakit bawaan.

Setiap pohon keputusan pada Random Forest akan melakukan klasifikasi terhadap data, kemudian hasil akhir ditentukan berdasarkan voting terbanyak dari seluruh pohon keputusan. Metode ini sangat cocok digunakan pada dataset penyakit paru-paru karena dataset didominasi oleh atribut kategorikal dan memiliki banyak faktor yang mempengaruhi hasil klasifikasi.

# Perbandingan Random Forest dan Decision Tree
| Aspek              | Decision Tree                    | Random Forest                      |
| ------------------ | -------------------------------- | ---------------------------------- |
| Struktur Model     | Menggunakan satu pohon keputusan | Menggunakan banyak pohon keputusan |
| Akurasi            | Cukup baik                       | Lebih tinggi dan stabil            |
| Overfitting        | Mudah terjadi overfitting        | Mengurangi overfitting             |
| Kecepatan Training | Lebih cepat                      | Sedikit lebih lambat               |
| Kompleksitas       | Sederhana dan mudah dipahami     | Lebih kompleks                     |
| Interpretasi Model | Mudah divisualisasikan           | Sulit divisualisasikan             |
| Stabilitas Model   | Kurang stabil                    | Lebih stabil                       |
| Cocok Untuk        | Dataset sederhana                | Dataset kompleks dan besar         |

# Tahapan Analisis
## Workflow Knime

![image](https://hackmd.io/_uploads/rkaKIarJGx.png)


```
CSV Reader
    │
    ▼
Table Partitioner
    │ ├───────────► Python Script Training Decision Tree
    │ │
    │ └───────────► Python Script Testing Decision Tree
    │                              │
    │                              ▼
    │                Scorer (JavaScript) Decision Tree
    │  
    ├──────────────► Python Script Training Random Forest
    │
    └──────────────► Python Script Testing Random Forest
                                  │
                                  ▼
                     Scorer (JavaScript) Random Forest
```

### CSV Reader
Node CSV Reader digunakan untuk membaca dataset dari file berformat CSV ke dalam workflow.

Pada node ini:
* File dataset dipilih dari direktori penyimpanan
* Delimiter (pemisah, koma) disesuaikan
* Tipe data tiap kolom dapat dideteksi otomatis atau diatur manual

![image](https://hackmd.io/_uploads/rJ8N9aE1ze.png)
![image](https://hackmd.io/_uploads/Hy1L9aVJMx.png)


### Table Partitioner
Node Table Partitioner digunakan untuk membagi dataset menjadi dua bagian, yaitu:

* data training
* data testing

Pada pengujian ini, pembagian data dilakukan dengan perbandingan:

```
80% data training
20% data testing
```

Data training digunakan untuk melatih model, sedangkan data testing digunakan untuk menguji hasil prediksi model.

Output dari node ini terdiri dari dua bagian:

```
First Partition  = data training
Second Partition = data testing
```
Data training akan masuk ke node Python Script untuk proses training model. Data testing akan masuk ke node Python Script untuk proses prediksi.

Metode sampling yang digunakan adalah:

`Stratified Sampling`

Penggunaan Stratified Sampling bertujuan agar proporsi class Ya dan Tidak pada atribut Hasil tetap seimbang pada data training maupun data testing sehingga proses klasifikasi Decision Tree dan Random Forest menjadi lebih akurat.

Group Column yang dipilih adalah atribut:

`Hasil`

Group Column bertujuan menentukan atribut target yang dijadikan dasar pembagian data pada proses Stratified Sampling. Pada pengujian ini atribut yang dipilih adalah Hasil sehingga proporsi class Ya dan Tidak tetap seimbang pada data training dan data testing.

![image](https://hackmd.io/_uploads/By6_2aV1Mg.png)

![image](https://hackmd.io/_uploads/Hyi52TE1Mg.png)

![image](https://hackmd.io/_uploads/rkvs26EkGg.png)


### Node Decision Tree
Bagian Decision Tree digunakan untuk membangun model klasifikasi dengan algoritma Decision Tree.

Pada bagian ini terdapat tiga node utama:
* Python Script (legacy) Training Decision Tree : Yang Atas
* Python Script (legacy) Testing Decision Tree : Yang Bawah
* Scorer (JavaScript) Decision Tree

![image](https://hackmd.io/_uploads/BkTgUTHJMg.png)


#### Python Script Training Decision Tree
Node Python Script Training Decision Tree digunakan untuk melatih model Decision Tree menggunakan `data training (80%)` dari Table Partitioner pada dataset prediksi penyakit paru-paru.

Pada node ini dilakukan preprocessing data kategorikal, pembuatan model Decision Tree, proses training, dan penyimpanan model menggunakan pickle.

**Kode lengkap:**
```
import pandas as pd
import os
import pickle
import numpy as np

from sklearn.tree import DecisionTreeClassifier
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
from sklearn.impute import SimpleImputer

# Ambil data training
df = input_table_1.copy()

# Target
target_col = "Hasil"

# Bersihkan data
df = df.replace("?", np.nan)

for col in df.columns:
    df[col] = df[col].astype(str).str.strip()
    df[col] = df[col].replace("nan", np.nan)

# Hapus kolom nomor
if "No" in df.columns:
    df = df.drop(columns=["No"])

# Kolom kategorikal
categorical_columns = [
    "Usia",
    "Jenis_Kelamin",
    "Merokok",
    "Bekerja",
    "Rumah_Tangga",
    "Aktivitas_Begadang",
    "Aktivitas_Olahraga",
    "Asuransi",
    "Penyakit_Bawaan"
]

# Hapus target kosong
df = df.dropna(subset=[target_col])

# Pisahkan fitur dan target
X_train = df.drop(columns=[target_col])
y_train = df[target_col].astype(str)

# Kolom kategorikal yang dipakai
categorical_cols = [
    col for col in categorical_columns
    if col in X_train.columns
]

# Encoder
try:
    encoder = OneHotEncoder(
        handle_unknown="ignore",
        sparse_output=False
    )
except TypeError:
    encoder = OneHotEncoder(
        handle_unknown="ignore",
        sparse=False
    )

# Transformer kategorikal
categorical_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("encoder", encoder)
])

# Preprocessor
preprocessor = ColumnTransformer(
    transformers=[
        ("cat", categorical_transformer, categorical_cols)
    ]
)

# Model Decision Tree
decision_tree = DecisionTreeClassifier(
    criterion="gini",
    min_samples_leaf=2,
    random_state=42
)

# Pipeline
model_pipeline = Pipeline(steps=[
    ("preprocessing", preprocessor),
    ("decision_tree", decision_tree)
])

# Training
model_pipeline.fit(X_train, y_train)

# Simpan model
model_folder = os.path.join(
    os.path.expanduser("~"),
    "knime_model"
)

os.makedirs(model_folder, exist_ok=True)

model_path = os.path.join(
    model_folder,
    "decision_tree_paru_paru_model.pkl"
)

with open(model_path, "wb") as file:
    pickle.dump(model_pipeline, file)

# Output
output_table_1 = pd.DataFrame({
    "Status": ["Decision Tree paru-paru berhasil dibuat"],
    "Model Path": [model_path],
    "Jumlah Data Training": [len(df)],
    "Jumlah Fitur": [X_train.shape[1]]
})
```

**Penjelasan kode:**

1. Import Library
    ```
    import pandas as pd
    import os
    import pickle
    import numpy as np
    ```
    * `pandas`  mengolah data tabel/dataframe
    * `os`  mengatur folder dan lokasi penyimpanan file
    * `pickle`  menyimpan model machine learning
    * `numpy`  menangani nilai numerik dan missing value

    ```
    from sklearn.tree import DecisionTreeClassifier
    from sklearn.pipeline import Pipeline
    from sklearn.compose import ColumnTransformer
    from sklearn.preprocessing import OneHotEncoder
    from sklearn.impute import SimpleImputer
    ```

    * `DecisionTreeClassifier` algoritma Decision Tree
    * `Pipeline` menggabungkan preprocessing + model
    * `ColumnTransformer` memilih kolom tertentu untuk diproses
    * `OneHotEncoder` mengubah data kategori menjadi angka
    * `SimpleImputer` mengisi data kosong
2. Mengambil Data Training
    
    ```
    df = input_table_1.copy()
    ```
    Mengambil data dari KNIME lalu disalin ke variabel df.

    Kenapa pakai .copy()?

    * Agar data asli tidak berubah saat diproses.

3. Menentukan Target
    ```
    target_col = "Hasil"
    ```
    Menentukan kolom target/class.

    Kolom "Hasil" adalah:

    * label prediksi
4. Membersihkan Data
    ```
    df = df.replace("?", np.nan)
    ```
    Mengubah simbol ? menjadi NaN (data kosong).
    
    * ? dianggap missing value
    * sklearn lebih mudah memproses NaN
    
    ```
    for col in df.columns:
        df[col] = df[col].astype(str).str.strip()
        df[col] = df[col].replace("nan", np.nan)
    ```
    Membersihkan semua kolom.

    * `astype(str)` ubah data jadi teks
    * `str.strip()` hapus spasi kosong
    * `"nan"` dikembalikan menjadi NaN
5. Menghapus Kolom Nomor
    ```
    if "No" in df.columns:
        df = df.drop(columns=["No"])
    ```
    Menghapus kolom nomor urut supaya tidak mempengaruhi prediksi dan hanya identitas data
6. Menentukan Kolom Kategorikal
    ```
    categorical_columns = [
        "Usia",
        "Jenis_Kelamin",
        "Merokok",
        "Bekerja",
        "Rumah_Tangga",
        "Aktivitas_Begadang",
        "Aktivitas_Olahraga",
        "Asuransi",
        "Penyakit_Bawaan"
    ]
    ```
    Daftar fitur kategorikal.
    Karena semua berisi teks/kategori:

    * Ya/Tidak
    * Pria/Wanita
    * Ringan/Berat
7. Menghapus Target Kosong
    ```
    df = df.dropna(subset=[target_col])
    ```
    Menghapus baris yang targetnya kosong, Karena model tidak bisa belajar tanpa label target.
8. Memisahkan Fitur dan Target
    ```
    X_train = df.drop(columns=[target_col])
    y_train = df[target_col].astype(str)
    ```

    Memisahkan:

    * `X_train` fitur/input
    * `y_train` target/output

    Contoh:
    | Usia   | Merokok | Hasil   |
    | ------ | ------- | ------- |
    | Dewasa | Ya      | Positif |

    Maka:

    * `X_train` Usia, Merokok
    * `y_train` Hasil
9. Memilih Kolom Kategorikal yang Ada
    ```
    categorical_cols = [
        col for col in categorical_columns
        if col in X_train.columns
    ]
    ```
    Memastikan hanya kolom yang benar-benar ada yang digunakan untuk enghindari error jika ada kolom hilang.
10. Membuat Encoder
    ```
    try:
        encoder = OneHotEncoder(
            handle_unknown="ignore",
            sparse_output=False
        )
    ```

    Mengubah data kategori menjadi angka.
    Contoh:

    | Jenis Kelamin |
    | ------------- |
    | Laki-laki     |
    | Perempuan     |

    Menjadi:
    | Laki-laki | Perempuan |
    | --------- | --------- |
    | 1         | 0         |
    | 0         | 1         |

    Penjelasan Parameter
    * handle_unknown="ignore" : Jika ada kategori baru saat testing program tidak error
    * sparse_output=False :Hasil encoder menjadi array biasa.
11. Membuat Transformer
    ```
    SimpleImputer(strategy="most_frequent")
    ```
    Mengisi data kosong dengan nilai yang paling sering muncul.

    Contoh:
    | Merokok |
    | ------- |
    | Ya      |
    | Tidak   |
    | Ya      |
    | kosong  |

    Menjadi:
    | Merokok |
    | ------- |
    | Ya      |
    | Tidak   |
    | Ya      |
    | Ya      |
12. Membuat Preprocessor
    ```
    preprocessor = ColumnTransformer(
        transformers=[
            ("cat", categorical_transformer, categorical_cols)
        ]
    )
    ```
    Menerapkan preprocessing hanya pada kolom kategorikal.
13. Membuat Model Decision Tree
    ```
    decision_tree = DecisionTreeClassifier(
        criterion="gini",
        min_samples_leaf=2,
        random_state=42
    )
    ```
    Membuat model klasifikasi Decision Tree.
    Penjelasan Parameter
    * `criterion="gini"` : Menggunakan metode Gini Index untuk menentukan percabangan terbaik.
    * 
    * `min_samples_leaf=2` : Minimal data pada daun pohon = 2.
        Tujuan: 
        * mengurangi overfitting
        * pohon tidak terlalu detail
    * `random_state=42` : Agar hasil training selalu sama.
14. Membuat Pipeline
    ```
    model_pipeline = Pipeline(steps=[
        ("preprocessing", preprocessor),
        ("decision_tree", decision_tree)
    ])
    ```
    Menggabungkan:

    * preprocessing
    * model training

    Menjadi satu alur otomatis.
15. Training Model
    ```
    model_pipeline.fit(X_train, y_train)
    ```
    Melatih model menggunakan data training.
    Proses:
    * data dibersihkan
    * diencoding
    * Decision Tree belajar pola data
16. Membuat Folder Penyimpanan
    ```
    model_folder = os.path.join(
        os.path.expanduser("~"),
        "knime_model"
    )
    ```
    Menentukan folder penyimpanan model.
17. Menentukan Lokasi Model
    ```
    model_path = os.path.join(
        model_folder,
        "decision_tree_paru_paru_model.pkl"
    )
    ```
    Nama file model yang disimpan, dengan Format `.pkl`
18. Menyimpan Model
    ```
    with open(model_path, "wb") as file:
        pickle.dump(model_pipeline, file)
    ```
    Menyimpan model ke file supaya model bisa dipakai kembali tanpa training ulang.
19. Output KNIME
    ```
    output_table_1 = pd.DataFrame({
        "Status": ["Decision Tree paru-paru berhasil dibuat"],
        "Model Path": [model_path],
        "Jumlah Data Training": [len(df)],
        "Jumlah Fitur": [X_train.shape[1]]
    })
    ```
    Menampilkan hasil proses ke output KNIME.
    
Kode ini membuat output ke KNIME. Output berisi status model, lokasi model, jumlah data training, target, dan jumlah fitur.
![image](https://hackmd.io/_uploads/ryF5z0ByMe.png)


#### Python Script Testing Decision Tree
Node Python Script Testing Decision Tree digunakan untuk menguji model Decision Tree menggunakan data testing dari Table Partitioner.

Pada node ini dilakukan pembersihan data, pemanggilan model yang telah disimpan, proses prediksi penyakit paru-paru, dan menampilkan hasil aktual serta hasil prediksi pada output KNIME Analytics Platform.

**Kode lengkap:**
```
import pandas as pd
import os
import pickle
import numpy as np

# Ambil data testing
df = input_table_1.copy()

# Target
target_col = "Hasil"

# Bersihkan data
df = df.replace("?", np.nan)

for col in df.columns:
    df[col] = df[col].astype(str).str.strip()
    df[col] = df[col].replace("nan", np.nan)

# Hapus kolom nomor
if "No" in df.columns:
    df = df.drop(columns=["No"])

# Kolom kategorikal
categorical_columns = [
    "Usia",
    "Jenis_Kelamin",
    "Merokok",
    "Bekerja",
    "Rumah_Tangga",
    "Aktivitas_Begadang",
    "Aktivitas_Olahraga",
    "Asuransi",
    "Penyakit_Bawaan"
]

# Hapus target kosong
df = df.dropna(subset=[target_col])

# Pisahkan fitur dan target
X_test = df.drop(columns=[target_col])
y_test = df[target_col].astype(str)

# Load model
model_folder = os.path.join(
    os.path.expanduser("~"),
    "knime_model"
)

model_path = os.path.join(
    model_folder,
    "decision_tree_paru_paru_model.pkl"
)

with open(model_path, "rb") as file:
    loaded_model = pickle.load(file)

# Prediksi
prediction = loaded_model.predict(X_test)

# Output
output_table_1 = pd.DataFrame({
    "Actual": y_test.values,
    "Prediction": prediction
})
```

**Penjelasan kode:**
1. Import Library
    ```
    import pandas as pd
    import os
    import pickle
    import numpy as np
    ```
    * `pandas` mengolah data tabel
    * `os` akses folder file model
    * `pickle` memuat model yang sudah disimpan
    * `numpy` menangani missing value (NaN)
2. Mengambil Data Testing
    ```
    df = input_table_1.copy()
    ```
    Mengambil data testing dari KNIME lalu disalin ke df, Agar data asli tidak berubah saat diproses.
3. Menentukan Target
    ```
    target_col = "Hasil"
    ```
    Menentukan kolom label/hasil sebenarnya (ground truth).
4. Membersihkan Data
    ```
    df = df.replace("?", np.nan)
    ```
    Mengubah tanda ? menjadi nilai kosong (NaN).
    ```
    for col in df.columns:
        df[col] = df[col].astype(str).str.strip()
        df[col] = df[col].replace("nan", np.nan)
    ```
    Membersihkan seluruh kolom:

    * `astype(str)` ubah jadi string
    * `str.strip()` hapus spasi
    * `"nan"` dikembalikan jadi missing value
5. Menghapus Kolom Nomor
    ```
    if "No" in df.columns:
        df = df.drop(columns=["No"])
    ```
    Menghapus kolom identitas yang tidak berpengaruh pada prediksi.
6. Daftar Kolom Kategorikal
    ```
    categorical_columns = [
        "Usia",
        "Jenis_Kelamin",
        "Merokok",
        "Bekerja",
        "Rumah_Tangga",
        "Aktivitas_Begadang",
        "Aktivitas_Olahraga",
        "Asuransi",
        "Penyakit_Bawaan"
    ]
    ```
    Menentukan fitur kategori yang digunakan dalam dataset.
7. Menghapus Data Target Kosong
    ```
    df = df.dropna(subset=[target_col])
    ```
    Menghapus baris yang tidak memiliki label (Hasil kosong).

8. Memisahkan Fitur dan Target
    ```
    X_test = df.drop(columns=[target_col])
    y_test = df[target_col].astype(str)
    ```
    * `X_test` data input (fitur)
    * `y_test` jawaban asli (untuk dibandingkan dengan prediksi)

    Contoh:

    | Usia   | Merokok | Hasil   |
    | ------ | ------- | ------- |
    | Dewasa | Ya      | Positif |


    Maka:

    * `X_test` Usia, Merokok
    * `y_test` Hasil.

9. Menentukan Lokasi Model
    ```
    model_folder = os.path.join(
        os.path.expanduser("~"),
        "knime_model"
    )
    ```
    Menentukan folder tempat model disimpan.
    ```
    model_path = os.path.join(
        model_folder,
        "decision_tree_paru_paru_model.pkl"
    )
    ```
    Menentukan file model yang akan digunakan.
10. Load Model (Membuka Model)
    ```
    with open(model_path, "rb") as file:
        loaded_model = pickle.load(file)
    ```
    Memuat model yang sudah dilatih sebelumnya.
    * ``"rb"` read binary (membaca file model)
    * `pickle.load()` membuka model Decision Tree
11. Melakukan Prediksi
    ```
    prediction = loaded_model.predict(X_test)
    ```
    Model memprediksi hasil berdasarkan data testing.

    Output:
    * array hasil prediksi (misalnya: Positif / Negatif)

12. Membuat Output Hasil
    ```
    output_table_1 = pd.DataFrame({
        "Actual": y_test.values,
        "Prediction": prediction
    })
    ```

    Membandingkan:
    | Actual  | Prediction |
    | ------- | ---------- |
    | Positif | Positif    |
    | Negatif | Positif    |

Kode ini membuat output ke KNIME Analytics Platform berupa nilai asli dan hasil prediksi penyakit paru-paru.

```
Actual     = nilai Hasil asli
Prediction = hasil prediksi model
```

![image](https://hackmd.io/_uploads/HyiLDRS1ze.png)


#### Scorer Decision Tree
Node Scorer Decision Tree digunakan untuk mengevaluasi hasil prediksi model Decision Tree pada dataset prediksi penyakit paru-paru.

Pada node ini, kolom yang dibandingkan adalah:

```
Actual
Prediction
```

Setting yang digunakan:

```
Actual column     = Actual
Predicted column  = Prediction
```

Output node Scorer berupa confusion matrix dan statistik evaluasi hasil prediksi model.

![image](https://hackmd.io/_uploads/Hy8hv0S1Mx.png)

![image](https://hackmd.io/_uploads/SJIuWxIyGx.png)

![image](https://hackmd.io/_uploads/ByUwbe81Gg.png)



### Node Random Forest
Bagian Random Forest digunakan untuk membangun model klasifikasi dengan algoritma Random Forest.

Random Forest yang digunakan pada workflow ini terdiri dari:

```
50 decision trees
```

Pada bagian ini terdapat tiga node utama:
* Python Script (legacy) Training Random Forest : Yang Atas
* Python Script (legacy) Testing Random Forest : Yang Bawah
* Scorer (JavaScript) Random Forest

![image](https://hackmd.io/_uploads/HywGLaB1Gg.png)


#### Python Script Training Random Forest
Node Python Script Training Random Forest digunakan untuk melatih model Random Forest menggunakan data training (80%) dari Table Partitioner.

**Kode lengkap:**
```
import pandas as pd
import os
import pickle
import numpy as np

from sklearn.ensemble import RandomForestClassifier
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
from sklearn.impute import SimpleImputer

# Ambil data training
df = input_table_1.copy()

# Target
target_col = "Hasil"

# Bersihkan data
df = df.replace("?", np.nan)

for col in df.select_dtypes(include=["object"]).columns:
    df[col] = df[col].astype(str).str.strip()
    df[col] = df[col].replace("nan", np.nan)

# Hapus kolom nomor jika ada
if "No" in df.columns:
    df = df.drop(columns=["No"])

# Kolom kategorikal
categorical_columns = [
    "Usia",
    "Jenis_Kelamin",
    "Merokok",
    "Bekerja",
    "Rumah_Tangga",
    "Aktivitas_Begadang",
    "Aktivitas_Olahraga",
    "Asuransi",
    "Penyakit_Bawaan"
]

for col in categorical_columns:
    if col in df.columns:
        df[col] = df[col].astype(str)

# Hapus target kosong
df = df.dropna(subset=[target_col])

# Pisahkan fitur dan target
X_train = df.drop(columns=[target_col])
y_train = df[target_col].astype(str)

# Kolom kategorikal yang digunakan
categorical_cols = [
    col for col in categorical_columns
    if col in X_train.columns
]

# Encoder
try:
    encoder = OneHotEncoder(
        handle_unknown="ignore",
        sparse_output=False
    )
except TypeError:
    encoder = OneHotEncoder(
        handle_unknown="ignore",
        sparse=False
    )

# Transformer kategorikal
categorical_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="most_frequent")),
    ("encoder", encoder)
])

# Preprocessor
preprocessor = ColumnTransformer(
    transformers=[
        ("cat", categorical_transformer, categorical_cols)
    ]
)

# Model Random Forest
random_forest = RandomForestClassifier(
    n_estimators=50,
    min_samples_leaf=1,
    max_depth=None,
    random_state=42,
    n_jobs=-1
)

# Pipeline model
model_pipeline = Pipeline(steps=[
    ("preprocessing", preprocessor),
    ("random_forest", random_forest)
])

# Training
model_pipeline.fit(X_train, y_train)

# Simpan model
model_folder = os.path.join(
    os.path.expanduser("~"),
    "knime_model"
)

os.makedirs(model_folder, exist_ok=True)

model_path = os.path.join(
    model_folder,
    "random_forest_paru_paru_model.pkl"
)

with open(model_path, "wb") as file:
    pickle.dump(model_pipeline, file)

# Output KNIME
output_table_1 = pd.DataFrame({
    "Status": ["Random Forest paru-paru berhasil dibuat dan disimpan"],
    "Model Path": [model_path],
    "Jumlah Data Training": [len(df)],
    "Target": [target_col],
    "Jumlah Fitur": [X_train.shape[1]],
    "Jumlah Tree": [50]
})
```

**Penjelasan kode:**
1. Import Library
    ```
    import pandas as pd
    import os
    import pickle
    import numpy as np
    ```
    * `pandas` mengolah data tabel
    * `os` mengatur folder penyimpanan model
    * `pickle` menyimpan model machine learning
    * `numpy` menangani missing value (NaN)

2. Import Library Machine Learning
    ```
    from sklearn.ensemble import RandomForestClassifier
    from sklearn.pipeline import Pipeline
    from sklearn.compose import ColumnTransformer
    from sklearn.preprocessing import OneHotEncoder
    from sklearn.impute import SimpleImputer
    ```
    * `RandomForestClassifier` membuat model Random Forest
    * `Pipeline` menggabungkan preprocessing dan model
    * `ColumnTransformer` preprocessing kolom tertentu
    * `OneHotEncoder` mengubah data kategorikal menjadi numerik
    * `SimpleImputer` mengisi data kosong 

3. Mengambil Data Training
    ```
    df = input_table_1.copy()
    ```

    Mengambil data training dari KNIME lalu disalin ke df.

    Tujuan:

    * agar data asli tidak berubah saat diproses.
    
4. Menentukan Target
    ```
    target_col = "Hasil"
    ```

    Menentukan kolom target/label yang akan diprediksi.

    Pada dataset ini:

    * Hasil = Ya / Tidak terkena penyakit paru-paru.
    
5. Membersihkan Data
    ```
    df = df.replace("?", np.nan)
    ```

    Mengubah simbol ? menjadi missing value (NaN).

    ```
    for col in df.select_dtypes(include=["object"]).columns:
        df[col] = df[col].astype(str).str.strip()
        df[col] = df[col].replace("nan", np.nan)
    ```

    Membersihkan seluruh kolom kategorikal:

    * `astype(str)` ubah ke string
    * `str.strip()` hapus spasi
    * `"nan"` dikembalikan menjadi missing value

6. Menghapus Kolom Nomor
    ```
    if "No" in df.columns:
        df = df.drop(columns=["No"])
    ```

    Menghapus kolom No karena hanya nomor urut dan tidak digunakan untuk prediksi.
    
7. Menentukan Kolom Kategorikal
    ```
    categorical_columns = [
        "Usia",
        "Jenis_Kelamin",
        "Merokok",
        "Bekerja",
        "Rumah_Tangga",
        "Aktivitas_Begadang",
        "Aktivitas_Olahraga",
        "Asuransi",
        "Penyakit_Bawaan"
    ]
    ```

    Menentukan fitur kategori yang digunakan pada dataset paru-paru.

8. Mengubah Semua Kolom Menjadi String
    ```
        for col in categorical_columns:
        if col in df.columns:
            df[col] = df[col].astype(str)
    ```

    Mengubah seluruh fitur kategorikal menjadi string agar dapat diproses oleh encoder.
    
9. Menghapus Target Kosong
    ```
    df = df.dropna(subset=[target_col])
    ```

    Menghapus data yang tidak memiliki nilai target Hasil.

10. Memisahkan Fitur dan Target
    ```
    X_train = df.drop(columns=[target_col])
    y_train = df[target_col].astype(str)
    ```

    * `X_train` fitur/input training
    * `y_train` label/target prediksi

    | Usia | Merokok | Hasil |
    | ---- | ------- | ----- |
    | Tua  | Aktif   | Ya    |

    Maka:

    * `X_train` Usia, Merokok
    * `y_train` Hasil

11. Menentukan Kolom Kategorikal yang Digunakan
    ```
    categorical_cols = [
        col for col in categorical_columns
        if col in X_train.columns
    ]
    ```

    Memilih kolom kategorikal yang benar-benar tersedia pada dataset training.
    
12. Membuat Encoder
    ```
    encoder = OneHotEncoder(
        handle_unknown="ignore",
        sparse_output=False
    )
    ```

    Mengubah data kategorikal menjadi numerik.

    Contoh:

    | Jenis_Kelamin |
    | ------------- |
    | Pria          |
    | Wanita        |

    Menjadi:

    | Pria | Wanita |
    | ---- | ------ |
    | 1    | 0      |
    | 0    | 1      |
    
13. Membuat Transformer Kategorikal
    ```
    categorical_transformer = Pipeline(steps=[
        ("imputer", SimpleImputer(strategy="most_frequent")),
        ("encoder", encoder)
    ])
    ```

    Tahapan preprocessing:

    * mengisi data kosong dengan nilai yang paling sering muncul
    * melakukan One Hot Encoding

14. Membuat Preprocessor
    ```
    preprocessor = ColumnTransformer(
        transformers=[
            ("cat", categorical_transformer, categorical_cols)
        ]
    )
    ```

    Menggabungkan preprocessing untuk semua fitur kategorikal.

15. Membuat Model Random Forest
    ```
    random_forest = RandomForestClassifier(
        n_estimators=50,
        min_samples_leaf=1,
        max_depth=None,
        random_state=42,
        n_jobs=-1
    )
    ```

    Membuat model Random Forest.

    Parameter:

    * `n_estimators=50` menggunakan 50 decision tree
    * `random_state=42` hasil training konsisten
    * `n_jobs=-1` menggunakan seluruh core CPU

16. Membuat Pipeline
    ```
    model_pipeline = Pipeline(steps=[
        ("preprocessing", preprocessor),
        ("random_forest", random_forest)
    ])
    ```

    Menggabungkan preprocessing dan model Random Forest menjadi satu proses otomatis.

17. Training Model
    ```
    model_pipeline.fit(X_train, y_train)
    ```

    Melatih model Random Forest menggunakan data training.

18. Menentukan Folder Penyimpanan
    ```
    model_folder = os.path.join(
        os.path.expanduser("~"),
        "knime_model"
    )
    ```

    Menentukan lokasi folder penyimpanan model.
    
19. Membuat Folder
    ```
    os.makedirs(model_folder, exist_ok=True)
    ```

    Membuat folder jika belum tersedia.

20. Menentukan Nama File Model
    ```
    model_path = os.path.join(
        model_folder,
        "random_forest_paru_paru_model.pkl"
    )
    ```

    Menentukan nama file model Random Forest.
    
21. Menyimpan Model
    ```
    with open(model_path, "wb") as file:
        pickle.dump(model_pipeline, file)
    ```

    Menyimpan model yang sudah dilatih ke file .pkl.

    * `"wb"` write binary
    * `pickle.dump()` menyimpan model

22. Membuat Output KNIME
    ```
    output_table_1 = pd.DataFrame({
    ```

    Membuat output hasil training ke KNIME.

    Isi output:

    * status model
    * lokasi model
    * jumlah data training
    * target prediksi
    * jumlah fitur
    * jumlah decision tree Random Forest.

![image](https://hackmd.io/_uploads/ryxK_l8yzl.png)



#### Python Script Testing Random Forest
Node Python Script Testing Random Forest digunakan untuk memanggil model Random Forest yang sudah disimpan, lalu melakukan prediksi pada data testing.

**Kode lengkap:**
```
import pandas as pd
import os
import pickle
import numpy as np

# Ambil data testing
df = input_table_1.copy()

# Target
target_col = "Hasil"

# Bersihkan data
df = df.replace("?", np.nan)

for col in df.select_dtypes(include=["object"]).columns:
    df[col] = df[col].astype(str).str.strip()
    df[col] = df[col].replace("nan", np.nan)

# Hapus kolom nomor jika ada
if "No" in df.columns:
    df = df.drop(columns=["No"])

# Kolom kategorikal
categorical_columns = [
    "Usia",
    "Jenis_Kelamin",
    "Merokok",
    "Bekerja",
    "Rumah_Tangga",
    "Aktivitas_Begadang",
    "Aktivitas_Olahraga",
    "Asuransi",
    "Penyakit_Bawaan"
]

for col in categorical_columns:
    if col in df.columns:
        df[col] = df[col].astype(str)

# Hapus target kosong
df = df.dropna(subset=[target_col])

# Pisahkan fitur dan target
X_test = df.drop(columns=[target_col])
y_test = df[target_col].astype(str)

# Load model
model_folder = os.path.join(
    os.path.expanduser("~"),
    "knime_model"
)

model_path = os.path.join(
    model_folder,
    "random_forest_paru_paru_model.pkl"
)

with open(model_path, "rb") as file:
    loaded_model = pickle.load(file)

# Prediksi
prediction = loaded_model.predict(X_test)

# Output
output_table_1 = pd.DataFrame({
    "Actual": y_test.values,
    "Prediction": prediction
})
```

**Penjelasan kode:**
1. Import Library
    ```
    import pandas as pd
    import os
    import pickle
    import numpy as np
    ```

    Fungsi:

    * `pandas` mengolah data tabel
    * `os` mengatur folder/path
    * `pickle` membuka model yang sudah disimpan
    * `numpy` mengolah data numerik dan missing value

2. Membaca Data Testing
    ```
    df = input_table_1.copy()
    ```

    Mengambil data testing dari KNIME ke Python.

    Data ini berasal dari:

    `20% testing`

    hasil pembagian Table Partitioner.
    
3. Menentukan Target
    ```
    target_col = "Hasil"
    ```

    Kolom target yang akan dibandingkan dengan hasil prediksi.

    Contoh isi:

    * Ya
    * Tidak

4. Membersihkan Data
    ```
    df = df.replace("?", np.nan)
    ```

    Mengubah tanda:

    `?`

    menjadi missing value (NaN).

5. Membersihkan Kolom String
    ```
    for col in df.select_dtypes(include=["object"]).columns:
    ```

    Membersihkan data teks:

    ```
    menghapus spasi
    mengubah format string
    memperbaiki null palsu
    ```

    Bagian ini:

    ```
    df[col] = df[col].astype(str).str.strip()
    ```

    menghapus spasi.

    Contoh:

    `" Ya " -> "Ya"`

6. Menghapus Kolom Nomor
    ```
    if "No" in df.columns:
        df = df.drop(columns=["No"])
    ```

    Kolom nomor tidak dipakai untuk prediksi.

    Karena:

    `No = hanya identitas data`


7. Kolom Kategorikal
    ```
    categorical_columns = [
    ```

    Berisi kolom kategori seperti:

    * Usia
    * Merokok
    * Asuransi

    Semua kolom ini akan diproses oleh encoder dari model training.

8. Mengubah Data Menjadi String
    ```
    df[col] = df[col].astype(str)
    ```

    Supaya format data konsisten dengan data training.
    
    
9. Menghapus Target Kosong
    ```
    df = df.dropna(subset=[target_col])
    ```

    Menghapus data yang tidak memiliki nilai target.
    
10. Memisahkan Fitur dan Target
    ```
    X_test = df.drop(columns=[target_col])
    y_test = df[target_col].astype(str)
    ```

    Fungsi:

    * `X_test` data input testing
    * `y_test` jawaban asli/testing asli

11. Menentukan Folder Model
    ```
    model_folder = os.path.join(
        os.path.expanduser("~"),
        "knime_model"
    )
    ```

    Menentukan lokasi model yang sudah disimpan sebelumnya. 
    
12. Menentukan File Model
    ```
    model_path = os.path.join(
        model_folder,
        "random_forest_paru_paru_model.pkl"
    )
    ```

    Memanggil file model:

    `random_forest_paru_paru_model.pkl`

    yang dibuat saat training.
    
13. Membuka Model
    ```
    with open(model_path, "rb") as file:
        loaded_model = pickle.load(file)
    ```

    Fungsi:

    * membuka model Random Forest
    * membaca hasil training sebelumnya 

14. Prediksi
    ```
    prediction = loaded_model.predict(X_test)
    ```

    Model melakukan prediksi pada data testing.

    Contoh hasil:

    ```
    Ya
    Tidak
    Ya
    ```

15. Menampilkan Output
    ```
    output_table_1 = pd.DataFrame({
    ```

    Menampilkan hasil ke KNIME.

    Isi output:

    * `Actual` data asli
    * `Prediction` hasil prediksi model

    Contoh:
    | Actual | Prediction |
    | ------ | ---------- |
    | Ya     | Ya         |
    | Tidak  | Tidak      |
    | Ya     | Ya         |

    Data ini nanti masuk ke:

    `Scorer (JavaScript)`

    untuk menghitung:

    ```
    Accuracy
    Precision
    Recall
    Confusion Matrix
    ```

![image](https://hackmd.io/_uploads/HyEt2xUkGe.png)


#### Scorer Random Forest
Node Scorer Random Forest digunakan untuk mengevaluasi hasil prediksi model Random Forest pada dataset prediksi penyakit paru-paru.

Pada node ini, kolom yang dibandingkan adalah:

```
Actual
Prediction
```

Setting yang digunakan:

```
Actual column     = Actual
Predicted column  = Prediction
```

Output node Scorer berupa confusion matrix dan statistik evaluasi hasil prediksi model Random Forest.

Hasil Scorer Random Forest kemudian dibandingkan dengan hasil Scorer Decision Tree.

![image](https://hackmd.io/_uploads/Hyt1al8yMe.png)

![image](https://hackmd.io/_uploads/Hy0HagIkGx.png)

![image](https://hackmd.io/_uploads/S1Q86xLyGe.png)





# Hasil Evaluasi
## Hasil Evaluasi Model
Setelah proses pembentukan model Decision Tree dan Random Forest selesai dilakukan, langkah selanjutnya adalah melakukan pengujian performa model menggunakan node Scorer pada KNIME.

Tahap evaluasi dilakukan dengan membandingkan dua kolom utama, yaitu:

```
Actual
Prediction
```

Kolom Actual menunjukkan nilai target Hasil yang sebenarnya pada dataset, sedangkan kolom Prediction berisi hasil klasifikasi yang diprediksi oleh model.

Melalui node Scorer, diperoleh beberapa hasil evaluasi model, antara lain:

* confusion matrix
* accuracy
* precision
* recall
* F1-score

### Confusion Matrix
Confusion matrix merupakan metode evaluasi yang digunakan untuk mengetahui performa model klasifikasi berdasarkan hasil prediksi yang benar maupun salah pada setiap kelas data.

Pada penelitian ini, variabel target Hasil terdiri dari dua kategori, yaitu:

Tidak = tidak terindikasi penyakit paru-paru
Ya = terindikasi penyakit paru-paru

Struktur confusion matrix dapat dijelaskan sebagai berikut:

```
Actual Tidak -> Predicted Tidak = True Negative (TN)
Actual Tidak -> Predicted Ya    = False Positive (FP)
Actual Ya    -> Predicted Tidak = False Negative (FN)
Actual Ya    -> Predicted Ya    = True Positive (TP)
```

Rumus confusion matrix:
$$\text{Confusion Matrix} = \begin{bmatrix} TN & FP \\ FN & TP \end{bmatrix}$$

Penjelasan Confusion Matrix

* True Negative (TN)
    Kondisi ketika data sebenarnya bernilai `Tidak` dan hasil prediksi model juga `Tidak`.
* False Positive (FP)
    Kondisi ketika data sebenarnya `Tidak`, tetapi model memprediksi `Ya`.
* False Negative (FN)
    Kondisi ketika data sebenarnya `Ya`, namun model memprediksi `Tidak`.
* True Positive (TP)
    Kondisi ketika data sebenarnya `Ya` dan model juga memprediksi `Ya`.

1. True Negative (TN)
    True Negative menunjukkan bahwa model berhasil mengenali data yang memang tidak terindikasi penyakit paru-paru. Dengan kata lain, hasil aktual dan hasil prediksi sama-sama bernilai Tidak.

2. False Positive (FP)
 
    False Positive terjadi ketika model memprediksi seseorang terindikasi penyakit paru-paru, padahal kondisi sebenarnya tidak terindikasi. Hal ini menunjukkan adanya kesalahan prediksi positif pada model.

3. False Negative (FN)
    False Negative merupakan kondisi ketika data sebenarnya terindikasi penyakit paru-paru, tetapi model justru memprediksi tidak terindikasi. Kesalahan ini menunjukkan bahwa model gagal mendeteksi kasus positif yang sebenarnya ada.

4. True Positive (TP)
    True Positive terjadi apabila model berhasil memprediksi data positif dengan benar, yaitu ketika kondisi aktual dan hasil prediksi sama-sama menunjukkan adanya indikasi penyakit paru-paru.
    
### Accuracy
Accuracy merupakan ukuran evaluasi yang digunakan untuk mengetahui tingkat ketepatan model dalam melakukan klasifikasi. Nilai accuracy diperoleh dari perbandingan jumlah prediksi yang benar terhadap seluruh data pengujian.

Rumus accuracy:

$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$

Keterangan:

* $TP$ = True Positive
* $TN$ = True Negative
* $FP$ = False Positive
* $FN$ = False Negative

Semakin besar nilai accuracy, maka semakin baik kemampuan model dalam melakukan prediksi secara keseluruhan.

### Precision
Precision digunakan untuk mengukur tingkat ketepatan model ketika memprediksi data positif. Metode ini menunjukkan seberapa banyak prediksi positif yang benar-benar sesuai dengan kondisi sebenarnya.

Rumus precision:

$$Precision = \frac{TP}{TP + FP}$$

Nilai precision yang tinggi menandakan bahwa model memiliki kesalahan prediksi positif yang rendah.

### Recall
Recall merupakan metrik evaluasi yang digunakan untuk mengetahui kemampuan model dalam menemukan seluruh data yang benar-benar positif.

Rumus recall:

$$Recall = \frac{TP}{TP + FN}$$

Semakin tinggi nilai recall, maka semakin baik model dalam mendeteksi data positif yang ada pada dataset.

### F1-Score
F1-Score adalah ukuran evaluasi yang digunakan untuk menilai keseimbangan antara precision dan recall. Metrik ini sering digunakan ketika distribusi data tidak seimbang.

Rumus F1-Score:

$$F1\text{-}Score = 2 \times \frac{Precision \times Recall}{Precision + Recall}$$

Nilai F1-Score yang tinggi menunjukkan bahwa model memiliki keseimbangan yang baik antara ketepatan prediksi positif dan kemampuan mendeteksi data positif.


## Hasil Evaluasi Decision Tree
Hasil evaluasi model Decision Tree diperoleh menggunakan node Scorer pada KNIME. Pada tahap ini, hasil prediksi dari model dibandingkan dengan nilai aktual dari variabel target Hasil.

Kolom yang digunakan dalam proses evaluasi yaitu:

```
Actual
Prediction
```

Kolom Actual menunjukkan nilai asli dari target Hasil, sedangkan kolom Prediction merupakan hasil prediksi yang dihasilkan oleh model Decision Tree.

![image](https://hackmd.io/_uploads/SkioJaIyzx.png)

![image](https://hackmd.io/_uploads/BkJnkTL1Mx.png)

### Confusion Matrix Decision Tree

Berdasarkan hasil node Scorer, diperoleh confusion matrix sebagai berikut:

    Actual Tidak -> Predicted Tidak = 3130
    Actual Tidak -> Predicted Ya    = 0
    Actual Ya    -> Predicted Tidak = 320
    Actual Ya    -> Predicted Ya    = 2550

Rumus confusion matrix:

Confusion Matrix=[
$$\text{Confusion Matrix} = \begin{bmatrix} TN & FP \\ FN & TP \end{bmatrix}$$

Keterangan:

* TN = 3130
* FP = 0
* FN = 320
* TP = 2550

1. Actual Tidak → Predicted Tidak (TN)

    Bagian ini menunjukkan jumlah data yang sebenarnya tidak terindikasi penyakit paru-paru dan berhasil diprediksi dengan benar oleh model sebagai Tidak.

2. Actual Tidak → Predicted Ya (FP)

    Bagian ini menunjukkan jumlah data yang sebenarnya tidak terindikasi penyakit paru-paru tetapi diprediksi sebagai Ya oleh model.

    Pada hasil evaluasi ini, nilai FP = 0, yang berarti model tidak melakukan kesalahan prediksi positif pada data negatif.

3. Actual Ya → Predicted Tidak (FN)

    Bagian ini menunjukkan jumlah data yang sebenarnya terindikasi penyakit paru-paru tetapi diprediksi sebagai Tidak oleh model.

    Hal ini menunjukkan bahwa masih terdapat beberapa data positif yang gagal dideteksi oleh model.

4. Actual Ya → Predicted Ya (TP)

    Bagian ini menunjukkan jumlah data yang memang terindikasi penyakit paru-paru dan berhasil diprediksi dengan benar oleh model sebagai Ya.

### Accuracy Decision Tree

Nilai accuracy digunakan untuk mengetahui tingkat ketepatan model dalam melakukan klasifikasi terhadap seluruh data testing.

Rumus accuracy:

$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$

Dengan memasukkan nilai confusion matrix:

$$Accuracy = \frac{2550+3130}{2550+3130+0+320}$$
	
Hasil perhitungan accuracy:

$$Accuracy = 0.947 \times 100\% = 94.7\%$$

Berdasarkan hasil tersebut, model Decision Tree memperoleh tingkat accuracy sebesar $94.7\%$.

### Analisis Hasil Decision Tree

Berdasarkan hasil evaluasi yang diperoleh, model Decision Tree mampu melakukan klasifikasi data dengan cukup baik terhadap target `Hasil`.

Model berhasil mengklasifikasikan sebagian besar data dengan benar, terutama pada kelas Tidak yang memperoleh nilai prediksi benar cukup tinggi.

Decision Tree bekerja menggunakan satu struktur pohon keputusan sehingga proses pengambilan keputusan lebih mudah dipahami dan divisualisasikan.

Meskipun demikian, karena hanya menggunakan satu pohon keputusan, model masih memiliki kemungkinan mengalami overfitting apabila pola data yang digunakan semakin kompleks atau jumlah data bertambah besa

## Hasil Evaluasi Random Forest
Hasil evaluasi model Random Forest diperoleh menggunakan node Scorer pada KNIME. Pada tahap ini, hasil prediksi dari model Random Forest dibandingkan dengan nilai aktual dari variabel target Hasil.

Kolom yang digunakan pada proses evaluasi yaitu:

```
Actual
Prediction
```

Kolom Actual berisi nilai asli dari target Hasil, sedangkan kolom Prediction berisi hasil prediksi yang dihasilkan oleh model Random Forest.

![image](https://hackmd.io/_uploads/HyZIm681Ge.png)


![image](https://hackmd.io/_uploads/B1BBmTL1Mx.png)

### Confusion Matrix Random Forest

Berdasarkan hasil node Scorer, diperoleh confusion matrix sebagai berikut:

```
Actual Tidak -> Predicted Tidak = 3130
Actual Tidak -> Predicted Ya    = 0
Actual Ya    -> Predicted Tidak = 320
Actual Ya    -> Predicted Ya    = 2550
```

Rumus confusion matrix:

Confusion Matrix=[
$$\text{Confusion Matrix} = \begin{bmatrix} TN & FP \\ FN & TP \end{bmatrix}$$

Keterangan:

* TN = 3130
* FP = 0
* FN = 320
* TP = 2550

1. Actual Tidak → Predicted Tidak (TN)

    Bagian ini menunjukkan jumlah data yang sebenarnya tidak terindikasi penyakit paru-paru dan berhasil diprediksi dengan benar oleh model sebagai Tidak.

2. Actual Tidak → Predicted Ya (FP)

    Bagian ini menunjukkan jumlah data yang sebenarnya tidak terindikasi penyakit paru-paru tetapi diprediksi sebagai Ya oleh model.

    Pada hasil evaluasi ini, nilai FP = 0 yang berarti model tidak melakukan kesalahan prediksi positif pada kelas negatif.

3. Actual Ya → Predicted Tidak (FN)

    Bagian ini menunjukkan jumlah data yang sebenarnya terindikasi penyakit paru-paru tetapi diprediksi sebagai Tidak oleh model.

    Hal ini menunjukkan bahwa masih terdapat beberapa data positif yang belum berhasil dikenali oleh model.

4. Actual Ya → Predicted Ya (TP)

    Bagian ini menunjukkan jumlah data yang memang terindikasi penyakit paru-paru dan berhasil diprediksi dengan benar oleh model sebagai Ya.

### Accuracy Random Forest

Accuracy digunakan untuk mengukur tingkat ketepatan model dalam mengklasifikasikan seluruh data testing.

Rumus accuracy:

$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$

Dengan memasukkan nilai confusion matrix:

$$Accuracy = \frac{2550+3130}{2550+3130+0+320}$$
	
Hasil perhitungan accuracy:

$$Accuracy = 0.947 \times 100\% = 94.7\%$$

Berdasarkan hasil evaluasi tersebut, model Random Forest memperoleh nilai accuracy sebesar $94.7\%$.

### Analisis Hasil Random Forest

Berdasarkan hasil pengujian yang telah dilakukan, model Random Forest mampu melakukan klasifikasi data dengan baik terhadap target Hasil.

Random Forest bekerja menggunakan banyak pohon keputusan (multiple decision tree) yang digabungkan menjadi satu model. Setiap pohon akan melakukan prediksi terhadap data, kemudian hasil akhir ditentukan berdasarkan metode voting.

Konsep voting pada Random Forest dapat dituliskan sebagai berikut:

$$\hat{y} = \text{mode}(T_1(x), T_2(x), T_3(x), \dots, T_n(x))$$

Keterangan:
* $\hat{y}$ = hasil akhir prediksi Random Forest
* $T_n(x)$ = hasil prediksi dari tree ke-$n$

Karena menggunakan banyak pohon keputusan, Random Forest umumnya memiliki performa yang lebih stabil dan mampu mengurangi risiko overfitting dibandingkan menggunakan satu Decision Tree saja.

# Perbandingan Decision Tree dan Random Forest
Model Decision Tree dan Random Forest digunakan untuk melakukan klasifikasi terhadap data indikasi penyakit paru-paru berdasarkan atribut pada dataset.

Decision Tree melakukan proses klasifikasi menggunakan satu pohon keputusan (single tree). Setiap percabangan pada pohon digunakan untuk membagi data hingga menghasilkan keputusan akhir berupa kelas Ya atau Tidak. Karena hanya menggunakan satu tree, struktur model ini lebih sederhana sehingga proses klasifikasi lebih mudah dipahami dan dianalisis.

Pada penelitian ini, model Decision Tree menghasilkan nilai accuracy sebesar:

$$Accuracy=94.7\%$$

Sementara itu, Random Forest merupakan pengembangan dari Decision Tree yang bekerja menggunakan banyak pohon keputusan (multiple trees). Setiap tree akan melakukan prediksi terhadap data testing, kemudian hasil akhirnya ditentukan berdasarkan voting mayoritas dari seluruh tree.

Pada penelitian ini, Random Forest dibangun menggunakan:

    50 decision trees

Hasil evaluasi menunjukkan bahwa Random Forest juga memperoleh nilai accuracy sebesar:

$$Accuracy=94.7\%$$

Berdasarkan hasil tersebut, kedua algoritma menghasilkan performa klasifikasi yang sama pada dataset yang digunakan.

Kesamaan hasil accuracy ini dapat terjadi karena pola data pada dataset sudah cukup jelas dan mudah dipisahkan oleh model klasifikasi. Selain itu, seluruh atribut pada dataset bersifat kategorikal sehingga proses pembentukan aturan klasifikasi menjadi lebih sederhana.

Jumlah data yang relatif terstruktur juga memungkinkan Decision Tree menghasilkan pemisahan data yang hampir optimal hanya dengan satu pohon keputusan. Akibatnya, ketika Random Forest menggunakan banyak tree, hasil voting yang diperoleh tetap menghasilkan prediksi yang sama dengan Decision Tree.

Dengan kata lain, penggunaan banyak tree pada Random Forest belum memberikan perubahan signifikan karena Decision Tree tunggal sudah mampu mengenali pola data dengan baik.

Walaupun nilai accuracy kedua model sama, Random Forest tetap memiliki keunggulan dalam kestabilan model karena menggunakan kombinasi banyak tree sehingga lebih tahan terhadap perubahan data dan risiko overfitting.

## Sebab Random Forest Lebih Stabil

Random Forest memiliki tingkat kestabilan yang lebih baik karena proses klasifikasi tidak hanya bergantung pada satu pohon keputusan saja. Model ini menggabungkan banyak decision tree untuk menentukan hasil prediksi akhir.

Beberapa faktor yang membuat Random Forest lebih stabil antara lain:

menggunakan banyak pohon keputusan dalam proses klasifikasi
mampu mengurangi kemungkinan overfitting
hasil akhir ditentukan berdasarkan voting dari seluruh tree
lebih konsisten terhadap perubahan data
mampu menangani data dengan pola yang lebih kompleks

Secara umum, konsep kerja Random Forest dilakukan dengan mengumpulkan hasil prediksi dari setiap tree, kemudian memilih hasil prediksi yang paling banyak muncul sebagai keputusan akhir.

$$\hat{y} = \text{mode}(T_1(x), T_2(x), T_3(x), \dots, T_n(x))$$

Keterangan:
* $\hat{y}$ = hasil akhir prediksi Random Forest
* $T_n(x)$ = hasil prediksi dari tree ke-$n$
* $n$ = jumlah pohon keputusan yang digunakan dalam Random Forest

# Kesimpulan

Berdasarkan penelitian yang telah dilakukan, algoritma Decision Tree dan Random Forest berhasil diterapkan menggunakan Python Script Legacy pada KNIME untuk klasifikasi Prediksi Terkena Penyakit Paru-Paru.

Dataset Prediksi Terkena Penyakit Paru-Paru yang digunakan terdiri dari atribut:

| No | Nama Atribut     | Keterangan                            |
| -- | ---------------- | ------------------------------------- |
| 1  | Usia             | Umur responden                        |
| 2  | Jenis Kelamin    | Pria atau Wanita              |
| 3  | Merokok          | Kebiasaan merokok                     |
| 4  | Begadang         | Kebiasaan tidur larut malam           |
| 5  | Olahraga         | Intensitas olahraga                   |
| 6  | Penyakit Bawaan  | Riwayat penyakit sebelumnya           |
| 7  | Konsumsi Alkohol | Kebiasaan konsumsi alkohol            |
| 8  | Polusi Udara     | Tingkat paparan polusi                |
| 9  | Pekerjaan        | Jenis pekerjaan responden             |
| 10 | Hasil            | Terkena penyakit paru-paru atau tidak |


Dengan target klasifikasi yaitu `Hasil` yang terdiri dari kelas Ya dan Tidak.

Data dibagi menjadi:

```
80% data training
20% data testing
```

Hasil evaluasi menggunakan node Scorer menunjukkan bahwa model Decision Tree dan Random Forest sama-sama menghasilkan nilai accuracy sebesar:

$$Accuracy=94.7\%$$

Decision Tree bekerja menggunakan satu pohon keputusan sehingga model lebih sederhana dan mudah dipahami. Sedangkan Random Forest menggunakan 50 decision tree dan menentukan hasil akhir menggunakan metode voting.

Nilai accuracy kedua model sama karena pola data pada dataset sudah cukup jelas sehingga kedua algoritma mampu melakukan klasifikasi dengan baik.

Meskipun hasil accuracy sama, Random Forest tetap lebih stabil dan lebih tahan terhadap overfitting dibandingkan Decision Tree karena menggunakan banyak pohon keputusan dalam proses klasifikasi.
