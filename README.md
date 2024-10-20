# Dicoding Predictive Analytics - Prediksi Harga British Pound Sterling ke United States Dollar
Predictive Analytics Dicoding Tentang Pergerakan Harga Mata Uang Pound Sterling terhadap United States Dollar 

# Domain Investing

**Latar Belakang**: <br>
GBP/USD adalah pasangan mata uang yang mencerminkan nilai tukar antara Poundsterling Inggris (GBP) dan Dolar Amerika Serikat (USD). Ketika melihat kuotasi harga GBP/USD, misalnya 1.2800, itu berarti 1 Poundsterling setara dengan 1.2800 Dolar AS. Nilai tukar Pound Sterling (GBP) terhadap Dolar AS (USD) merupakan salah satu pasokan mata uang yang sangat penting dalam perdagangan internasional. Nilai tukar ini mempengaruhi harga barang dan jasa antara kedua negara, serta investasi dan kebijakan moneter. Fluktuasi nilai tukar ini dapat disebabkan oleh berbagai faktor seperti perubahan kebijakan fiskal dan moneter, kondisi ekonomi global, dan kekhawatiran investasi.

**Masalah yang Perlu Diselesaikan**: <br>
Masalah utama dari kasus ini adalah sering terjadi volatilitas nilai tukar yang dapat menimbulkan ketidakpastian ekonomi dan dampak negatif dalam suatu perdagangan. Perubahan nilai tukar yang drastis dapat menyebabkan ketidakstabilan pasar, meningkatkan biaya impor, dan mengurangi daya saing produk domestik.

**Penyelesaian**: <br>
Untuk menyelesaikan masalah ini, diperlukan kebijakan yang tepat dari pemerintah dan bank sentral dari kedua negara, baik dari pihak Inggris maupun pihak Amerika Serikat untuk menjaga stabilitas nilai tukar. Kebijakan fiskal yang sehat dan kebijakan moneter yang tepat dapat membantu mengurangi volatilitas. Selain itu, kerjasama internasional dan komunikasi yang baik antara negara-negara juga penting untuk menjaga stabilitas pasar mata uang.

**Referensi**: <br>
Investing.com. (n.d.). Harga Mata Uang Pound Sterling terhadap US Dollar. Retrieved from https://id.investing.com/currencies/gbp-usd?form=MG0AV3

# Business Understanding

Berdasarkan latar belakang yang telah dipaparkan di atas, berikut ini adalah permasalahan dan tujuan yang diperoleh adalah sebagai berikut:
- **Problem Statements**:
  1. Volatilitas Harga: Bagaimana cara mengatasi fluktuasi nilai tukar GBP/USD yang tinggi yang dapat menyebabkan ketidakpastian dalam perdagangan dan investasi internasional?
  2. Faktor Eksternal: Harga GBP/USD dipengaruhi oleh banyak faktor eksternal seperti kebijakan moneter, ekonomi global, dan stabilitas politik, yang dapat mempersulit prediksi yang akurat.
- **Goals**:
  1. Analisis Mendalam: Mengembangkan model prediksi yang lebih akurat dengan menggunakan data historis dan metode analisis canggih.
  2. Stabilitas Ekonomi: Memberikan rekomendasi kebijakan kepada pembuat kebijakan untuk membantu menjaga stabilitas nilai tukar dan mengurangi volatilitas yang berlebihan.

Dari Problem Statement dan Goals di atas, solusi yang ditawarkan adalah sebagai berikut:
**Solution Statement**:
1. Menggunakan metode Exploratory Data Analysis/(EDA) yang meliputi Analisis Univariat dan Multivariat untuk melihat data tanggal dan harga GBP/USD sebelum melakukan time series.
2. Menggunakan metode pelatihan Long Short Term Memory/(LSTM) yang dirancang untuk melatih perubahan harga GBP/USD dibandingkan menggunakan data tradisional seperti Auto Regressive Integrated Moving Average/(ARIMA).

# Data Understanding

