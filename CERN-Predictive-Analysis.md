# Laporan Proyek Machine Learning - Abisatya Hastarangga Pradana

## Domain Proyek

Massa invarian, juga dikenal sebagai massa diam atau massa intrinsik, merupakan karakteristik fundamental dari sistem energi total dan momentum yang tidak berubah di semua kerangka acuan yang terkait dengan transformasi Lorentz [(Fedorov, 2017)](https://iopscience.iop.org/article/10.1088/1555-6611/aa567f/meta). Konsep ini menjadi sangat penting dalam fisika energi tinggi karena memungkinkan identifikasi dan karakterisasi partikel subatomik dengan tepat. Massa invarian merupakan properti unik yang membantu fisikawan membedakan berbagai jenis partikel, termasuk elektron, muon, dan kemungkinan partikel eksotis yang sebelumnya belum terdeteksi.

Dalam eksperimen tabrakan partikel energi tinggi, partikel yang menarik (misalnya Higgs) direkonstruksi menggunakan informasi tentang produk peluruhan, momentum, deposit energi, dan sudut partikel-partikel tersebut. Massa invarian partikel dihitung menggunakan kinematika relativistik, menghasilkan histogram massa versus jumlah kejadian. Meskipun massa invarian merupakan properti unik suatu partikel, data eksperimental menunjukkan distribusi dengan lebar yang signifikan (Δm) [(Pseudo, 2019)](https://physics.stackexchange.com/questions/478681/why-does-the-reconstructed-mass-of-a-particle-have-a-fairly-wide-distribution) dalam histogram, yang menantang untuk dianalisis dengan metode konvensional.

Rekonstruksi massa invarian dari data eksperimen CERN menghadapi beberapa tantangan signifikan:

1. Kehadiran Neutrino yang Hilang: Rekonstruksi massa invarian menjadi sangat sulit ketika partikel meluruh menjadi lepton tau karena adanya neutrino yang hilang dalam keadaan akhir. Neutrino tidak terdeteksi langsung oleh detektor, yang menyebabkan informasi momentum yang tidak lengkap [(Vinaya; dkk., 2023)](https://arxiv.org/pdf/2304.01126).
2. Ketidakpastian Pengukuran: Pengukuran energi dan momentum partikel di detektor memiliki ketidakpastian intrinsik yang berkontribusi pada pelebaran distribusi massa invarian.
3. Volume Data yang Besar: Eksperimen di CERN menghasilkan volume data yang sangat besar, melebihi lima petabyte data terbuka, yang membutuhkan metode analisis yang efisien dan skalabel.
4. Outlier yang Bermakna: Dalam fisika partikel, outlier sering kali mewakili kejadian fisik yang signifikan daripada sekadar noise data. Penghapusan outlier dapat menghilangkan informasi berharga tentang peristiwa langka atau partikel eksotis.

Seiring dengan berkembangnya pembelajaran mesin, teknik-teknik baru telah dikembangkan untuk mengatasi tantangan dalam rekonstruksi massa invarian. Metode pembelajaran mesin telah banyak dimanfaatkan dalam fisika energi tinggi eksperimental, khususnya dalam menganalisis data yang dihasilkan di LHC. Berdasarkan pemahaman tentang pentingnya massa invarian dalam fisika partikel dan keunggulan model regresi berbasis pohon, proyek ini bertujuan untuk:
1. Mengembangkan model prediksi massa invarian elektron yang akurat menggunakan teknik regresi berbasis pohon, memanfaatkan data dari eksperimen tabrakan partikel CERN.
2. Mengoptimalkan model untuk bekerja secara efisien dengan volume data besar yang dihasilkan oleh eksperimen CERN, memastikan skalabilitas dan kinerja yang baik.
3. Menerapkan pendekatan yang mempertahankan integritas fisik analisis dengan tidak perlu menghapus atau mendistorsi outlier data, mengingat signifikansi potensial dari kejadian ekstrem dalam fisika partikel.

## Business Understanding

### Problem Statements

Eksperimen partikel berenergi tinggi seperti di CERN menghasilkan data dalam jumlah besar yang kompleks dan penuh dengan informasi fisika penting. Salah satu parameter kunci yang dipelajari dari hasil tabrakan partikel adalah **massa invarian (invariant mass)**, karena dapat mengindikasikan keberadaan partikel-partikel baru atau resonansi dari partikel yang telah dikenal.

Namun, proses prediksi massa invarian dari fitur-fitur hasil tabrakan menghadirkan beberapa tantangan:

1. **Pernyataan Masalah 1:** Bagaimana cara membangun model prediksi massa invarian yang akurat dari fitur-fitur tabrakan partikel seperti momentum dan sudut arah?
2. **Pernyataan Masalah 2:** Bagaimana memastikan model yang digunakan mampu bekerja secara efisien dalam skala besar dan menangani *outlier* yang sering kali merupakan sinyal penting dalam fisika partikel?
3. **Pernyataan Masalah 3:** Algoritma dan pendekatan apa yang paling efektif untuk memberikan prediksi yang akurat namun tetap mempertahankan integritas fisika dari data eksperimen?

---
### Goals

Tujuan utama dari proyek ini adalah:

- **Tujuan 1:** Mengembangkan model regresi prediktif untuk memperkirakan massa invarian elektron dari data hasil tabrakan partikel.
- **Tujuan 2:** Mengevaluasi dan mengoptimalkan berbagai model regresi berbasis pohon dan neural network untuk memastikan performa prediktif yang tinggi.
- **Tujuan 3:** Menjamin bahwa pendekatan yang digunakan mampu bekerja tanpa menghilangkan *outlier*, yang dalam konteks fisika partikel, sering kali justru mengandung informasi penting.

---

### Solution Statements

Untuk menjawab pertanyaan dan mencapai tujuan di atas, pendekatan solusi yang digunakan meliputi:

1. **Solusi 1: Implementasi dan Perbandingan Model Regresi**
   - Model yang digunakan meliputi:
     - Random Forest
     - XGBoost
     - LightGBM
     - Neural Network (Deep Learning)
   - Model dibangun untuk memprediksi nilai kontinu (massa invarian) berdasarkan 18 fitur yang tersedia dari dataset hasil eksperimen CERN.

2. **Solusi 2: Hyperparameter Tuning untuk Optimasi Kinerja**
   - Dilakukan pencarian grid (GridSearchCV) pada tiga model regresi utama:
     - **XGBoost:** Disesuaikan parameter seperti `max_depth`, `eta`, `subsample`, dan `reg_lambda`.
     - **Random Forest:** Diatur `n_estimators`, `max_depth`, `min_samples_split`, dan `max_features`.
     - **LightGBM:** Disesuaikan `max_depth`, `learning_rate`, `subsample`, `reg_lambda`, dan `n_estimators`.
   - Proses tuning ini ditujukan untuk mencapai generalisasi model yang lebih baik tanpa overfitting.

3. **Solusi 3: Eksperimen dengan Neural Network**
   - Arsitektur deep learning dirancang dengan beberapa hidden layer (256-128-64-32-1), menggunakan aktivasi ReLU dan output linear untuk regresi.
   - Meskipun memiliki performa tinggi, model ini dievaluasi terhadap model tree-based dari segi akurasi dan kecepatan pelatihan.

4. **Solusi 4: Evaluasi Menggunakan Metrik yang Tepat**
   - **Mean Squared Error (MSE):** Untuk mengukur seberapa jauh prediksi dari nilai sebenarnya.
   - **R² Score:** Untuk mengevaluasi seberapa baik model menjelaskan variasi pada data target.

Dengan pendekatan ini, proyek tidak hanya fokus pada performa prediksi semata, tetapi juga menjaga nilai-nilai penting dari data eksperimen — yaitu tetap mempertahankan outlier sebagai bagian dari analisis ilmiah.

## Data Understanding
### Sumber dan Deskripsi Dataset

Dataset yang digunakan dalam proyek ini adalah **CERN Electron Collision Data**, yang tersedia secara publik melalui platform Kaggle pada tautan berikut:  
🔗 [CERN Electron Collision Data – Kaggle](https://www.kaggle.com/datasets/fedesoriano/cern-electron-collision-data/data)

Dataset ini berisi **100.000** entri hasil eksperimen tabrakan elektron yang dilakukan oleh **CMS experiment di CERN**, yang diseleksi untuk tujuan edukasi dan outreach. Data ini sangat kaya akan fitur fisika partikel dan digunakan untuk menganalisis **massa invarian** dari pasangan elektron, yang merupakan indikator penting untuk identifikasi partikel baru dalam fisika berenergi tinggi.

---

### Fitur dalam Dataset

Dataset terdiri dari 19 fitur numerik dan kategorikal yang masing-masing merepresentasikan parameter fisika dari dua elektron hasil tabrakan. Penjelasan tiap variabel adalah sebagai berikut:

| No | Fitur       | Deskripsi                                                                 |
|----|-------------|---------------------------------------------------------------------------|
| 1  | `Run`       | Nomor run dari event (ID sesi eksperimen)                                |
| 2  | `Event`     | Nomor event individual (unik untuk tiap tabrakan)                        |
| 3  | `E1`        | Energi total elektron 1 (GeV)                                             |
| 4  | `px1`       | Komponen momentum X dari elektron 1 (GeV)                                 |
| 5  | `py1`       | Komponen momentum Y dari elektron 1 (GeV)                                 |
| 6  | `pz1`       | Komponen momentum Z dari elektron 1 (GeV)                                 |
| 7  | `pt1`       | Transverse momentum elektron 1 (GeV)                                      |
| 8  | `eta1`      | Pseudorapidity elektron 1                                                 |
| 9  | `phi1`      | Sudut phi (rad) elektron 1                                                |
| 10 | `Q1`        | Muatan (charge) elektron 1                                                |
| 11 | `E2`        | Energi total elektron 2 (GeV)                                             |
| 12 | `px2`       | Komponen momentum X dari elektron 2 (GeV)                                 |
| 13 | `py2`       | Komponen momentum Y dari elektron 2 (GeV)                                 |
| 14 | `pz2`       | Komponen momentum Z dari elektron 2 (GeV)                                 |
| 15 | `pt2`       | Transverse momentum elektron 2 (GeV)                                      |
| 16 | `eta2`      | Pseudorapidity elektron 2                                                 |
| 17 | `phi2`      | Sudut phi (rad) elektron 2                                                |
| 18 | `Q2`        | Muatan (charge) elektron 2                                                |
| 19 | `M`         | **Massa invarian** dari pasangan elektron (target regresi) (GeV)          |

---

### Eksplorasi Data dan Visualisasi

Untuk memahami distribusi dan karakteristik awal dari data, dilakukan beberapa tahapan eksplorasi data berikut:

1. **Histogram Target (`M`)**  
   Visualisasi histogram pada target variable `M` menunjukkan distribusi massa invarian yang tidak normal dan memiliki beberapa puncak (multimodal), yang menunjukkan adanya kemungkinan resonansi partikel yang berbeda.
    ![Histogram](https://github.com/bisat19/CERN-Predictive-Analysis/blob/main/image/download%20(3).png)

3. **Correlation Matrix**  
   Matriks korelasi digunakan untuk melihat hubungan antar fitur. Beberapa fitur momentum dan energi menunjukkan korelasi kuat terhadap target `M`, yang mengindikasikan relevansi tinggi dalam proses prediksi.
   ![Correlation Matrix](https://github.com/bisat19/CERN-Predictive-Analysis/blob/main/image/download%20(4).png)

4. **Boxplot Target (`M`)**  
   Visualisasi boxplot menunjukkan adanya *outlier* signifikan pada massa invarian. Dalam konteks fisika partikel, *outlier* seperti ini justru penting karena bisa menunjukkan peristiwa langka seperti deteksi partikel eksotik.
   ![Boxplot](https://github.com/bisat19/CERN-Predictive-Analysis/blob/main/image/download%20(5).png)


## Data Preparation
Sebelum memulai proses pelatihan model, dilakukan beberapa tahap *data preparation* untuk memastikan bahwa data dalam kondisi bersih, lengkap, dan sesuai untuk dianalisis oleh algoritma machine learning. Pada proyek ini, dataset yang digunakan adalah hasil eksperimen tabrakan partikel dari CERN yang terdiri dari 100.000 entri data dengan 19 kolom numerik.

Berikut ini adalah langkah-langkah yang dilakukan:

### 1. Penanganan Nilai Kosong (Missing Values)

Setelah dilakukan inspeksi awal terhadap data, ditemukan adanya nilai kosong (NaN) pada kolom target yaitu `M` (invariant mass). Massa invarian adalah variabel target utama dalam proyek ini, sehingga penting untuk mengatasi ketidakhadirannya.

Langkah yang diambil:
- Mengisi nilai kosong pada kolom `M` menggunakan rata-rata (mean) dari kolom tersebut.
- Pendekatan ini dipilih karena:
  - `M` adalah variabel numerik kontinu.
  - Jumlah data yang hilang relatif sedikit dibandingkan total dataset.
  - Nilai rata-rata tidak akan mengganggu distribusi secara signifikan.
  - Outlier dalam fisika partikel dianggap penting, sehingga imputasi yang sederhana dianggap paling aman.kah data preparation yang dilakukan:
---
### 2. Penghapusan Duplikasi
Data duplikat dapat memperburuk kinerja model dengan cara memberikan bobot lebih terhadap informasi yang redundan. Oleh karena itu, dilakukan pemeriksaan dan penghapusan seluruh baris yang merupakan duplikat.

---
### 3. Pemeriksaan dan Penyesuaian Tipe Data
Seluruh fitur pada dataset ini terdiri dari angka numerik kontinu (float/integer). Karena itu:
- Tidak diperlukan teknik encoding seperti One-Hot Encoding atau Label Encoding.
- Tidak dilakukan normalisasi atau standardisasi awal karena model utama yang digunakan adalah tree-based (XGBoost, Random Forest, LightGBM), yang tidak sensitif terhadap skala data.
---
### 4. Standardisasi Fitur untuk Neural Network
Untuk model Neural Network (Deep Learning), dilakukan proses standardisasi fitur menggunakan StandardScaler dari scikit-learn. Ini bertujuan untuk:
- Meningkatkan stabilitas dan kecepatan proses pelatihan.
- Menghindari dominasi fitur dengan skala besar terhadap fitur lain yang berskala kecil.
- Mempercepat konvergensi dalam proses backpropagation.


## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

