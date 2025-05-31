# Laporan Proyek Machine Learning - Sinta Ezra Wati Gulo

## Project Overview
### Latar Belakang
Sistem rekomendasi telah menjadi komponen kunci dalam industri hiburan digital, khususnya dalam membantu pengguna menemukan konten yang relevan dari ribuan pilihan yang tersedia. Ketika jumlah film yang tersedia terus bertambah setiap hari, pengguna cenderung mengalami kesulitan dalam memilih konten yang sesuai dengan preferensi mereka. Hal ini tidak hanya berdampak pada pengalaman pengguna, tetapi juga dapat mengurangi waktu tonton, menurunkan kepuasan pengguna, dan meningkatkan risiko perpindahan ke platform kompetitor.

Masalah ini perlu diselesaikan karena ketidakmampuan pengguna dalam menemukan konten yang relevan secara cepat dapat menurunkan tingkat kepuasan dan retensi pengguna pada platform hiburan digital. Untuk itu, sistem rekomendasi menjadi solusi penting yang memungkinkan personalisasi konten bagi setiap pengguna secara efisien.

Salah dua pendekatan populer dalam sistem rekomendasi adalah Content-Based Filtering (CBF) dan Collaborative Filtering (CF). CBF bekerja dengan merekomendasikan item berdasarkan kesamaan atribut konten—seperti genre atau tag—dengan item yang telah disukai atau ditonton oleh pengguna sebelumnya. Sementara itu, CF menyarankan item berdasarkan kesamaan perilaku pengguna, yakni dengan melihat pola rating pengguna lain yang memiliki preferensi serupa.

Keberhasilan penerapan sistem rekomendasi telah dibuktikan dalam praktik industri. Netflix, misalnya, menerapkan sistem rekomendasi yang memadukan pendekatan content-based dan collaborative filtering untuk mempertahankan atensi pengguna dan mengurangi churn rate (Gomez-Uribe & Hunt, 2015). Studi komprehensif oleh Bobadilla et al. (2013) juga menunjukkan bahwa sistem rekomendasi memiliki peran penting dalam meningkatkan efisiensi pencarian informasi dan pengalaman pengguna secara keseluruhan.

Dengan demikian, penerapan sistem rekomendasi dalam domain film tidak hanya meningkatkan pengalaman pengguna, tetapi juga berdampak langsung terhadap keberhasilan bisnis dan loyalitas pengguna terhadap platform.

