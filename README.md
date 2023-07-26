# Laporan Proyek Machine Learning:Sistem Rekomendasi Destinasi Wisata Indonesia- Dadan AHmad Dani

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



Dataset yang digunakan dalam proyek ini adalah dataset [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination) yang diambil dari Kaggle dengan `tourism_with_id.csv` dan `tourism_rating.csv` sebagai dataset yang digunakan.

  
  **Tabel 2. Variabel Dataset tourism_with_id**

  | #   | Variabel     | Deskripsi                                            | Tipe Data   |
  | --- | ------------ | -----------------------------------------------------| ----------- |
  | 0   | Place_Id     | Id unik untuk setiap lokasi wisata                   | int64       |
  | 1   | Place_Name   | Nama dari lokasi wisata                              | object      |
  | 2   | Description  | Deskripsi singkat tentang lokasi wisata              | object      |
  | 3   | Category     | Kategori atau jenis dari lokasi wisata               | object      |
  | 4   | City         | Nama kota atau daerah tempat lokasi wisata berada    | object      |
  | 5   | Price        | Harga tiket masuk ke lokasi wisata.                  | int64       |
  | 6   | Rating       | Rating lokasi wisata tersebut                        | float64     |
  | 7   | Time_Minutes | Perkiraan waktu tempuh untuk mencapai lokasi wisata  | float64     |
  | 8   | Coordinate   | Koordinat geografis lokasi wisata.                   | object      |
  | 9   | Lat          | Latitude (garis lintang) lokasi wisata               | float64     |
  | 10  | Long         | Longitude (garis bujur) lokasi wisata.               | float64     |



  **Tabel 2. Variabel Dataset tourism_with_id**

  | #   | Variabel      | Deskripsi                                                             | Dtype |
  | --- | ------------- | --------------------------------------------------------------------  | ----- |
  | 0   | User_Id       | Id unik wisatan                                                       | int64 |
  | 1   | Place_Id      | Id unik untuk setiap lokasi wisata                                    | int64 |
  | 2   | Place_Ratings | Rating yang diberikan oleh wisatawan terhadap tempat wisata tersebut  | int64 |

## Data Preparation

Tahap ini bertujuan untuk mempersiapkan data yang akan digunakan untuk proses training model. Di sini dilakukan penghapusan kolom yang tidak diperlukan, pembersihkan data _missing value_, dan melakukan pengecekan dan penghapusan data duplikat.

1. **Penghapusan Kolom yang Tidak Diperlukan**

   Pada dataset tourism_with_id, data yang diperlukan hanya ada pada kolom `Place_Id`, `Place_Name`, dan `Category`, jadi hapus yang lain.

   Pada dataset tourism_rating, semua kolom diperlukan, jadi tidak ada kolom yang dihapus.

2. **Pengecekan Missing Values**

   Proses pengecekan data yang hilang atau _missing value_ dilakukan pada masing-masing dataset tourism_with_id dan tourism_rating. Berdasarkan hasil pengecekan, ternyata tidak ada data yang hilang dari kedua dataset tersebut.



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

Dengan langkah-langkah di atas, rekomendasi tempat wisata yang serupa dapat diberikan berdasarkan nama tempat wisata yang diinputkan, menggunakan pendekatan TF-IDF dan Cosine Similarity.


##### Hasil _Top-N Recommendation_

  Setelah data tempat wisata dikonversi menjadi matriks dengan menggunakan TF-IDF Vectorizer, dan tingkat kesamaan antar nama tempat ditentukan dengan menggunakan cosine similarity, selanjutnya dilakukan pengujian terhadap sistem rekomendasi yang menggunakan pendekatan content-based filtering recommendation. Hasil pengujian tersebut dapat dilihat sebagai berikut:

  Diambil sebuah nama tempat yang dipilih oleh pengguna.

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

  Berdasarkan hasil rekomendasi di atas, dapat dilihat bahwa sistem yang dibuat berhasil memberikan rekomendasi tempat berdasarkan sebuah tempat, yaitu 'Monumen Nasional' dan dihasilkan rekomendasi tempat dengan kategori yang sama, yaitu budaya.

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

##### Pengembangan Model dan Pengujian

- Dalam tahap pengembangan model, model machine learning dibangun menggunakan kelas MyRecommendationModel yang merupakan model rekomendasi kustom dengan pendekatan collaborative filtering.
- Model ini menggunakan layer embedding untuk merepresentasikan pengguna (users) dan tempat wisata (places) dalam ruang berdimensi rendah.
- Proses pelatihan model menggunakan optimizer Adam dan binary crossentropy loss function untuk menghitung loss dan meminimalkan kesalahan prediksi.
- Evaluasi kinerja sistem rekomendasi dilakukan dengan menggunakan metrik RMSE (Root Mean Squared Error) berdasarkan data validasi.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
