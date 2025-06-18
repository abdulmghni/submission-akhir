## Laporan Proyek Machine Learning - Abdul Mughni

## Domain Proyek
Industri perbukuan merupakan salah satu sektor penting dalam dunia literasi dan pendidikan. Dengan jutaan judul buku yang tersedia dari berbagai genre dan penulis, pembaca seringkali kesulitan menemukan buku yang sesuai dengan minat dan preferensi mereka. Proyek ini bertujuan untuk membangun sistem rekomendasi buku berbasis data menggunakan pendekatan Content-Based Filtering (CBF).

Masalah ini penting untuk diselesaikan agar dapat membantu pembaca dalam menemukan buku yang sesuai dan meningkatkan pengalaman membaca mereka. Di sisi lain, sistem ini juga dapat membantu penerbit, penulis, dan toko buku untuk memahami tren preferensi pembaca. Dalam era informasi yang melimpah, pembaca seringkali menghadapi overload informasi, sehingga sistem rekomendasi cerdas diperlukan untuk menyaring dan memperkenalkan buku-buku baru atau penulis yang kurang dikenal yang memiliki potensi menarik bagi segmen pembaca tertentu.

## 🎓 Proyek Sistem Rekomendasi Buku - Dicoding
Project Overview
Industri penerbitan dan literasi terus berkembang, dengan semakin banyaknya judul buku yang tersedia bagi pembaca. Dalam era digital, pembaca semakin mengandalkan sistem rekomendasi untuk menemukan buku baru yang sesuai dengan minat dan preferensi mereka.

Proyek ini bertujuan membangun sistem rekomendasi buku berbasis machine learning yang mampu memprediksi rating dan memberikan saran buku yang relevan.

## 📚 Referensi
G. Adomavicius, A. Tuzhilin, “Toward the Next Generation of Recommender Systems: A Survey,” IEEE TKDE, 2005.
D. Jannach, et al., “Recommender Systems: Challenges, Insights, and Research Opportunities,” ACM TiiS, 2021.

## 📌 Business Understanding
### 🔍 Problem Statements
Bagaimana membantu pengguna menemukan buku baru yang mungkin mereka sukai, meskipun mereka belum pernah memberikan rating atau interaksi sebelumnya?

### 🌟 Goals
Membangun sistem prediksi rating berdasarkan fitur buku (Content-Based Filtering/CBF) dan interaksi pengguna (Collaborative Filtering/CF).
Menyajikan rekomendasi top-N berdasarkan prediksi terbaik.

---

## 📊 Data Understanding & Exploratory Data Analysis

### Dataset yang digunakan bersumber dari Kaggle: [Book Recommendation Dataset] https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?select=Books.csv

### 1. Informasi Umum Dataset