### Referensi
Gomez-Uribe, C. A., & Hunt, N. (2015). The Netflix recommender system: Algorithms, business value, and innovation. 𝘈𝘊𝘔 𝘛𝘳𝘢𝘯𝘴𝘢𝘤𝘵𝘪𝘰𝘯𝘴 𝘰𝘯 𝘔𝘢𝘯𝘢𝘨𝘦𝘮𝘦𝘯𝘵 𝘐𝘯𝘧𝘰𝘳𝘮𝘢𝘵𝘪𝘰𝘯 𝘚𝘺𝘴𝘵𝘦𝘮𝘴 (𝘛𝘔𝘐𝘚), 6(4), 1–19. [https://doi.org/10.1145/2843948](https://doi.org/10.1145/2843948)

Bobadilla, J., Ortega, F., Hernando, A., & Gutiérrez, A. (2013). Recommender systems survey. 𝘒𝘯𝘰𝘸𝘭𝘦𝘥𝘨𝘦-𝘉𝘢𝘴𝘦𝘥 𝘚𝘺𝘴𝘵𝘦𝘮𝘴, 46, 109–132. [https://doi.org/10.1016/j.knosys.2013.03.012](https://doi.org/10.1016/j.knosys.2013.03.012)

## Business Understanding
### Problem Statements
- Pengguna mengalami kesulitan menemukan film yang sesuai dengan preferensi pribadi karena banyaknya pilihan film yang tersedia.
- Ketiadaan sistem yang mampu menyajikan rekomendasi film secara personal menyebabkan pengguna merasa bosan dan berpotensi meninggalkan platform.

### Goals
- Membangun sistem rekomendasi film yang dapat memberikan saran film sesuai dengan preferensi pengguna berdasarkan histori tontonan dan karakteristik film (genre dan tag).
- Menyediakan top-N rekomendasi film yang mudah diakses agar pengguna tidak kesulitan memilih film yang sesuai.

### Solution Statements
Untuk mencapai tujuan tersebut, dalam proyek ini digunakan dua pendekatan sistem rekomendasi, yaitu:
- Content-Based Filtering: Sistem merekomendasikan film berdasarkan kemiripan konten, yaitu genre dan tag film, dengan film yang telah disukai pengguna. Pendekatan ini menggunakan data metadata film untuk menghitung kemiripan antar film.
- Collaborative Filtering: Sistem merekomendasikan film berdasarkan pola kesamaan preferensi antar pengguna, yaitu film-film yang disukai oleh pengguna dengan profil preferensi mirip akan direkomendasikan.

## Data Understanding
Proyek ini menggunakan dataset Movie Rating Dataset yang dapat diakses melalui Kaggle pada link berikut [Movie Rating Dataset](https://www.kaggle.com/datasets/rockyt07/movie-rating-dataset?select=movies.csv). Dataset ini terdiri dari 3 file yaitu movies.csv, ratings.csv, dan tags.csv.

### Variabel-variabel pada Movie Rating Dataset adalah sebagai berikut:
1. movies.csv
   - movieId: ID unik untuk setiap film.
   - title: Judul film yang mencakup tahun rilis dalam tanda kurung untuk mengenali film secara spesifik, terutama jika terdapat film dengan nama serupa yang dirilis di tahun berbeda.
   - genres: Kategori/genre film, dipisahkan oleh karakter | jika lebih dari satu genre.
2. ratings.csv
   - userId: ID unik untuk setiap user.
   - movieId: ID unik untuk setiap film.
   - rating: Menunjukkan skor atau penilaian yang diberikan oleh pengguna terhadap suatu film dengan skala 0-5.
   - timestamp: Mencatat waktu ketika rating diberikan.
3. tags.csv
   - userId: ID unik untuk setiap user.
   - movieId: ID unik untuk setiap film.
   - tag: Menunjukkan ata kunci atau frasa pendek yang diberikan oleh pengguna untuk menggambarkan film tersebut.
   - timestamp: Mencatat waktu ketika tag diberikan.

### Exploratory Data Analysis 
1. Data df_movies
   - Informasi df_movies
     <br>![image](https://github.com/user-attachments/assets/489fb472-f2eb-477b-82ef-fa7e3e5ec32d)
     - Ada 9.742 baris dalam dataset.
     - Terdapat 3 kolom yaitu `movieId`, `title`dan `genres`.
   - Distribusi Film per Tahun
     <br>![distribusi film](img/distribusifilmpertahun.png)
     <br>Grafik di atas menunjukkan distribusi film dari tahun ke tahun dan menunjukkan peningkatan semakin bertambahnya tahun terutama disekitar tahun 2008-2010.
   - Distribusi Genre
     <br>![distribusi genre](img/distribusi_genre.png)
     <br>Secara keseluruhan, grafik di atas menunjukkan distribusi genre dari yang palng dominan hingga yang paling sedikit pada data.
   - Jumlah Genre per Film
     <br>![genre flm](img/jumlah_genre_film.png)
     <br>Grafik menunjukkan sebagian besar film hanya memiliki 1 hingga 3 genre, menunjukkan bahwa mayoritas film memiliki fokus genre yang jelas, dimana film dengan 2 genre adalah yang paling umum.
2. Data df_ratings
   - Informasi df_ratings
     <br>![image](https://github.com/user-attachments/assets/c6475f7a-b27f-4159-90f0-b0ec9bdce6c8)
     - Ada 100.836 baris dalam dataset.
     - Terdapat 4 kolom yaitu `userId`, `movieId`, `rating`, dan `timestamp`.
    - Distribusi Rating
      <br>![rating](img/distribusi_rating.png)
      <br>Secara keseluruhan, grafik di atas menunjukkan distribusi rating dari yang mana rating terkecil adalah 0.5 dan paling besar 0.5. Rating 4.0 merupakan yang paling sering diberikan, menandakan banyak pengguna cenderung memberi penilaian positif.
   - Jumlah Rating per User
     <br>![rating](img/rating_user.png)
     <br>Grafik di atas menunjukkan jumlah rating yang diberikan oleh user, dimana sebagian besar pengguna memberikan kurang dari 100 rating, menunjukkan banyak pengguna yang kurang aktif.
   - Jumlah Rating per Film
     <br>![rating](img/rating_film.png)
     <br>Grafik di atas menunjukkan jumlah rating yang dimiliki oleh film, dimana sebagian besar film hanya menerima sedikit rating, menunjukkan banyak film kurang populer atau jarang ditonton.
   - Top 10 Film dengan Jumlah Rating Terbanyak
     <br>![rating](img/top10_film.png)
     <br>Grafik di atas  menunjukkan judul-judul film yang menjadi top 10 film dengan rating terbanyak, dimana film klasik dari era 1990-an mendominasi daftar ini.
3. Data df_tags
   - Informasi df_tags
     <br>![image](https://github.com/user-attachments/assets/17962186-5adc-42c0-8bca-33022d50c329)
   - Jumlah Tag Unik
     <br>![image](https://github.com/user-attachments/assets/211c9291-a1c6-4991-9805-d6b291d0e36d)
     <br>Output di atas menunjukkan bahwa terdapat 1.589 tag unik pada df_tags.
   - Top 10 Tag yang Paling Sering Muncul
     <br>![tag](img/top10_tag.png)
     <br>Tag In Netflix queue muncul paling banyak, jauh melampaui tag lainnya. Ini menunjukkan bahwa banyak pengguna menandai film bukan berdasarkan konten atau genre, tetapi sebagai daftar tontonan atau preferensi pribadi untuk ditonton nanti. Tag-tag berikutnya mencerminkan karakteristik atau tema film.
   - Top 10 Tag yang Paling Jarang Muncul
     <br>![tag](img/top10_tagterbawah.png)
     <br>Semua tag hanya muncul 1 kali, menunjukkan bahwa tag-tag ini sangat jarang digunakan oleh pengguna. Ini bisa menandakan niche interest atau ketidakkonsistenan dalam proses penandaan.
   - Jumlah Tag per Film
     <br>![tag](img/tag_film.png)
     <br>Sebagian besar film hanya memiliki 1–2 tag, dengan lebih dari 1400 film hanya memiliki 1 tag saja.
   - Jumlah Tag per User
     <br>![tag](img/tag_user.png)
     <br>Sebagian besar user hanya memberikan kurang dari 10 tag, bahkan banyak yang hanya memberi 1–2 tag saja.

## Data Preparation
Pada bagian ini akan dilakukan beberapa tahap persiapan data, yaitu:
1. Data Preparation untuk Content Based Filtering
   - Menghapus data dengan genres = (no genres listed) pada df_movies
     <br>Pada bagian ini, dilakukan penghapusan untuk data yang `genres` nya adalah (no genres listed), karena film yang tidak memiliki genre tidak memberikan informasi berarti untuk sistem rekomendasi, terutama pada metode Content Based Filtering yang mengandalkan deskripsi konten (genre dan tag) untuk menemukan kesamaan antar item (film). Dimana jumlah data dengan genres = '(no genres listed)' adalah 34, sehingga data tersebut lebih baik dihapus. Adapun jumlah data setelah dihapus menjadi 9.708, yang mana sebelumnya adalah 9.742.
   - Menggabungkan tag berdasarkan movieId
     <br>Pada tahapan ini melakukan group by aggregation pada df_tags berdasarkan movieId, lalu menggabungkan tag menjadi satu string. Setiap tag dari pengguna terhadap satu movieId dikumpulkan dan digabungkan menggunakan metode berikut.<br>
     ```python
     tags_agg = df_tags.groupby('movieId')['tag'].apply(lambda x: ' '.join(x)).reset_index()
     ```
     Alasan proses ini dilakukan adalah karena tag dari pengguna merepresentasikan deskripsi subjektif tambahan dari sebuah film. Menggabungkannya memungkinkan sistem mengenali karakteristik film secara lebih kaya.
   - Menggabungkan df_movies dengan df_tags berdasarkan movieId
     <br>Pada tahap ini, dilakukan penggabungan df_movies dengan df_tags menggunakan `merge()`. Alasannya adalah untuk menyatukan informasi genre (dari df_movies) dan tag (dari df_tags) agar dapat digunakan bersama-sama dalam representasi konten. Berikut adalah hasilnya:
     <br>![image](https://github.com/user-attachments/assets/1e7e0af2-eeb3-4e61-ad4a-cd45474134e8)
   - Menangani missing value pada movies_tags
     <br>Pada tahap ini, dilakukan penanganan missing value pada movie_tags. Dimana,  dapat dilihat pada movies_tags bahwa ada beberapa data yang tag nya tidak memiliki nilai (missing value), sehingga perlu ditangani. Pada tahap ini dilakukan imputasi data kosong (missing value) menggunakan nilai default (fillna('')). Metode ini mengisi nilai NaN pada kolom tag hasil merge dengan string kosong ' '. Alasannya adalah untuk menghindari error saat pengolahan teks, seperti ketika membuat representasi vektor konten. Film tanpa tag tetap dapat diproses hanya dengan informasi genre.
   - Memisahkan kolom genres sebagai teks biasa
     <br>Pada tahap ini dilakukan data transformation, dari format string dengan delimiter | menjadi format teks biasa (natural text). Dimana kolom genres diubah dari 'Action|Adventure|Fantasy' menjadi 'Action Adventure Fantasy'. Alasannya adalah agar genre dapat diolah oleh model representasi teks seperti TF-IDF, yang mengharapkan teks biasa, bukan string dengan delimiter khusus.
   - Membuat kolom gabungan antara genres dan tag dengan nama content
     <br>Pada tahap ini kolom genres dan tag digabung menjadi satu kolom content menggunakan +. Karena kolom content akan digunakan sebagai input untuk proses ekstraksi fitur (TF-IDF) pada Content Based Filtering. Penggabungan ini menciptakan representasi yang lebih lengkap dari konten film. 
     
3. Data Preparation untuk Collaborative Filtering
   - Melakukan Encoding pada userId dan movieId
     <br>Pada tahap ini melakukan encoding menggunakan dictionary mapping (dict). Alasannya adalah karena Collaborative Filtering membutuhkan input berupa indeks numerik yang unik untuk setiap pengguna dan film. Dengan representasi indeks ini, model dapat belajar merepresentasikan setiap user dan item sebagai vektor embedding berdimensi tetap
   - Melakukan normalisasi pada rating
     <br>Pada tahap ini, rating dinormalisasi ke rentang 0–1. Alasannya adalah karena normalisasi membantu model memahami preferensi relatif pengguna, dan menghindari bias terhadap pengguna yang cenderung memberikan rating terlalu tinggi atau rendah. Hasil normalisasinya disimpan dalam kolom rating_scaled seperti berikut:
     <br>
   - Split data train dan validasi
     <br>Pada tahap ini dilakukan split data train dan validasi dengan rasio 80:20. Alasannya tahap ini dilakukan adalah untuk mengevaluasi kinerja model Collaborative Filtering secara objektif, penting memiliki data validasi yang tidak digunakan saat pelatihan.
   



