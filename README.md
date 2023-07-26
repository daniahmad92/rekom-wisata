# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Pada bagian ini, Kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.


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


Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.


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
