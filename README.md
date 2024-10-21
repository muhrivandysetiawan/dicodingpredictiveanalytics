# Dicoding Predictive Analytics - Prediksi Harga British Pound Sterling ke United States Dollar
Predictive Analytics Dicoding Tentang Pergerakan Harga Mata Uang Pound Sterling terhadap United States Dollar 

**Latar Belakang**: <br>
GBP/USD adalah pasangan mata uang yang mencerminkan nilai tukar antara Poundsterling Inggris (GBP) dan Dolar Amerika Serikat (USD). Ketika menganalisis pada suatu grafik harga GBP/USD, misalnya 1.2800, artinya 1 Poundsterling setara dengan 1.2800 Dolar AS. Pertukaran Nilai Pound Sterling (GBP) terhadap Dolar AS (USD) merupakan salah satu pasokan mata uang yang  penting dalam perdagangan antar dua negara. Pertukaran niali ini mempengaruhi harga barang dan jasa antara kedua negara, serta investasi dan kebijakan moneter. Nilai tukar yang fluktuatif ini bisa disebabkan oleh berbagai faktor seperti perubahan kebijakan fiskal dan moneter, kondisi ekonomi global, dan kecemasan investasi.

**Masalah yang Perlu Diselesaikan**: <br>
Masalah utama dari kasus ini adalah sering terjadi volatilitas nilai tukar yang dapat menimbulkan ketidakpastian ekonomi dan dampak negatif dalam suatu perdagangan. Perubahan nilai tukar yang drastis dapat menyebabkan ketidakstabilan pasar, meningkatkan biaya impor, dan mengurangi daya saing produk domestik.

**Penyelesaian**: <br>
Untuk menyelesaikan masalah ini, diperlukan kebijakan yang tepat dari pemerintah dan bank sentral dari kedua negara, baik dari pihak Inggris maupun pihak Amerika Serikat untuk menjaga stabilitas nilai tukar. Kebijakan fiskal yang sehat dan kebijakan moneter yang tepat dapat membantu mengurangi volatilitas. Selain itu, kerjasama internasional dan komunikasi yang baik antara negara-negara juga penting untuk menjaga stabilitas pasar mata uang.


# Business Understanding

Berdasarkan latar belakang yang telah dipaparkan di atas, berikut ini adalah permasalahan dan tujuan yang diperoleh adalah sebagai berikut:
- **Problem Statements**: <br>
  1. Bagaimana cara memprediksi fluktuasi nilai tukar mata uang GBP/USD dengan akurasi tinggi untuk mendukung pengambilan keputusan investasi dan bisnis?
  2. Bagaimana cara mereduksi dimensi data historis nilai tukar GBP/USD tanpa kehilangan informasi penting untuk meningkatkan kinerja model machine learning?
- **Goals**:<br>
  1. Mengembangkan model yang dapat memprediksi nilai tukar GBP/USD dengan akurasi tinggi.
  2. Mengurangi dimensi data historis nilai tukar GBP/USD tanpa kehilangan informasi penting.
  
Dari Problem Statement dan Goals di atas, solusi yang ditawarkan adalah sebagai berikut: <br>
**Solution Statement**: <br>
1. Model LSTM (Long Short-Term Memory) digunakan untuk mempelajari pola historis dan menghasilkan prediksi nilai tukar GBP/USD pada beberapa hari ke depan.
2. Principal Component Analysis (PCA) digunakan untuk mereduksi dimensi data, sehingga model machine learning dapat bekerja lebih efektif dan efisien.

# Data Understanding