Data yang diambil untuk proyek ini adalah data harga GBP/USD yang meliputi Date, Price, Open, High, Low, Volume, dan Change %. Dikarenakan nilai Volume ddalam data ini tidak dicantumkan, maka bisa dihapus dan menyisakan Date, Price, Open, High, Low, dan Change %. Data ini diambil dari 1 Januari 2014 sampai 14 Oktober 2024. 
Sumber datanya adalah sebagai berikut: <br>
[https://www.investing.com/currencies/gbp-usd-historical-data]
Tips: Data ini bisa diambil sesuai dengan keinginan. Misalnya data diambil dari 2019 sampai 2024, dan 2010 smapai 2024.

| No.| Kolom    | Jumlah Data | Tipe Data | Penjelasan                                      |
|----|----------|-------------|-----------|-------------------------------------------------|
| 1  | Date     | 2816        | Object    | Tanggal transaksi atau pengukuran               |
| 2  | Price    | 2816        | Float64   | Harga penutupan pada tanggal tersebut           |
| 3  | Open     | 2816        | Float64   | Harga pembukaan pada tanggal tersebut           |
| 4  | High     | 2816        | Float64   | Harga tertinggi pada tanggal tersebut           |
| 5  | Low      | 2816        | Float64   | Harga terendah pada tanggal tersebut            |
| 6  | Change % | 2816        | Object    | Persentase perubahan harga dari hari sebelumnya |

Ini adalah isi data dari harga . Tipe data ini tidak bisa dipakai untuk melakukan analisis univariat, maka harus diubah menjadi datetime64 dan float64 agar bisa diperkirakan. Hasilnya terdapat tabel di bawah ini:

| No.| Kolom    | Jumlah Data | Tipe Data      | Penjelasan                                      |
|----|----------|-------------|----------------|-------------------------------------------------|
| 1  | Date     | 2816        | datetime64[ns] | Tanggal transaksi atau pengukuran               |
| 2  | Price    | 2816        | Float64        | Harga penutupan pada tanggal tersebut           |
| 3  | Open     | 2816        | Float64        | Harga pembukaan pada tanggal tersebut           |
| 4  | High     | 2816        | Float64        | Harga tertinggi pada tanggal tersebut           |
| 5  | Low      | 2816        | Float64        | Harga terendah pada tanggal tersebut            |
| 6  | Change % | 2816        | Float64        | Persentase perubahan harga dari hari sebelumnya |

Pada tabel di bawah ini, dijelaskan status harga dari 4 kolom, mulai dari rata-rata,standar deviasi, median, kuartil 1, kuartil 3, minimal, dan maksimal. 

| Status | Price     | Open      | High      | Low       |
|--------|-----------|-----------|-----------|-----------|
| count  | 2816      | 2816      | 2816      | 2816      |
| mean   | 1.351450  | 1.351648  | 1.357125  | 1.345927  |
| std    | 0.131583  | 0.131646  | 0.131314  | 0.131936  |
| min    | 1.068400  | 1.069000  | 1.084000  | 1.038400  |
| 25%    | 1.262100  | 1.262300  | 1.267075  | 1.257775  |
| 50%    | 1.309250  | 1.309400  | 1.315150  | 1.304950  |
| 75%    | 1.401475  | 1.402050  | 1.409125  | 1.397925  |
| max    | 1.716600  | 1.716700  | 1.719300  | 1.714100  |

Boxplot adalah jenis visualisasi data yang digunakan untuk menunjukkan distribusi data berdasarkan lima ringkasan statistik utama: minimum, kuartil pertama (Q1), median, kuartil ketiga (Q3), dan maksimum. Ini juga menunjukkan potensi outliers atau nilai ekstrim dalam data. Boxplot dapat membantu dalam analisis awal data historis GBP/USD dengan memberikan gambaran tentang distribusi dan variabilitas harga. Ini sangat penting untuk memahami Volatilitas, Trend Analysis, dan Outliers

Berikut ini adalah Boxplot dari berbagai kolom
1. Price
2. Open
3. High
4. Low
5. Change %

Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

# Data Preparation
Menerapkan dan menyebutkan teknik data preparation yang dilakukan.
Teknik yang digunakan pada notebook dan laporan harus berurutan.

Menjelaskan proses data preparation yang dilakukan
Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.


# Modeling
Membuat model machine learning untuk menyelesaikan permasalahan.
Menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. Jelaskan proses improvement yang dilakukan.
Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. Jelaskan mengapa memilih model tersebut sebagai model terbaik.

# Evaluation
Menyebutkan metrik evaluasi yang digunakan.
Menjelaskan hasil proyek berdasarkan metrik evaluasi.
Metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

Menjelaskan metrik evaluasi yang digunakan untuk mengukur kinerja model. Misalnya, menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.


Struktur Laporan
Laporan harus dapat dimengerti oleh pembaca dengan mengikuti beberapa ketentuan sebagai berikut :

Mengikuti struktur yang benar dan terorganisir sesuai template laporan.

Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
Resources (seperti gambar) harus bisa dimuat dengan baik oleh reader jika menggunakan markdown.
