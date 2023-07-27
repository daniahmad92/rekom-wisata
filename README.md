# Laporan Proyek Machine Learning:Sistem Rekomendasi Destinasi Wisata Indonesia- Dadan Ahmad Dani

## Project Overview

  Pariwisata merupakan salah satu sektor ekonomi yang memiliki peran penting dalam pertumbuhan dan pembangunan suatu negara. Di Indonesia, sektor pariwisata telah menjadi salah satu kontributor utama bagi perekonomian negara.Menurut laporan Badan Pusat Statistik (BPS), kunjungan wisman pada periode Januari hingga April 2023 meningkat sebesar 393,83 persen dibandingkan dengan periode yang sama pada tahun sebelumnya, yaitu tahun 2022. Angka pertumbuhan yang sangat signifikan ini mencerminkan pemulihan sektor pariwisata Indonesia setelah menghadapi tantangan besar akibat pandemi COVID-19 yang melanda dunia sejak tahun 2020 [[1]](https://www.bps.go.id/pressrelease/2023/06/05/1978/peningkatan-kunjungan-wisatawan-mancanegara-pada-april-2023-yang-tumbuh-276-31-persen-dibandingkan-april-2023-dan-jumlah-penumpang-angkutan-laut-dalam-negeri-pada-april-2023-naik-24-75-persen.html).

  Pertumbuhan kunjungan wisman yang signifikan pada Januari hingga April 2023, seperti yang diungkapkan oleh Badan Pusat Statistik (BPS), menunjukkan bahwa ada peluang besar bagi industri pariwisata Indonesia untuk memanfaatkan data wisman yang masuk dan mengoptimalkan pengalaman wisata mereka. Inilah saat yang tepat untuk mengintegrasikan sistem rekomendasi berbasis machine learning dalam industri pariwisata untuk memberikan pengalaman wisata yang lebih personal dan relevan bagi para wisman yang datang ke Indonesia.Dengan demikian, Pengalaman wisata yang disesuaikan dengan minat individu ini akan meningkatkan kepuasan wisman dan membantu meningkatkan citra Indonesia sebagai destinasi pariwisata yang menarik dan berkualitas.

## Business Understanding



### Problem Statements

Berdasarkan latar belakang yang telah dipaparkan sebelumnya, maka rumusan masalah dalam proyek ini adalah:

Bagaimana mengintegrasikan sistem rekomendasi berbasis machine learning  dalam industri pariwisata untuk memberikan pengalaman wisata yang lebih personal dan relevan bagi para wisman yang datang ke Indonesia?


### Goals

 Proyek ini bertujuan untuk mencari solusi dan implementasi terbaik dalam mengintegrasikan sistem rekomendasi berbasis machine learning dalam industri pariwisata Indonesia untuk meningkatkan pengalaman wisatawan dan mendukung perkembangan pariwisata secara berkelanjutan 

### Solution statements

Integrasi sistem rekomendasi berbasis machine learning dalam industri pariwisata untuk memberikan pengalaman wisata yang lebih personal dan relevan bagi para wisman dapat dilakukan melalui beberapa langkah strategis berikut:

1. Penerapan Content Based Filtering pada model machine learning:

Content Based Filtering adalah salah satu pendekatan dalam sistem rekomendasi yang menganalisis konten dari tempat wisata, penginapan, dan aktivitas wisata. Berdasarkan data yang telah dikumpulkan, sistem dapat menyajikan rekomendasi yang sesuai dengan minat wisman berdasarkan kesesuaian dengan konten yang telah disukai atau dipilih sebelumnya oleh wisman tersebut. Misalnya, jika seorang wisman tertarik pada destinasi alam, sistem akan merekomendasikan tempat wisata dengan fokus pada alam yang serupa

2. Implementasi Collaborative Filtering pada model machine learning:

Collaborative Filtering adalah metode yang memanfaatkan pola kesamaan dan kesesuaian minat antara wisatawan lain untuk memberikan rekomendasi. Dengan menggunakan data dari banyak wisatawan, sistem dapat mengidentifikasi tren dan pola minat yang serupa. Jika sejumlah besar wisatawan memiliki minat terhadap destinasi budaya, sistem dapat merekomendasikan tempat wisata budaya yang populer kepada wisatawan lain dengan minat serupa.



## Data Understanding


### Informasi Dataset

Dataset yang digunakan dalam proyek ini adalah dataset [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination) yang diambil dari Kaggle dengan `tourism_with_id.csv` dan `tourism_rating.csv` sebagai dataset yang digunakan.

##### Dataset Lokasi Wisata (tourism_with_id.csv)
  
  Dataset  `tourism_with_id.csv` , memiliki 11 kolom dan 437 baris.  Dari 11 kolom, terdapat 2 kolom yang memiliki tipe data integer, 4 float dan 5 object. Adapun Deskripsi dari masing masing variabel dapat dilihat pada Tabel 1 dibawah ini.

  Tabel 1. Variabel Dataset tourism_with_id

  | No  | Variabel     | Deskripsi                                            | Tipe Data   |
  | --- | ------------ | -----------------------------------------------------| ----------- |
  | 1   | Place_Id     | Id unik untuk setiap lokasi wisata                   | int64       |
  | 2   | Place_Name   | Nama dari lokasi wisata                              | object      |
  | 3   | Description  | Deskripsi singkat tentang lokasi wisata              | object      |
  | 4   | Category     | Kategori atau jenis dari lokasi wisata               | object      |
  | 5   | City         | Nama kota atau daerah tempat lokasi wisata berada    | object      |
  | 6   | Price        | Harga tiket masuk ke lokasi wisata.                  | int64       |
  | 7   | Rating       | Rating lokasi wisata tersebut                        | float64     |
  | 8   | Time_Minutes | Perkiraan waktu tempuh untuk mencapai lokasi wisata  | float64     |
  | 9   | Coordinate   | Koordinat geografis lokasi wisata.                   | object      |
  | 10  | Lat          | Latitude (garis lintang) lokasi wisata              | float64     |
  | 11  | Long         | Longitude (garis bujur) lokasi wisata.               | float64     |

##### Dataset Rating (tourism_rating.csv)
  
  Dataset  `tourism_rating.csv` , memiliki 3 kolom dan 10.000 baris. Semua kolom memiliki tipe data Integer.Adapun Deskripsi dari masing masing variabel dapat dilihat pada Tabel 2 dibawah ini.

  Tabel 2. Variabel Dataset tourism_rating.csv

  | #   | Variabel      | Deskripsi                                                             | Dtype |
  | --- | ------------- | --------------------------------------------------------------------  | ----- |
  | 0   | User_Id       | Id unik wisatawan                                                       | int64 |
  | 1   | Place_Id      | Id unik untuk setiap lokasi wisata                                    | int64 |
  | 2   | Place_Ratings | Rating yang diberikan oleh wisatawan terhadap tempat wisata tersebut  | int64 |


### Pengecekan Missing Value
  
  Proses pengecekan data yang hilang atau Missing Value dilakukan pada semua dataset baik dataset lokasi wisata maupun dataset rating. Setelah dilakukan pengecekan, tidak ada data yang hilang/kosong pada kedua dataset tersbut.



## Data Preparation

Tahap ini bertujuan untuk mempersiapkan data yang akan digunakan untuk proses training model. Di sini dilakukan penghapusan kolom yang tidak diperlukan, pembersihkan data _missing value_, dan melakukan pengecekan dan penghapusan data duplikat.

1. **Penghapusan Kolom yang Tidak Diperlukan**

   Pada dataset tourism_with_id, data yang diperlukan hanya ada pada kolom `Place_Id`, `Place_Name`, dan `Category`, jadi hapus yang lain.

   Pada dataset tourism_rating, semua kolom diperlukan, jadi tidak ada kolom yang dihapus.





## Modeling


### Model Development dengan Content Based Filtering

Pada tahap ini, akan dikembangkan model untuk rekomendasi tempat wisata dengan memanfaatkan metode TF-IDF (Term Frequency-Inverse Document Frequency) dan Cosine Similarity. Pendekatan Content-Based Filtering ini akan berfokus pada karakteristik atau konten dari item yang direkomendasikan, dalam hal ini, teks deskripsi kategori wisata

TF-IDF akan digunakan untuk mengubah teks deskripsi kategori wisata menjadi representasi vektor numerik yang mencerminkan pentingnya setiap kata dalam teks tersebut. Sedangkan Cosine Similarity akan mengukur kesamaan antara vektor representasi TF-IDF dari teks kategori wisata. Dengan demikian, pendekatan Content-Based Filtering dengan TF-IDF dan Cosine Similarity memungkinkan kita untuk merekomendasikan tempat wisata yang serupa berdasarkan kemiripan konten atau karakteristik teks kategorinya.

Adapun tahap dalam pembuatan rekomendasi ini , diantaranya:

***Langkah 1:*** Menghitung TF-IDF

- Inisialisasi TfidfVectorizer untuk mengubah teks kategori wisata menjadi matriks TF-IDF.
- Lakukan fit pada TfidfVectorizer untuk menghitung TF-IDF dari data kategori wisata.
- Dapatkan matriks TF-IDF dan daftar nama fitur (kata-kata unik) dari kategori wisata.


***Langkah 2 :*** Menghitung Cosine Similarity

- Gunakan matriks TF-IDF yang telah dihitung sebelumnya.
- Hitung cosine similarity antara setiap pasang teks kategori wisata.
- Hasilnya akan berupa sebuah dataframe yang berisi nilai cosine similarity antara setiap pasang teks kategori wisata.


***Langkah 3 :*** Membuat Fungsi Rekomendasi

- Buat sebuah fungsi yang disebut rekomendasi_destinasi_wisata.
- Fungsi ini akan digunakan untuk merekomendasikan tempat wisata yang serupa berdasarkan nama tempat wisata yang diinputkan.
- Fungsi akan menerima beberapa parameter, yaitu:
  - input_tempat_wisata: Nama tempat wisata yang ingin direkomendasikan.
  - similarity_data: Dataframe yang berisi nilai cosine similarity dari langkah sebelumnya.
  - Items: Nama dan fitur yang digunakan untuk mendefinisikan kemiripan (misalnya 'Place_Name' dan 'Category').
  - k: Banyak rekomendasi yang ingin diberikan.

- Dalam fungsi, ambil baris dari dataframe similarity_data yang sesuai dengan input_tempat_wisata.
- Urutkan baris tersebut berdasarkan nilai similarity secara menurun.
- Hapus nilai similarity pada tempat wisata input agar tempat wisata itu sendiri tidak menjadi rekomendasi.
- Ambil k rekomendasi teratas berdasarkan urutan similarity yang sudah diurutkan.
- Hasil rekomendasi berupa daftar nama tempat wisata yang serupa.


***Langkah 4:*** Penggunaan Fungsi Rekomendasi

- Gunakan fungsi rekomendasi_destinasi_wisata untuk mendapatkan rekomendasi tempat wisata berdasarkan nama tempat wisata yang diinputkan.
- Masukkan nama tempat wisata yang ingin direkomendasikan ke parameter input_tempat_wisata.
- Tentukan jumlah rekomendasi yang ingin ditampilkan dengan mengisi nilai k.


***Langkah 5:*** Output

- Hasil dari fungsi rekomendasi akan berupa daftar nama tempat wisata yang direkomendasikan berdasarkan similarity dengan tempat wisata input.


### Model Development dengan Collaborative Filtering

Tahap-tahap yang dilakukan untuk membuat sistem rekomendasi dengan pendekatan collaborative filtering meliputi data preparation, pembagian data menjadi data latih dan data validasi, serta pembangunan model dan pengujian sistem rekomendasi. Berikut adalah rincian dari setiap tahap yang telah dijelaskan:
   
##### Data Preparation:

- Pada tahap data preparation, dilakukan proses encoding fitur User_Id pada dataset ratings dan fitur Place_Id pada dataset ratings menjadi sebuah array.
- Hasil encoding tersebut kemudian dipetakan (mapped) ke dalam dataset ratings untuk menghubungkan data pengguna dengan data tempat wisata.
- Dalam tahap ini, juga diperoleh informasi tentang jumlah pengguna (user) yang teridentifikasi, yaitu sebanyak 300 pengguna, dan jumlah tempat wisata (place) yang terdaftar, yaitu sebanyak 437 tempat wisata.
- Rentang nilai rating yang digunakan dalam dataset adalah dari 1 hingga 5.


##### Pembagian Data Latih dan Data Validasi:

- Untuk mempersiapkan proses pengujian, data ratings diacak sebelum dilakukan pembagian menjadi data latih (train data) dan data validasi (validation data).
- Pembagian data dilakukan dengan rasio 80:20, di mana 80% data digunakan sebagai data latih dan 20% data digunakan sebagai data validasi.

##### Pembuatan Model dan pelatihan

Adapun tahapan pembuatan model rekomendasi dengan pendekatan collaborative filtering,dapat dijelaskan sebagai berikut:

1. Inisialisasi Model:
   - Membuat kelas `MyRecommendationModel` yang akan digunakan sebagai model rekomendasi kustom dengan pendekatan collaborative filtering.
   - Kelas ini memiliki atribut untuk menyimpan jumlah pengguna, jumlah tempat wisata, dan ukuran embedding yang akan digunakan dalam model.
   - Empat layer embedding dibuat untuk merepresentasikan pengguna, bias pengguna, tempat wisata, dan bias tempat.

2. Metode `call`:
   - Metode `call` digunakan saat model dipanggil dengan input data.
   - Di dalam metode ini, embedding vektor untuk pengguna dan tempat wisata diambil berdasarkan ID yang diberikan sebagai input.
   - Vektor bias untuk pengguna dan tempat wisata juga diambil dari layer embedding yang telah diinisialisasi sebelumnya.
   - Perhitungan hasil perkalian dot (dot product) antara embedding vektor pengguna dan tempat wisata dilakukan untuk setiap pasangan pengguna dan tempat dalam batch input.
   - Hasil perkalian dot tersebut dijumlahkan dengan vektor bias pengguna dan bias tempat wisata untuk menghasilkan nilai probabilitas rekomendasi melalui fungsi aktivasi sigmoid.

3. Pengembangan Model dan Proses Pelatihan:
   - Model rekomendasi dikembangkan dengan ukuran embedding 50.
   - Model dikompilasi dengan konfigurasi loss menggunakan binary crossentropy, yang cocok untuk tugas klasifikasi biner seperti rekomendasi.
   - Sebagai optimizer, digunakan Adam dengan learning rate 0.0001 untuk mempercepat proses pembelajaran model.
   - Metrik evaluasi RMSE digunakan untuk mengukur sejauh mana perbedaan antara rating prediksi dan rating sebenarnya pada data validasi.
   - Early Stopping digunakan untuk menghentikan pelatihan jika tidak ada peningkatan yang signifikan dalam RMSE dalam jumlah epoch tertentu, menghindari overfitting dan menghemat waktu pelatihan.
   - Proses pelatihan dilakukan dengan data pelatihan dan validasi menggunakan batch size 8 dan jumlah epoch 100.

##### Hasil Rekomendasi:

- Hasil rekomendasi berisi 10 tempat wisata teratas yang direkomendasikan oleh model untuk pengguna acak.
- Selain itu, output dari rekomendasi ini juga menampilkan 5 tempat wisata dengan peringkat tertinggi dari pengguna acak berdasarkan data rating yang sudah diberikan sebagai perbandingan.




## Evaluation


#### Evaluasi Model Content Based Filtering
  
  Adapun matriks evaluasi yang akan digunakan untuk mengevaluasi model content based filtering dapat menggunakan matrik precision.

  Precision adalah metrik evaluasi yang mengukur sejauh mana rekomendasi yang diberikan oleh sistem relevan dan tepat. Dalam konteks sistem rekomendasi, Precision mengukur persentase item yang relevan dari seluruh item yang direkomendasikan kepada pengguna


  $$precision = \frac{TP}{TP + FP}$$

  Keterangan:

  -  $TP =$ _True Positive_; jumlah item rekomendasi yang sesuai
  - $FP =$ _False Positive_; jumlah item  rekomendasi yang tidak sesuai


  Adapun output model Content Based Filtering pada penelitan ini dapat dilihat dari Tabel 1 dan Tabel 1 dibawah ini :

  **Tabel 5. Nama Tempat yang Dipilih Pengguna**

  | Place_Id | Place_Name | Category |
  | -------- | ---------- | ----------- |
  | 1        | Monumen Nasional | Budaya |

  Berikut adalah hasil rekomendasi nama tempat berdasarkan kategori yang sama.

  **Tabel 6. Hasil Rekomendasi _Content-based Filtering_**

  | Place_Name                          | Category |
  | ----------------------------------- | -------- |
  | Candi Sewu                          | Budaya   |
  | Museum Benteng Vredeburg Yogyakarta | Budaya   |
  | Museum Satria Mandala               | Budaya   |
  | Kyotoku Floating Market             | Budaya   |
  | Bandros City Tour                   | Budaya   |


  Berdasarkan informasi diatas , bahwa:

  Karena semua item dalam Tabel 2 memiliki kategori yang sama dengan item yang dipilih oleh pengguna (Budaya), maka semua rekomendasi adalah True Positives.
  
  - TP = jumlah item rekomendasi yang sesuai = 5
  - TN= Jumlah item  rekomendasi yang tidak sesuai= 0

  Maka ,Presisinya dapat dihitung sebagai berikut:

  Presisi = TP / (TP+TN) = 5 / (5+0) = 1, Artinya, model memberikan rekomendasi yang relevan dengan preferensi pengguna untuk semua tempat yang direkomendasikan.


  
#### Evaluasi Model Collaborative Filtering


  RMSE (Root Mean Squared Error) adalah metrik evaluasi yang digunakan dalam sistem rekomendasi berbasis peringkat atau rating-based. Metrik ini mengukur seberapa akurat sistem dalam melakukan prediksi peringkat atau nilai yang diberikan oleh pengguna terhadap item yang direkomendasikan.

  Dalam sistem rekomendasi Collaborative Filtering, RMSE digunakan untuk membandingkan perbedaan antara nilai peringkat atau skor yang diprediksi oleh sistem dengan nilai sebenarnya dari pengguna untuk item-item yang direkomendasikan.

  Berikut adalah rumus RMSE untuk evaluasi sistem rekomendasi Collaborative Filtering:

  $$RMSE=\sqrt{\sum^{n}_{i=1} \frac{y_i - y\\_pred_i}{n}}$$

   Keterangan:
   - $n =$ jumlah _dataset_
   - $i =$ urutan data dalam _dataset_
   - $y_i =$ nilai yang sebenarnya
   - $y_{pred} =$ nilai prediksi terhadap $i$



   Kurva RMSE dapat dilihat pada gambar dibawah ini.

   ![RMSE](https://raw.githubusercontent.com/daniahmad92/rekom-wisata/main/Evaluasi_model_2b.png)


   Nilai RMSE dari sistem rekomendasi dengan pendekatan _collaborative filtering_ adalah 0.3344 pada _Training RMSE_, dan 0.3413 pada _Validation RMSE_.Nilai ini relatif kecil menunjukkan bahwa performa model cukup baik
