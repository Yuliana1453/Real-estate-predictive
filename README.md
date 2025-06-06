# Laporan Proyek Machine Learning - Yuliana

## Domain Proyek

Pasar properti merupakan salah satu sektor ekonomi yang krusial, terutama dalam pengambilan keputusan investasi dan kebijakan. Prediksi harga rumah secara akurat sangat penting bagi agen properti, pembeli rumah, dan pengembang.

Dalam proyek ini, akan dilakukan analisis dan prediksi harga rumah berdasarkan fitur seperti luas area, jumlah kamar tidur, dan lokasi properti.

## Business Understanding
### Problem Statements
Harga rumah sangat dipengaruhi oleh banyak faktor, seperti lokasi, aksesibilitas, tingkat kriminalitas, dan kondisi lingkungan. Mengetahui faktor-faktor ini dapat membantu pemangku kebijakan, investor, atau calon pembeli untuk mengambil keputusan yang lebih baik.

Masalah: Bagaimana memprediksi harga rumah di daerah Boston berdasarkan faktor lingkungan dan sosial ekonomi?
### Goals

Membuat model prediktif untuk memperkirakan harga rumah (MEDV) berdasarkan fitur-fitur seperti tingkat kriminalitas (CRIM), akses jalan (RAD), kualitas pendidikan (PTRATIO), dan lainnya.

### Solution statements
Solusi yang diusulkan:
- Baseline Model: Menggunakan Linear Regression sebagai baseline.
- Model Alternatif: Menggunakan Random Forest Regressor dan Gradient Boosting Regressor.
- Improvement: Melakukan hyperparameter tuning pada model terbaik menggunakan GridSearchCV.
- Evaluasi: Menggunakan metrik evaluasi seperti MAE, RMSE, dan R² score.

## Data Understanding
Dataset yang digunakan berasal dari Kaggle: [Real Estate Price](https://www.kaggle.com/code/fahadrehman07/real-estate-price-prediction?select=data.csv)
1. Jumlah Baris dan Kolom
- 511 baris data (observasi)
- 14 kolom (fitur)
2. Kolom/Fitur:
  - `CRIM`:	Tingkat kriminalitas per kapita
  - `ZN`	Proporsi lahan zonasi untuk rumah besar
  - `INDUS`	Proporsi area bisnis non-ritel
  - `CHAS`	Apakah berbatasan dengan Sungai Charles
  - `NOX`	Konsentrasi polutan NOx
  - `RM`:	Rata-rata jumlah kamar
  - `AGE`:	Persentase rumah yang dibangun sebelum 1940
  - `DIS`:	Jarak ke pusat pekerjaan di Boston
  - `RAD`:	Akses ke jalan utama
  - `TAX`:	Tarif pajak properti
  - `PTRATIO`:	Rasio siswa-guru
  - `B`:	Transformasi dari proporsi penduduk kulit hitam
  - `LSTAT`:	Persentase penduduk berstatus ekonomi rendah
  - `MEDV`:	Harga rumah median (target)

2. Kondisi Awal Data
- Missing Values
  - Terdapat 5 Missing Value pada kolom `RM`
- Distribusi dan Outlier
  
  Berdasarkan hasil .describe():

  - Kolom CRIM memiliki nilai maksimum 88.98, jauh di atas nilai kuartil ketiga (Q3 = 3.62), menunjukkan potensi outlier pada tingkat kejahatan.
  - Kolom LSTAT juga memiliki nilai maksimum tinggi (76.00), dengan Q3 = 17.11, menunjukkan keberadaan outlier yang signifikan.
  - Kolom RM berkisar dari 3.56 hingga 8.78, nilai ekstrem yang mungkin menunjukkan properti tidak biasa.
- Data ini tidak memiliki duplikat.

## Data Preparation
### 📌 Tahapan Data Preparation
- Handling Missing Values: Menangani 5 missing values pada kolom `RM`.
- Split Data: 80% data untuk training dan 20% untuk testing.
- Scaling: Menggunakan StandardScaler karena model seperti Linear Regression dan Gradient Boosting sensitif terhadap skala.

### 📌 Alasan Tahapan
Scaling diperlukan untuk menyamakan skala fitur numerik agar model tidak bias.

Handling missing values penting agar tidak terjadi error saat training.

Split data untuk menghindari data leakage dan memastikan evaluasi model adil.


## Modeling
Algoritma yang Digunakan:

1. Linear Regression
- Linear Regression adalah metode regresi yang berusaha mencari garis lurus terbaik untuk memetakan hubungan antara variabel input (fitur) dan output (target). Model ini bekerja dengan meminimalkan total selisih kuadrat antara prediksi dan nilai sebenarnya.
- Parameter yang digunakan: default (tidak ada yang disetel secara eksplisit)

2. Random Forest Regressor
- Random Forest merupakan algoritma ensemble berbasis decision tree. Ia membangun banyak decision tree (hutan) dan menggabungkan hasil prediksi dari semua tree (rata-rata untuk regresi) untuk meningkatkan akurasi dan mengurangi overfitting.

- Parameter yang digunakan:
  - random_state=42 untuk memastikan hasil yang konsisten
  - Parameter lainnya menggunakan default

3. Gradient Boosting Regressor
- Gradient Boosting adalah algoritma ensemble yang membangun model secara bertahap. Setiap tree baru berusaha memperbaiki kesalahan dari tree sebelumnya, dengan pendekatan gradient descent pada fungsi loss.

- Parameter model awal:
  - random_state=42
  - Lainnya default

- Parameter setelah tuning dengan GridSearchCV:

      {
        'learning_rate': 0.05,
        'max_depth': 5,
        'min_samples_leaf': 3,
        'min_samples_split': 2,
        'n_estimators': 200
      }

### 📌 Metrik Evaluasi
- MAE	(Rata-rata nilai absolut error): Semakin kecil, semakin baik
- RMSE	(Akar dari rata-rata kuadrat error): Lebih penal terhadap error besar
- R² Score	(1 - (RSS/TSS)): Proporsi variansi target yang dijelaskan oleh model
### 📌 Interpretasi Hasil
- Hasil metrik akan dibandingkan antar model.
- Model dengan MAE dan RMSE paling rendah serta R² Score tertinggi akan dipilih sebagai model final.


## Evaluation
1. **Linear Regression** menunjukkan performa paling rendah dengan MAE tertinggi (4.14) dan R² terendah (0.17), artinya model ini kurang mampu menjelaskan variansi data harga rumah.

2. **Random Forest** jauh lebih baik dengan MAE 2.83 dan R² 0.66, memperlihatkan model ini lebih stabil dan akurat dalam prediksi.

3. **Gradient Boosting** versi default memberikan performa terbaik dengan MAE 2.70 dan R² 0.73, yang berarti prediksi paling mendekati harga sebenarnya.

4. **Gradient Boosting setelah hyperparameter tuning** ternyata mengalami penurunan performa dibanding versi default (MAE naik jadi 3.00 dan R² turun ke 0.58). Hal ini bisa terjadi karena overfitting saat tuning atau parameter tuning belum optimal.

**Kesimpulan:**
**Model Gradient Boosting** versi default adalah pilihan terbaik untuk prediksi harga rumah di proyek ini. Untuk hyperparameter tuning, perlu eksplorasi lebih lanjut agar mendapatkan konfigurasi parameter yang benar-benar meningkatkan performa.