![image](https://github.com/user-attachments/assets/d8682654-32e1-4685-8c49-05b7000e63e5)

## A. Books Dataset

### Jumlah Data:
- Jumlah Baris: 271.360
- Jumlah Kolom: 8
  
### Penjelasan Fitur:
- ISBN: (String) International Standard Book Number, ID unik untuk setiap buku. Digunakan sebagai pengidentifikasi buku dan kunci untuk penggabungan data.
- Book-Title: (String) Judul buku. Digunakan sebagai fitur konten utama dalam model CBF.
- Book-Author: (String) Nama penulis buku. Digunakan sebagai fitur konten utama dalam model CBF.
- Year-Of-Publication: (Integer) Tahun buku diterbitkan. Digunakan untuk analisis deskriptif, namun tidak secara langsung dalam fitur konten CBF tekstual.
- Publisher: (String) Nama penerbit buku. Digunakan sebagai fitur konten utama dalam model CBF.
- Image-URL-S, Image-URL-M, Image-URL-L: (String) URL gambar sampul buku dalam ukuran kecil, sedang, dan besar. Tidak digunakan dalam pemodelan CBF karena merupakan fitur non-tekstual/konten desk

## B. Ratings Dataset

### Jumlah Data:
- Jumlah Baris: 271.360
- Jumlah Kolom: 3

### Penjelasan Fitur:
- User-ID: (Integer) ID pengguna yang memberikan rating. Digunakan untuk mengidentifikasi pengguna yang berinteraksi.
- ISBN: (String) ISBN buku yang diberi rating. Digunakan sebagai pengidentifikasi buku yang menerima rating.
- Book-Rating: (Integer) Nilai rating yang diberikan oleh pengguna untuk buku tersebut (biasanya skala 0-10). Digunakan sebagai informasi kunci tentang preferensi pengguna, meskipun model CBF ini tidak secara - langsung memprediksi rating numerik, informasi ini penting untuk pemahaman data interaksi.

## C. Users Dataset

### Jumlah Data:
- Jumlah Baris: 278.858
- Jumlah Kolom: 3

### Penjelasan Fitur:
- User-ID: (Integer) ID unik untuk setiap pengguna. Digunakan sebagai pengidentifikasi pengguna.
- Location: (String) Lokasi geografis (kota, negara) tempat tinggal pengguna. Digunakan untuk konteks demografi pengguna, namun tidak secara langsung dalam model CBF.
- Age: (Float/Integer) Usia pengguna. Digunakan untuk analisis demografi; missing values mungkin perlu ditangani (misalnya, diisi dengan median atau dihapus, tergantung strategi Anda).


### 2. Pengecekan Missing Values
Pada tahap ini, dilakukan pengecekan untuk melihat apakah ada nilai yang hilang (missing values) di dalam setiap dataset. Missing values dapat mempengaruhi kualitas model, oleh karena itu perlu dilakukan penanganan lebih lanjut

![image](https://github.com/user-attachments/assets/df5fbb55-c0e9-476e-8ce8-05cc2e6c39c0)


### 3. Menangani Duplikat Data
Di bawah ini adalah pemeriksaan jumlah data duplikat untuk masing-masing dataset. Duplikat dapat mempengaruhi kualitas analisis dan model, sehingga penting untuk mengidentifikasinya dan mengambil tindakan yang sesuai.

![image](https://github.com/user-attachments/assets/dcba8b4e-029b-49f2-aa52-e009a10fb763)



### 4. Visualisasi Distribusi Fitur Numerik
Bagian ini bertujuan untuk memvisualisasikan distribusi fitur numerik yang terdapat pada setiap dataset untuk membantu memahami data lebih baik.

![image](https://github.com/user-attachments/assets/276257ec-475a-42ee-a5ed-815e184c4860)

![image](https://github.com/user-attachments/assets/66bef0a9-c392-4388-adf8-cd79628b425d)


### 5. Visualisasi Pairplot untuk Fitur Numerik
Bagian ini berfungsi untuk memvisualisasikan hubungan antar fitur numerik menggunakan pairplot. Pairplot memungkinkan kita untuk melihat distribusi dari setiap fitur dan korelasi antar fitur dalam dataset.

![image](https://github.com/user-attachments/assets/83b40ac3-e73c-4024-b17f-e0ec9da949fa)


### 6. Visualisasi Heatmap Korelasi
Bagian ini bertujuan untuk menampilkan heatmap korelasi antar fitur numerik dalam setiap dataset. Heatmap korelasi memungkinkan kita untuk dengan cepat mengidentifikasi hubungan antar variabel, dengan warna yang menunjukkan tingkat korelasi antara fitur-fitur tersebut.

![image](https://github.com/user-attachments/assets/7d25f35a-d03c-470a-a660-5bb3e8eeb114)

![image](https://github.com/user-attachments/assets/946136ca-d216-4648-b5a3-0ab92fdd4f9a)


### 7. Visualisasi Distribusi Kategorikal
Bagian ini digunakan untuk menampilkan distribusi fitur kategorikal pada setiap dataset. Visualisasi yang digunakan berupa countplot dan barplot, untuk memberikan gambaran mengenai seberapa banyak setiap kategori muncul dalam dataset.

![image](https://github.com/user-attachments/assets/1a7f8463-8c43-447c-b95d-6f1c39f8e6ba)

![image](https://github.com/user-attachments/assets/0d250b51-e049-4c7c-b7c0-ec1b8c498822)

![image](https://github.com/user-attachments/assets/e1e6fa57-a651-4b52-8470-4cd6150bb241)

![image](https://github.com/user-attachments/assets/41cd33ec-6ec9-4dbe-bd4f-858f7999f801)

![image](https://github.com/user-attachments/assets/b0558b7f-6d6b-4f47-8683-df435253d6e3)

![image](https://github.com/user-attachments/assets/e8dac496-773a-4846-bb16-44dfaaae478c)

![image](https://github.com/user-attachments/assets/7adca16a-959f-4482-bbfd-9e66fffbe419)

### Penjelasan:
- categorical_dfs: List yang berisi DataFrame yang hanya mencakup kolom bertipe kategorikal (tipe object) dari setiap dataset.
- titles: Daftar judul untuk setiap plot berdasarkan dataset yang bersangkutan.
- Distribusi Kategorikal: Jika kolom kategorikal memiliki kurang dari 30 kategori, kita menggunakan countplot untuk menampilkan distribusi kategori tersebut. Jika lebih dari 30 kategori, kita hanya menampilkan top 15 kategori teratas menggunakan barplot.

####  Interpretasi:
- Countplot: Digunakan untuk visualisasi frekuensi setiap kategori. Jika kolom memiliki sedikit kategori, countplot sangat cocok untuk menampilkan distribusinya.
- Barplot: Digunakan jika jumlah kategori lebih banyak. Menampilkan 15 kategori teratas berdasarkan frekuensi kemunculan.

#### Manfaat:
- Membantu memahami distribusi data kategorikal dan memeriksa ketidakseimbangan kelas pada kolom kategorikal.
- Memberikan wawasan untuk memperbaiki data seperti kategori yang jarang muncul (outlier kategorikal), atau memilih fitur kategorikal mana yang penting untuk model.


### 8. Statistik Deskriptif Fitur Kategorikal
Bagian ini akan menampilkan statistik deskriptif untuk kolom-kolom bertipe kategorikal (tipe data object) di setiap dataset. Statistik deskriptif ini memberikan informasi tentang distribusi nilai dalam kolom kategorikal.

![image](https://github.com/user-attachments/assets/3cb2119f-ea86-476e-8f28-6b52b0efff7d)

#### Penjelasan:

1. df.describe(include='object'):
- Fungsi ini memberikan statistik deskriptif untuk kolom bertipe object (biasanya untuk kolom kategorikal). Statistik yang dihasilkan antara lain:
  - count: jumlah data yang tidak kosong.
  - unique: jumlah nilai unik dalam kolom.
  - top: nilai yang paling sering muncul.
  - freq: frekuensi kemunculan nilai yang paling sering.
2. Penggunaan Looping for df, title in zip(categorical_dfs, titles):
- Melalui looping ini, kode akan menjalankan statistik deskriptif untuk setiap DataFrame yang berisi kolom-kolom kategorikal.

#### Interpretasi Hasil:
- count: Memberikan informasi seberapa banyak data dalam kolom tersebut, menghindari adanya nilai yang hilang (NaN).
- unique: Memberikan jumlah kategori yang berbeda dalam kolom tersebut, memberi gambaran tentang keragaman data kategorikal.
- top: Menunjukkan kategori yang paling sering muncul, memberikan insight tentang kategori dominan dalam dataset.
- freq: Memberikan frekuensi kemunculan kategori yang paling sering.

#### Manfaat:
- Mengetahui distribusi nilai dalam kolom kategorikal membantu kita memahami variasi dan konsentrasi data.
- Membantu dalam mendeteksi data yang memiliki kategori dominan yang mungkin mempengaruhi model rekomendasi.
- Dapat menunjukkan apakah data tersebut memiliki banyak kategori yang unik atau apakah ada kategori yang sangat jarang, yang penting untuk desain model rekomendasi.


### 9. Distribusi Data Berdasarkan Lokasi, dan Age
Bagian ini menampilkan informasi terkait lokasi pengguna, dan Age

![image](https://github.com/user-attachments/assets/c05dc6b6-1a76-4553-8ed2-f4a909c7f347)

#### Penjelasan:
1. Lokasi Pengguna (df_user['Location']):
- Menampilkan 10 lokasi teratas berdasarkan jumlah pengguna yang terdaftar di lokasi tersebut.
- Ini menunjukkan di mana konsentrasi pengguna paling banyak berada

2. Usia Pengguna (df_users['Age']):
- Menampilkan 10 nilai usia teratas berdasarkan jumlah pengguna.
- Membantu untuk melihat rentang usia di mana pengguna paling banyak berasal.

#### Interpretasi:
- Lokasi Pengguna: Melihat lokasi dengan jumlah pengguna terbanyak, seperti London, Toronto, dan Sydney, memberikan gambaran tentang konsentrasi geografis pengguna dalam dataset. Ini bisa membantu dalam merancang strategi pemasaran atau rekomendasi yang lebih relevan dengan preferensi geografis tertentu.
- Usia Pengguna: Mengetahui usia pengguna terbanyak (misalnya 24, 25, 26 tahun) memberi wawasan tentang demografi dominan dari pengguna. Informasi ini sangat berguna untuk mempersonalisasi rekomendasi buku agar lebih relevan dengan minat dan preferensi kelompok usia tersebut.

#### Manfaat:
- Memberikan informasi tentang distribusi geografis dan demografis (usia) pengguna dalam dataset.
- Wawasan ini sangat penting untuk membangun sistem rekomendasi yang lebih cerdas dan relevan, baik berdasarkan lokasi pengguna maupun kelompok usia mereka.
- Membantu mengidentifikasi potensi ketidakseimbangan data, misalnya, jika ada lokasi atau kelompok usia yang sangat dominan, yang dapat memengaruhi cara sistem rekomendasi bekerja dan perlu dipertimbangkan dalam strategi penanganan data.





## 10. Visualisasi Analisis Distribusi Penulis Buku

Dengan menampilkan 20 penulis teratas berdasarkan jumlah buku yang mereka miliki, kita dapat melihat dominasi penulis tertentu. Grafik batang ini memberikan gambaran mengenai penulis-penulis populer atau yang paling banyak terwakili dalam koleksi buku yang ada.

Informasi ini sangat penting dalam membangun sistem rekomendasi. Misalnya, jika ingin mengembangkan model rekomendasi berbasis penulis, data ini dapat memberikan wawasan tentang penulis mana yang memiliki basis data yang kuat untuk analisis. Selain itu, ini juga dapat membantu dalam mengidentifikasi penulis yang kurang terwakili jika ada kebutuhan untuk memperluas cakupan rekomendasi.

![image](https://github.com/user-attachments/assets/e704a291-c906-4437-98fe-8223f6570fc6)

Dari grafik batang "Distribusi Penulis Buku Teratas" di atas, dapat disimpulkan bahwa Agatha Christie merupakan penulis buku yang paling dominan dalam dataset, diikuti oleh William Shakespeare dan Stephen King. Sementara itu, penulis seperti Piers Anthony, Janet Dailey, dan Franklin W. Dixon memiliki jumlah buku yang lebih sedikit dalam dataset ini.

Dominasi penulis tertentu dapat mempengaruhi proses sistem rekomendasi berbasis konten. Misalnya, jika pengguna memiliki preferensi terhadap penulis yang jarang muncul, sistem perlu memiliki strategi untuk tetap memberikan rekomendasi yang relevan meskipun datanya terbatas untuk penulis tersebut.

Selain itu, distribusi yang tidak seimbang ini juga menunjukkan pentingnya mempertimbangkan representasi penulis dalam dataset agar sistem rekomendasi tidak bias terhadap penulis mayoritas. Hal ini krusial untuk memastikan sistem dapat memberikan rekomendasi yang bervariasi dan adil kepada pengguna.


## 11. Analisis Part-of-Speech (POS) pada Judul Buku
Untuk mendalami lebih jauh karakteristik dari judul buku, dilakukan analisis Part-of-Speech (POS) menggunakan pustaka TextBlob. POS Tagging bertujuan untuk mengidentifikasi jenis kata seperti kata benda (noun), kata sifat (adjective), kata kerja (verb), dan lainnya dari kumpulan judul buku.

Dengan menggabungkan semua judul buku menjadi satu teks, kita dapat menganalisis frekuensi masing-masing jenis kata yang muncul. Visualisasi ini akan memberikan gambaran mengenai struktur umum penamaan judul buku, misalnya apakah lebih banyak menggunakan kata benda atau kata sifat.

Informasi POS ini juga bisa memberikan insight tambahan jika ingin mengembangkan model rekomendasi yang mempertimbangkan karakter linguistik dari judul buku.

![image](https://github.com/user-attachments/assets/8ae07290-bed1-43de-839c-3fd5f823a318)



### 12. Visualisasi Bigram Menggunakan TF-IDF pada Judul Buku
Pada bagian ini, dilakukan analisis terhadap bigram, yaitu kombinasi dua kata yang muncul secara berurutan dalam judul buku. Untuk menghitung bobot kemunculan bigram, digunakan pendekatan TF-IDF (Term Frequency-Inverse Document Frequency) yang tidak hanya mempertimbangkan frekuensi kata, tetapi juga signifikansi relatifnya di seluruh kumpulan judul buku.

Tujuan dari analisis ini adalah untuk mengidentifikasi pasangan kata yang paling sering dan paling penting dalam judul-judul buku. Hal ini dapat memberikan insight tentang pola penamaan buku atau genre yang dominan, misalnya apakah sering muncul frasa seperti "harlequin presents", "harlequin romance", atau "special edition".

Visualisasi ini membantu kita memahami struktur frasa yang dominan dalam judul buku, yang dapat digunakan dalam pengembangan model Content-Based Filtering untuk meningkatkan akurasi rekomendasi berdasarkan kemiripan judul atau genre yang tersirat dari bigram tersebut.

![image](https://github.com/user-attachments/assets/9afeeba7-ae9d-4c1e-a30f-13316a62e6d9)


### 13. Visualisasi Trigram Menggunakan TF-IDF pada Judul Buku
Setelah analisis bigram, dilakukan pula analisis terhadap trigram, yaitu kombinasi tiga kata yang muncul berurutan dalam judul buku. Seperti sebelumnya, metode TF-IDF digunakan untuk mengukur pentingnya trigram yang muncul, bukan hanya berdasarkan frekuensinya tetapi juga berdasarkan tingkat kekhususan trigram di seluruh data.

Trigram dapat memberikan informasi yang lebih kontekstual dibandingkan unigram (satu kata) atau bigram, karena tiga kata berturut-turut cenderung membentuk frasa yang lebih bermakna atau spesifik. Misalnya, frasa seperti "silhouette special edition" atau "harlequin american romance" bisa muncul sebagai trigram yang signifikan.

Visualisasi ini membantu mengidentifikasi pola atau struktur umum dalam penamaan judul buku yang bisa dimanfaatkan lebih lanjut untuk proses ekstraksi fitur dalam sistem rekomendasi berbasis konten. Ini memberikan wawasan yang lebih mendalam tentang genre, seri, atau tema yang dominan dalam dataset buku.

![image](https://github.com/user-attachments/assets/b0f04508-3358-46e4-b6e6-6f661b31ac6d)


## 🪝 Data Preparation


### 1. Pembersihan Kolom Tidak Relevan
Menghapus kolom tidak relevan:
Dari dataset buku (df_books): Image-URL-S, Image-URL-M, Image-URL-L)

![image](https://github.com/user-attachments/assets/5a2da435-1646-4786-8710-2b4cf2488818)


### 2. Penanganan Missing Values
Berdasarkan hasil eksplorasi awal, ditemukan sejumlah nilai kosong pada beberapa kolom penting di dataset df_books. Untuk memastikan kualitas data:

Pada kolom seperti Book-Author dan Publisher, nilai kosong diisi dengan string kosong ("") agar proses ekstraksi teks tidak terganggu.

Untuk dataset df_users dan df_ratings, nilai kosong yang ditemukan pada kolom kritikal dihapus menggunakan dropna() karena tidak dapat diimputasi secara logis tanpa risiko bias.

![image](https://github.com/user-attachments/assets/f99b9c89-d943-4bb9-baec-0508fe9f8add)


### 3. Penghapusan data duplikat
Dilakukan penghapusan data yang bersifat duplikat pada seluruh dataframe yang digunakan, yaitu: df_users, df_ratings, dan df_books

Langkah ini memastikan bahwa setiap entri dalam dataset bersifat unik dan valid sebelum dilakukan proses lebih lanjut seperti penanganan nilai yang hilang atau pengkodean data. Setelah penghapusan, dilakukan pengecekan ulang 

![image](https://github.com/user-attachments/assets/cd9029b3-6ce1-478b-b1a6-ae1714bc7407)


### 4. Deteksi Outlier Menggunakan Boxpl
Untuk mengidentifikasi adanya outlier dalam data numerik, dilakukan visualisasi boxplot pada masing-masing dataframe: df_ratings, df_books, dan df_user.

![image](https://github.com/user-attachments/assets/8abece25-65e2-4bc1-b284-4b1489d5775a)


### 5. Menghapus Outlier Menggunakan Metode IQR
Pada bagian ini, Dari hasil visualisasi dan analisis statistik, ditemukan nilai-nilai ekstrem (outlier) terutama pada kolom numerik seperti:

Age pada df_users

Book-Rating pada df_ratings

Pembersihan dilakukan menggunakan metode Interquartile Range (IQR) untuk memastikan distribusi data menjadi lebih normal dan tidak terpengaruh oleh nilai-nilai ekstrem yang dapat menurunkan performa model.

![image](https://github.com/user-attachments/assets/2a71b6a3-cdba-4b67-86da-e81155f85e3f)


### 6. Visualisasi Boxplot setelah Penghapusan Outlier
Pada tahap ini, dilakukan visualisasi menggunakan boxplot untuk masing-masing dataset (Users, Ratings, dan books). Boxplot digunakan untuk:
- Melihat distribusi data numerik
- Mengidentifikasi outlier secara visual
- Memahami sebaran dan variasi data

Setiap grafik menampilkan kolom-kolom numerik dari masing-masing DataFrame. Proses ini membantu dalam validasi apakah metode penghapusan outlier sebelumnya telah bekerja secara efektif.

![image](https://github.com/user-attachments/assets/bce3055f-bf00-42c7-9f30-137d87e645d1)


### 7. Penggabungan Fitur Konten
Setelah data dibersihkan, langkah selanjutnya adalah membentuk fitur gabungan yang akan digunakan sebagai input untuk sistem rekomendasi berbasis konten.
Tujuan: Menggabungkan informasi deskriptif tentang buku (judul, penulis, dan penerbit) ke dalam satu fitur teks, agar dapat diolah sebagai dokumen dalam ekstraksi fitur teks.

Langkah-langkah:
- Dataset df_books telah difilter untuk hanya menyertakan kolom penting:
ISBN, Book-Title, Book-Author, dan Publisher.
- Nilai kosong (missing values) pada kolom-kolom tersebut sebelumnya telah diganti dengan string kosong ("") agar proses penggabungan tidak gagal.
- Penggabungan dilakukan menggunakan + operator dengan spasi sebagai pemisah:
  
![image](https://github.com/user-attachments/assets/2f86de77-ef45-4636-b164-2ad65a0a9511)

Contoh hasil penggabungan:

![image](https://github.com/user-attachments/assets/a4a53dcb-4d67-4589-b030-92ef87f8bfb9)

Fitur metadata ini akan menjadi dasar untuk menghitung kemiripan antar buku menggunakan metode pemrosesan teks (TF-IDF).


### 8. Ekstraksi Fitur dengan TF-IDF
Setelah kolom metadata terbentuk, dilakukan konversi dari teks ke bentuk numerik yang bisa dianalisis oleh mesin.
Tujuan: Mengubah teks gabungan dari metadata menjadi representasi vektor numerik berdasarkan frekuensi kata yang bersifat unik pada setiap dokumen (buku).

Langkah-langkah teknis:
- Menggunakan TfidfVectorizer dari sklearn.feature_extraction.text.
- Parameter yang digunakan:
  
![image](https://github.com/user-attachments/assets/a31e11b2-06b6-4869-90bd-a0df3902bbb5)

- Stop words bahasa Inggris dihapus secara otomatis untuk menghindari gangguan dari kata-kata umum seperti “the”, “and”, “of”.

- Output tfidf_matrix berbentuk matriks sparse (jumlah baris = jumlah buku, jumlah kolom = jumlah kata unik) yang menyimpan bobot penting dari setiap kata di setiap buku.

Kegunaan:
- Matriks ini menjadi dasar untuk menghitung kemiripan antar buku menggunakan cosine similarity, yang akan digunakan dalam sistem rekomendasi berbasis konten.


### 9. Mapping Judul Buku ke Indeks
Agar sistem dapat mengambil indeks dari buku berdasarkan judul yang diberikan pengguna, dibuat pemetaan judul → indeks.

![image](https://github.com/user-attachments/assets/3ceb62d3-3021-4613-93b8-57e8d57fd523)

Kegunaan:

- Memungkinkan pencarian cepat indeks berdasarkan input judul buku dari pengguna.

- Indeks tersebut kemudian digunakan untuk mengambil baris dari tfidf_matrix dan menghitung kemiripan antar buku menggunakan cosine similarity.


---

### 🤖 Modeling & Results
Content-Based Filtering (CBF):
Pada tahap Modeling, dilakukan pembangunan sistem rekomendasi yang bertujuan untuk memberikan saran buku kepada pengguna berdasarkan preferensi dan pola interaksi yang tersedia dalam data. Sistem rekomendasi ini memainkan peran penting dalam membantu pengguna menemukan buku yang relevan, menarik, dan sesuai dengan minat mereka, terutama ketika jumlah pilihan sangat banyak.

## Content-Based Filtering (CBF)


### 1. Perhitungan Cosine Similarity
Cosine Similarity digunakan untuk mengukur tingkat kemiripan antar buku berdasarkan representasi vektor dari TF-IDF. Representasi vektor ini berasal dari fitur metadata yang telah kita buat sebelumnya (gabungan Book-Title, Book-Author, Publisher).

Nilai kemiripan ini disusun dalam bentuk matriks, sehingga kita dapat melihat seberapa mirip satu buku dengan buku lainnya.

Hasilnya disimpan dalam model_knn, yang akan menjadi dasar untuk sistem rekomendasi buku berbasis konten. Semakin tinggi nilai cosine similarity antara dua buku, semakin mirip konten kedua buku tersebut.

![image](https://github.com/user-attachments/assets/32b5598e-2f29-4396-ab58-012b92bc80de)


### 2. Fungsi Rekomendasi Buku
Fungsi get_recommendations digunakan untuk memberikan rekomendasi buku yang mirip dengan judul buku yang diberikan sebagai input. Prosesnya meliputi:

- Pengecekan Ketersediaan: Memeriksa apakah judul buku yang dimasukkan (input) ada dalam data. Jika tidak ada, fungsi akan memberikan pesan bahwa buku tidak ditemukan.
- Pengambilan Indeks: Mengambil indeks dari buku yang menjadi input menggunakan mapping indices yang sudah dibuat sebelumnya.
- Perhitungan Skor Kesamaan: Mengambil skor kesamaan (cosine similarity) dari matriks similarity_df antara buku input dengan semua buku lainnya.
- Pengurutan dan Pemilihan: Mengurutkan skor kesamaan tersebut dari yang tertinggi dan mengambil 10 buku teratas yang paling mirip (selain buku itu sendiri).
- Pengembalian Rekomendasi: Mengembalikan data buku yang direkomendasikan dalam bentuk DataFrame, termasuk judul, penulis, dan penerbit buku-buku tersebut.

![image](https://github.com/user-attachments/assets/c12cbeca-75ae-4527-9b25-837b2811a026)


### 3. Contoh Penggunaan Fungsi Rekomendasi
Contoh berikut menunjukkan cara memanggil fungsi get_recommendations dengan memasukkan judul buku, misalnya "Harry Potter and the Chamber of Secrets". Fungsi akan menampilkan daftar buku lain yang memiliki kemiripan konten berdasarkan judul, penulis, dan penerbit, menggunakan metode Content-Based Filtering (CBF).

Ini akan memberikan gambaran bagaimana sistem merekomendasikan buku-buku yang serupa kepada pengguna berdasarkan karakteristik buku yang mereka minati.

![image](https://github.com/user-attachments/assets/2766a6a4-c752-46a8-ab65-8050599204fd)


##  Evaluasi Sistem Rekomendasi
Evaluasi sistem rekomendasi bertujuan untuk mengukur seberapa baik model dalam menyarankan buku yang relevan dan sesuai preferensi pengguna. Dalam proyek ini, dilakukan  pendekatan utama dalam pembuatan sistem rekomendasi, yaitu:
Content-Based Filtering (CBF)
 
Metode Evaluasi: Precision@K (dengan K = 10)

Content-Based Filtering menggunakan fitur konten buku (seperti judul, penulis, dan penerbit) untuk menghitung kemiripan antar buku, lalu merekomendasikan buku-buku yang paling mirip.

Untuk mengevaluasi performa CBF, digunakan metrik Precision@10. Metrik ini mengukur rasio jumlah buku yang relevan (misalnya, memiliki penulis atau genre yang sama, atau sesuai dengan preferensi pengguna yang disiratkan dari buku awal) terhadap jumlah total rekomendasi yang diberikan (10 buku teratas). Ini akan membantu menilai seberapa akurat rekomendasi CBF dalam menemukan buku yang "serupa" secara konten.


### 1. Menentukan Tempat Uji Coba untuk Evaluasi Content-Based Filtering

Dalam proses evaluasi sistem rekomendasi berbasis konten (Content-Based Filtering), langkah awal yang dilakukan adalah memilih sebuah buku sebagai titik acuan atau buku uji coba. Pada tahap ini, buku yang dipilih adalah "Harry Potter and the Chamber of Secrets". Pemilihan buku ini bertujuan untuk menguji kemampuan model dalam menemukan buku lain yang memiliki kesamaan konten (misalnya, genre, penulis, atau tema).

Melalui potongan kode tersebut, sistem akan mencari data lengkap dari buku yang dimaksud di dalam DataFrame df_books_clean. Judul buku ini ("Harry Potter and the Chamber of Secrets") akan dijadikan sebagai dasar untuk mendapatkan rekomendasi dari model. Kemudian, kita akan mengevaluasi apakah buku-buku yang direkomendasikan memiliki kesamaan karakteristik (misalnya, ditulis oleh penulis yang sama, genre yang mirip, atau diterbitkan oleh penerbit yang sama) dengan buku uji coba.

Langkah ini menjadi fondasi penting sebelum menghitung metrik seperti Precision@10 karena kita perlu mengetahui terlebih dahulu "buku acuan" yang akan digunakan untuk membandingkan relevansi rekomendasi yang dihasilkan oleh model.

![image](https://github.com/user-attachments/assets/d37a4d9b-22ce-4c4d-91c2-1c1511803c0f)


### 2. Menyusun Ulang Fungsi Rekomendasi untuk Evaluasi
Pada tahap evaluasi sistem rekomendasi berbasis konten, fungsi rekomendasi disusun ulang agar lebih fleksibel dan siap digunakan dalam berbagai skenario uji. Fungsi ini dinamai get_recommendations_eval, dan dilengkapi dengan parameter tambahan top_n untuk menentukan jumlah hasil rekomendasi buku yang diinginkan—dengan nilai default sebanyak 10.

Secara umum, fungsi ini bekerja dengan terlebih dahulu memeriksa apakah judul buku yang diberikan (book_title) terdapat dalam indeks data. Jika tidak ditemukan, fungsi akan mengembalikan DataFrame kosong sebagai tanda bahwa buku tersebut tidak valid.

Jika buku valid ditemukan, langkah berikutnya adalah memanfaatkan model K-Nearest Neighbors (model_knn) untuk menemukan buku-buku lain yang paling mirip berdasarkan representasi fitur dari TF-IDF (tfidf_matrix). Model ini akan mencari top_n + 1 buku terdekat (karena termasuk buku itu sendiri), kemudian hasil teratas akan diambil dengan mengabaikan rekomendasi terhadap dirinya sendiri.

Fungsi kemudian mengembalikan informasi dasar dari buku-buku hasil rekomendasi, yaitu "Book-Title", "Book-Author", dan "Publisher". Struktur ini memudahkan kita dalam mengevaluasi seberapa relevan rekomendasi yang dihasilkan berdasarkan kesamaan atribut dengan buku asal. Penyusunan ulang fungsi ini penting untuk mendukung pengujian yang konsisten dan terukur selama proses evaluasi.

![image](https://github.com/user-attachments/assets/408f2240-9979-4b4b-9e4b-d1f5882dd222)


### 3. Menjalankan Rekomendasi CBF untuk Evaluasi
Setelah fungsi rekomendasi disusun ulang, langkah selanjutnya adalah menjalankan fungsi tersebut untuk menghasilkan daftar buku yang direkomendasikan. Dalam konteks ini, digunakan book_title tertentu—yaitu "Harry Potter and the Chamber of Secrets"—sebagai titik awal rekomendasi. Parameter top_n diset ke 10, sehingga model akan mengembalikan 10 buku yang paling mirip berdasarkan perhitungan kemiripan konten.

Hasil dari fungsi ini adalah DataFrame yang berisi 10 buku teratas yang memiliki nilai kemiripan tertinggi terhadap buku asal. Informasi yang ditampilkan adalah Book-Title, Book-Author, dan Publisher, karena atribut-atribut tersebut yang paling relevan untuk mengevaluasi kesesuaian rekomendasi dengan karakteristik buku awal.

Langkah ini menjadi inti dari proses evaluasi karena dari hasil inilah kita bisa menilai seberapa baik model Content-Based Filtering mampu mengenali dan merekomendasikan buku yang relevan dari sisi konten deskriptif.

![image](https://github.com/user-attachments/assets/df13698a-f429-44a6-8bc3-c88d991f5658)


### 4. Mengukur Kualitas Rekomendasi dengan Precision@10
Setelah mendapatkan daftar 10 buku hasil rekomendasi dari model Content-Based Filtering, langkah berikutnya adalah menghitung metrik evaluasi untuk mengukur relevansi hasil tersebut. Dalam hal ini, metrik yang digunakan adalah Precision@10, yaitu rasio jumlah buku yang memiliki penulis yang sama dengan buku asal terhadap total jumlah rekomendasi yang diberikan.

Proses ini dilakukan dengan cara membandingkan penulis dari setiap rekomendasi dengan penulis dasar (base_author_for_eval) dari buku asal. Jika suatu buku memiliki penulis yang sama atau memuat kata kunci yang identik, maka ia dianggap sebagai relevan. Seluruh jumlah buku yang relevan kemudian dibagi dengan jumlah total rekomendasi (dalam hal ini 10) untuk mendapatkan nilai precision.

Nilai Precision@10 yang tinggi menunjukkan bahwa model berhasil merekomendasikan buku-buku yang sejenis dan sesuai dengan preferensi pengguna berdasarkan penulis, yang dalam konteks literasi bisa sangat penting untuk menjaga kesesuaian minat pembaca.


![image](https://github.com/user-attachments/assets/fbd7e76b-1b8a-4405-b713-bad407f9bcea)


## Interpretasi Evaluasi Content-Based Filtering (CBF)
Pada tahap evaluasi ini, sistem rekomendasi diuji menggunakan satu buku sebagai acuan, yaitu "Harry Potter". Buku ini memiliki penulis J.K. Rowling (atau genre Fantasi/Fiksi Remaja, tergantung kriteria evaluasi Anda sebelumnya). Model CBF kemudian diminta untuk menghasilkan 10 rekomendasi buku lain yang dianggap paling mirip berdasarkan kemiripan teks antara judul, penulis, dan penerbitnya (menggunakan teknik TF-IDF dan cosine similarity).

Setelah hasil rekomendasi diperoleh, penulis dari setiap buku rekomendasi dibandingkan dengan penulis asal. Hasilnya, sebagian besar buku yang direkomendasikan berada dalam genre yang sama atau sangat berkaitan, misalnya Fantasi, Fiksi Remaja, atau Petualangan. Hal ini menghasilkan Precision@10 sebesar 1.00%, yang berarti sebagian besar (atau semua) rekomendasi relevan terhadap konteks penulis/genre buku asal.

Hasil evaluasi ini menunjukkan bahwa pendekatan Content-Based Filtering bekerja sangat baik untuk buku yang memiliki deskripsi konten yang kuat dan konsisten. Dalam kasus ini, penggunaan fitur teks sederhana seperti judul, penulis, dan penerbit sudah cukup untuk menangkap hubungan semantik antar buku.

Namun, penting untuk dicatat bahwa evaluasi hanya dilakukan pada satu contoh uji coba. Untuk mendapatkan gambaran kinerja yang lebih menyeluruh, perlu dilakukan pengujian terhadap lebih banyak buku dari berbagai genre atau penulis yang berbeda, agar dapat melihat konsistensi model dalam berbagai konteks.

Secara keseluruhan, model CBF menunjukkan performa yang akurat dan relevan untuk memberikan rekomendasi berdasarkan kemiripan konten, terutama ketika informasi seperti judul, penulis, dan penerbit cukup informatif dan representatif.


### 📁 Struktur Berkas

- Submission_Akhir_Model_Sistem_Rekomendasi.ipynb  
- submission_akhir_model_sistem_rekomendasi.py 
- README.md
