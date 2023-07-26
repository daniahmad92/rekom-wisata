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


Dalam sistem rekomendasi wisata menggunakan Content-based Filtering, model akan merekomendasikan destinasi wisata berdasarkan kesamaan konten atau fitur antara destinasi wisata yang telah dikunjungi atau disukai oleh pengguna sebelumnya. Sedangkan dalam Collaborative Filtering, model akan merekomendasikan destinasi wisata berdasarkan pola preferensi dari pengguna yang memiliki kesamaan dengan pengguna lain.

### Model Development dengan Content Based Filtering

##### TF-IDF Vectorizer

1. Inisialisasi TfidfVectorizer
2. Melakukan perhitungan idf pada data kategori wisata
3. Mengambil daftar nama fitur (kata-kata unik) dari kategori wisata dengan menggunakan metode get_feature_names_out()
4. Melakukan fit lalu ditransformasikan ke bentuk matrix untuk mengubah teks kategori wisata menjadi matriks TF-IDF
5. Mengubah vektor TF-IDF dalam bentuk matriks dengan fungsi todense()
6. Membuat dataframe untuk melihat TF-IDF matrix. Kolom diisi dengan "Kategori wisata" dan baris diisi dengan naama tempat wisata tersebut

Output yang dihasilkan pada tahap ini yaitu berupa dataframe yang menunjukkan korelasi antara nama tempat wisata dengan kategori wisata tersebut

##### Cosine Similarity

1. Menghitung cosine similarity pada matrix tf-idf
2. Membuat dataframe dari variabel cosine_similarity dengan baris dan kolom berupa nama tempat wisatg

ouput yang dihasilkan pada tahap ini yaitu berupa dataframe yang berisi data similarity (kesamaan) antar kategori wisata

##### Membuat fungsi Rekomendasi

Fungsi ini untuk merekomendasikan tempat wisata yang serupa berdasarkan nama tempat wisatanya

Pada tahap ini,peneliti membuat fungsi rekomendasi_destinasi_wisata dengan beberapa parameter sebagai berikut:
- input_tempat_wisata :  Nama tempat wisata
- similarity_data     :  Dataframe mengenai similarity yang didefinisikan sebelumnya
- Items  : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'Place_Name' dan 'Category'
- k : Banyak rekomendasi yang ingin diberikan

Adapun output pada fungsi ini yaitu dihasilkan 5 rekomendasi tempat wiasata

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



## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
