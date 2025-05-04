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

Pada bagian ini, kamu perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Statement” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution statement. Misalnya, menggunakan dua atau lebih algoritma untuk mencapai solusi yang diinginkan atau melakukan improvement pada baseline model dengan hyperparameter tuning.
    - Solusi yang diberikan harus dapat terukur dengan metrik evaluasi.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

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