Data yang diambil untuk proyek ini adalah data harga GBP/USD yang meliputi Date, Price, Open, High, Low, Volume, dan Change %. Dikarenakan nilai Volume ddalam data ini tidak dicantumkan, maka bisa dihapus dan menyisakan Date, Price, Open, High, Low, dan Change %. Data ini diambil dari 1 Januari 2014 sampai 14 Oktober 2024 karena proyek ini meneliti perkebangan pertukaran nilai ini dalam 10 tahun terakhir. <br>
Sumber datanya adalah sebagai berikut: <br>
[https://www.investing.com/currencies/gbp-usd-historical-data]  <br>
Tips: Data ini bisa diambil sesuai dengan keinginan. Misalnya data diambil dari 2019 sampai 2024, dan 2010 sampai 2024.

| No.| Kolom    | Jumlah Data | Tipe Data | Penjelasan                                      |
|----|----------|-------------|-----------|-------------------------------------------------|
| 1  | Date     | 2816        | Object    | Tanggal transaksi atau pengukuran               |
| 2  | Price    | 2816        | Float64   | Harga penutupan pada tanggal tersebut           |
| 3  | Open     | 2816        | Float64   | Harga pembukaan pada tanggal tersebut           |
| 4  | High     | 2816        | Float64   | Harga tertinggi pada tanggal tersebut           |
| 5  | Low      | 2816        | Float64   | Harga terendah pada tanggal tersebut            |
| 6  | Change % | 2816        | Object    | Persentase perubahan harga dari hari sebelumnya |

Ini adalah isi data dari harga British Pound Sterling dalam US Dollar. Tipe data ini tidak bisa dipakai untuk melakukan analisis univariat, maka harus diubah menjadi datetime64 dan float64 agar bisa diperkirakan. Hasilnya terdapat tabel di bawah ini:

| No.| Kolom    | Jumlah Data | Tipe Data      | Penjelasan                                      |
|----|----------|-------------|----------------|-------------------------------------------------|
| 1  | Date     | 2816        | datetime64[ns] | Tanggal transaksi atau pengukuran               |
| 2  | Price    | 2816        | Float64        | Harga penutupan pada tanggal tersebut           |
| 3  | Open     | 2816        | Float64        | Harga pembukaan pada tanggal tersebut           |
| 4  | High     | 2816        | Float64        | Harga tertinggi pada tanggal tersebut           |
| 5  | Low      | 2816        | Float64        | Harga terendah pada tanggal tersebut            |
| 6  | Change % | 2816        | Float64        | Persentase perubahan harga dari hari sebelumnya |

Pada tabel di bawah ini, dijelaskan status harga dari 4 kolom, mulai dari frekuensi, rata-rata,standar deviasi, median, kuartil 1, kuartil 3, minimal, dan maksimal. 

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
1. Price <br>
![Image 1](https://github.com/user-attachments/assets/880fe418-25d9-4ba7-a6cf-c11c6dfc5082)
2. Open <br>
![Image 2](https://github.com/user-attachments/assets/27a66147-8764-439c-958b-3ea2db640575)
3. High <br>
![Image 3](https://github.com/user-attachments/assets/98496ef8-a7bf-4135-8eb8-972a4983ca82)
4. Low <br>
![Image 4](https://github.com/user-attachments/assets/a4fcae87-619b-402b-8a81-a57010604b5f)
5. Change % <br>
![Image 5](https://github.com/user-attachments/assets/9dd7d3d4-29a8-4416-ad17-f2d9b54165db)

Analisis univariat adalah jenis analisis data yang hanya melibatkan satu variabel pada satu waktu sedangkan Analisis multivariat adalah jenis analisis data yang melibatkan lebih dari satu variabel secara bersamaan.

**Analisis Univariat**:
1. Price <br>
![Image 6](https://github.com/user-attachments/assets/b0df03d4-25e5-4760-9966-ab10fbbba17f)
2. Open <br>
![Image 7](https://github.com/user-attachments/assets/32e4cfe7-cd12-416c-a92e-2445aa5bf997)
3. High <br>
![Image 8](https://github.com/user-attachments/assets/62ea63f1-a0c9-4935-aeac-04e1c57da090)
4. Low <br>
![Image 9](https://github.com/user-attachments/assets/748d9e4b-b1fd-41d4-b1ee-f50309452f2d)
5. Change % <br>
![Image 10](https://github.com/user-attachments/assets/48fc95c1-d03b-4540-9d96-32db4d2783f5)


Ini adalah diagram Pair GBPUSD dari 1 Januari 2014 sampai 16 Oktober 2024 yang terdiri dari Price sebagai label x dan Date sebagai label y: <br>
![Image 11](https://github.com/user-attachments/assets/1f9ba653-16c3-483f-8ad4-f0a2f40b2864)

Ini juga adalah diagram perubahan kenaikan dan penurunan pair GBPUSD dari 1 Januari 2014 sampai 16 Oktober 2024 yang terdiri dari Date sebagai label x dan Change % sebagai label y: <br>
![Image 12](https://github.com/user-attachments/assets/9329699d-4c45-4f9f-a869-1ce5ed106711)

**Analisis Multivariat**:

Analisis ini merupakan gabungan dari kolom Price, Open, High Low sebagai label x da Date sebagai label y <br>
![Image 13](https://github.com/user-attachments/assets/f80ca5b5-f6f7-4abf-935e-7d7a8e615f89)

Pairplot adalah jenis visualisasi yang digunakan untuk melihat distribusi dan hubungan antar beberapa variabel dalam dataset. Pairplot menghasilkan scatter plots untuk setiap pasangan variabel, serta histogram atau KDE plots untuk distribusi dari masing-masing variabel di diagonal. Ini membantu dalam mengidentifikasi pola, korelasi, dan outliers dalam data.

Correlation Matrix adalah tabel yang menunjukkan koefisien korelasi antara setiap pasangan variabel dalam dataset. Nilai korelasi berkisar dari -1 hingga 1, di mana:
- 1 menunjukkan korelasi positif sempurna
- 0 menunjukkan tidak ada korelasi
- -1 menunjukkan korelasi negatif sempurna

Matrix ini sangat berguna untuk mengidentifikasi variabel-variabel yang berkaitan erat satu sama lain dan bisa memberikan wawasan tentang hubungan linear dalam data.

Berikut ini adalah Pairplot dan Correlation Matrix dari kolo yang tersedia:
1. Pairplot <br>
![Image 14](https://github.com/user-attachments/assets/b313a52a-2793-4783-a554-5f8adc691153)
1. Correlation Matrix <br>
![Image 15](https://github.com/user-attachments/assets/6bc55a17-56c6-4f24-a0f8-16bb6d15d50c)

# Data Preparation
Persiapan Data yang telah dilakukan adalah sebagai berikut:
1. Pengumpulan Data
2. Data Cleaning (Menghilangkan Kolom Volume)
3. Data Convert (Mengubah data Date dan Change % menjadi datetime64 dan float64)
4. Exploratory Data Analysis (EDA)
5. Principal Component Analysis (PCA)
6. Menggunakan MinMaxScaler
7. Menerapkan Window Dataset


Langkah yang dilakukan untuk persiapan data adalah sebagai berikut: <br>
1. Melakukan PCA dengan menggunakan PCA dari sklearn
2. Menginterpretasikan Komponen Utama denganmelihat varians yang dijelaskan oleh masing-masing komponen
3. Menggunakan MinMaxScaler
4. Menerapkan Window Dataset

Menjelaskan proses data preparation yang dilakukan <br>
Alasan melakukan persiapan data menggunakan PCA sebagai berikut: <br>
- Reduksi Dimensi: PCA membantu mengurangi jumlah fitur dalam dataset, yang dapat meningkatkan kinerja dan mengurangi overfitting dalam model prediksi. <br>
- Meningkatkan Efisiensi: Dengan mengurangi jumlah fitur, waktu komputasi untuk pelatihan model juga berkurang. <br>
- Mengatasi Multikolinearitas: PCA dapat mengatasi masalah multikolinearitas dengan mengubah fitur asli menjadi sekumpulan komponen utama yang orthogonal satu sama lain. <br>

Alasan melakukan persiapan data menggunakan MinMaxScaler adalah agar bisa mencegah fitur dengan skala yang lebih besar mendominasi proses pelatihan model.Fitur ini sangat penting saat menggabungkan fitur dengan satuan atau skala yang berbeda.

Alasan melakukan persiapan data menggunakan Window Dataset adalah agar model ini dapat belajar ketergantungan temporal dalam data. Model ini dapat lebih memahami urutan dan meningkatkan akurasi prediksinya untuk data masa depan.

# Modeling

LSTM (Long Short-Term Memory) adalah jenis jaringan saraf tiruan yang digunakan dalam deep learning untuk menangani data urutan atau time series. LSTM sangat efektif untuk tugas yang melibatkan data urutan panjang seperti prediksi harga saham atau pasangan mata uang (seperti GBP/USD), pemrosesan bahasa alami (NLP), dan prediksi cuaca.

Ini adalah tabel untuk modelling LSTM
| Layer (type)       | Output Shape      | Parameter |
|--------------------|-------------------|-----------|
| lstm (LSTM)        | (None, None, 64)  | 16,896    |
| dropout (Dropout)  | (None, None, 64)  | 0         |
| lstm_1 (LSTM)      | (None, 100)       | 66,000    |
| dropout_1 (Dropout)| (None, 100)       | 0         |
| dense (Dense)      | (None, 50)        | 5,050     | 
| dense_1 (Dense)    | (None, 1)         | 51        |

**Kelebihan LSTM**: Mampu menangani data sekuensial dengan lebih baik, mampu mengatasi masalah vanishing gradient.
**Kekurangan LSTM**:  Memerlukan waktu pelatihan yang lebih lama, lebih kompleks dibandingkan model tradisional.

Improvisasi pada proyek di atas adalah
1. SGD dengan Momentum, parameter ini mempercepat proses pelatihan dengan melewati gradien yang kecil.
2. Adam Optimizer, parameter ini efektif dalam menangani gradien yang jarang terjadi dengan mengadaptasi laju pembelajaran.
3. Huber Loss dengan MAE, parameter ini digunakan untuk mengukur Error dalam Time Series. 

# Evaluation

MAE adalah rata-rata dari selisih absolut antara nilai prediksi dan nilai aktual. Semakin rendah MAE, semakin akurat prediksi model. MAE menunjukkan seberapa besar rata-rata kesalahan yang kita buat dalam satuan asli data, misalnya dalam dolar jika kita memprediksi harga.
![Image 19](https://github.com/user-attachments/assets/072990da-7f18-47c9-bb18-43fdfb5ba7ab)

dimana di mana 𝑦𝑖 adalah nilai sebenarnya dan 𝑦^𝑖 adalah prediksi model. Semakin kecil nilai Loss, semakin baik model dalam memprediksi data dengan akurasi yang lebih tinggi.

Loss adalah suatu fungsi yang digunakan untuk minimalisir perbedaan antara nilai prediksi dan nilai aktual. Contoh Loss yang digunakan adalah Mean Squared Error (MSE) atau Huber Loss. Loss ini memiliki fungsi untuk membantu algoritma belajar dengan memberikan sinyal sejauh mana prediksi dari target sebenarnya.

Loss ini dihitung menggunakan rumus Mean Squared Error (MSE) untuk masalah ini, yang diformulasikan sebagai:
![Image 20](https://github.com/user-attachments/assets/07c889ec-7bdb-4d47-abc1-12c6111e3dc1)

di mana:
𝑛 = Jumlah data
𝑦𝑖 = Nilai sebenarnya untuk data ke-𝑖
𝑦^𝑖 = Nilai prediksi dari model untuk data ke-𝑖

MAE mengukur seberapa besar rata-rata kesalahan absolut antara nilai sebenarnya dan prediksi, tanpa mengkuadratkan kesalahan tersebut. Karena itu, nilai MAE menunjukkan seberapa jauh model berada dari nilai aktual secara langsung dalam unit yang sama dengan data.

Ini adalah hasil model pelatihan pada variabel Loss <br>
![Image 16](https://github.com/user-attachments/assets/c3afc450-136c-4bf6-baa6-71b716a53e41)

Pada grafik di atas, terlihat perubahan nilai loss selama proses pelatihan model. Garis biru menunjukkan loss pada data pelatihan, sementara garis oranye menunjukkan loss pada data validasi. Grafik ini menunjukkan bahwa loss pada data pelatihan dan validasi cenderung menurun seiring bertambahnya jumlah epoch, meskipun terdapat beberapa fluktuasi. Hal ini mengindikasikan bahwa model mengalami proses pelatihan yang baik dan mampu meminimalisir kesalahan prediksi. Grafik menunjukkan bahwa pada awal pelatihan, Training Loss dan Validation Loss cukup tinggi namun menurun seiring bertambahnya epoch, meskipun Validation Loss tampak berfluktuasi secara signifikan. <br>

Pada titik akhir pelatihan, perlu disebutkan nilai Loss untuk Training dan Validation saat model berhenti (misalnya, di epoch 200). Dari grafik, terlihat Training Loss lebih stabil dan rendah dibandingkan Validation Loss. <br>

Ini adalah hasil model pelatihan pada variabel MAE <br>
![Image 17](https://github.com/user-attachments/assets/b7058c03-e3da-4942-aa1d-f65890839387)

Grafik di atas menampilkan nilai Mean Absolute Error (MAE) pada model selama proses pelatihan. Garis biru menunjukkan MAE pada data pelatihan, sementara garis oranye menunjukkan MAE pada data validasi. Terlihat bahwa nilai MAE secara umum menurun seiring bertambahnya jumlah epoch, meskipun terdapat beberapa fluktuasi pada garis oranye, mengindikasikan bahwa model semakin baik dalam memprediksi nilai target. Grafik itu juga tampak bahwa Training MAE konsisten menurun dan stabil setelah beberapa epoch, sedangkan Validation MAE mengalami fluktuasi besar, menunjukkan adanya variasi dalam performa model pada data validasi.

Nilai MAE pada akhir pelatihan (epoch terakhir) yang tercantum adalah sebesar 0.015185105614364147, dimana hasil MAE itu cukup kecil dan nilai prediksi cukup rapat dengan nilai sebenarnya.

Berikut ini adalah hasil prediksi dari pelatihan di bawah ini
![Image 18](https://github.com/user-attachments/assets/7ce69426-9e29-4543-a592-5271d4d30e39)
dimana garis merah adalah Harga Prediksi dan garis biru adalah Prediksi yang sebenarnya.   


# Kesimpulan 
Berdasarkan hasil proyek ini, model LSTM yang dikembangkan berhasil memprediksi nilai tukar GBP/USD dengan akurasi yang cukup baik, seperti terlihat pada grafik hasil prediksi yang menunjukkan tren yang mirip antara harga aktual dan prediksi. Penggunaan PCA untuk reduksi dimensi data historis terbukti efektif dalam meningkatkan efisiensi model tanpa kehilangan informasi penting, yang tercermin dari performa model yang baik. Meskipun masih ada ruang untuk perbaikan, proyek ini telah mencapai tujuannya dalam mengembangkan model prediksi nilai tukar yang akurat dan menerapkan teknik reduksi dimensi yang efektif.

Berikut ini adalah kelebihan hasil dari proyek ini adalah:
1. Penggunaan model LSTM yang tepat untuk kasus time series keuangan, memungkinkan model untuk menangkap pola kompleks dalam pergerakan nilai tukar GBP/USD.
2. Penerapan PCA untuk reduksi dimensi membantu meningkatkan efisiensi komputasi dan mengurangi potensi overfitting.
3. Implementasi teknik preprocessing yang komprehensif, termasuk MinMaxScaler dan Window Dataset dimana teknik ini membantu meningkatkan kinerja model.
4. Visualisasi yang cukup baik untuk analisis univariat dan multivariat, membantu pemahaman mendalam tentang karakteristik data.
5. Penggunaan metrik evaluasi yang relevan, baik dari MAE dan Loss untuk mengukur kinerja model dalam konteks prediksi nilai tukar.

Berikut ini adalah kelebihan hasil dari proyek ini adalah:
1. Tidak adanya perbandingan dengan model baseline atau model alternatif, yang bisa memberikan konteks lebih baik tentang seberapa baik kinerja model LSTM.
2. Kurangnya analisis mendalam tentang faktor-faktor eksternal yang memengaruhi nilai tukar, seperti kebijakan moneter atau peristiwa geopolitik.
3. Tidak disebutkan adanya validasi silang atau pengujian pada data out-of-sample untuk memastikan generalisasi model.
4. Kurangnya penjelasan tentang interpretasi hasil PCA dan bagaimana komponen utama dipilih untuk digunakan dalam model.
5. Tidak adanya diskusi tentang potensi overfitting atau underfitting, yang penting dalam evaluasi model machine learning.Kurangnya analisis tentang implikasi praktis dari hasil prediksi, seperti bagaimana model ini bisa digunakan dalam pengambilan keputusan investasi atau bisnis.

**Referensi**: <br>
Investing.com. (n.d.). Harga Mata Uang Pound Sterling terhadap US Dollar. Retrieved from https://id.investing.com/currencies/gbp-usd?form=MG0AV3
