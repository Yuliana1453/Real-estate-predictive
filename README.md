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

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

### Solution statements
Solusi yang diusulkan:
- Baseline Model: Menggunakan Linear Regression sebagai baseline.
- Model Alternatif: Menggunakan Random Forest Regressor dan Gradient Boosting Regressor.
- Improvement: Melakukan hyperparameter tuning pada model terbaik menggunakan GridSearchCV.
- Evaluasi: Menggunakan metrik evaluasi seperti MAE, RMSE, dan R² score.

## Data Understanding
Dataset yang digunakan berasal dari Kaggle: [Real Estate Price](https://www.kaggle.com/code/fahadrehman07/real-estate-price-prediction?select=data.csv)
- Kolom/Fitur:
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

## Data Preparation
### 📌 Tahapan Data Preparation
Handling Missing Values: Cek dan tangani jika ada.

Encoding: Variabel CHAS sudah dalam bentuk 0/1 (tidak perlu encoding tambahan).

Scaling: Menggunakan StandardScaler karena model seperti Linear Regression dan Gradient Boosting sensitif terhadap skala.

Split Data: 80% data untuk training dan 20% untuk testing.

### 📌 Alasan Tahapan
Scaling diperlukan untuk menyamakan skala fitur numerik agar model tidak bias.

Handling missing values penting agar tidak terjadi error saat training.

Split data untuk menghindari data leakage dan memastikan evaluasi model adil.


## Modeling
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
