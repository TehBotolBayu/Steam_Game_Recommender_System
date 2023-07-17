# Laporan Proyek Sistem Rekomendasi - Bayu Abdurrosyid

## Project Overview

Industri video game telah menjadi salah satu industri hiburan terbesar dan paling menguntungkan di dunia. Dalam beberapa dekade terakhir, pertumbuhan industri ini sangat pesat dan telah mengubah lanskap hiburan global. Berdasarkan riset dari Statista, pada tahun 2023 penjualan disektor industri video game secara global diperkirakan mencapai 365.6 miliar USD yang didominasi produk game digital. Platform penjualan video game digital sangat berperan besar dalam industri video game. Platform digital mempermudah baik pengguna maupun publisher video game untuk memasarkan produk mereka secara daring. 
Memanfaatkan teknologi machine learning, platform digital seperti contohnya steam, dapat mengembangkan sistem rekomendasi yang berpotensi meningkatkan _user engagement_ dan penjualan produk mereka.
Sistem rekomendasi yang baik dapat menjadi sarana untuk meningkatkan penjualan produk video game. Dengan sistem rekomendasi, pengguna bisa mendapatkan informasi mengenai video game yang relevan dengan preferensi pribadi, sehingga memperbesar kemungkinan bagi pengguna tersebut untuk memilih atau membeli produk video game terkait.
Melihat besarnya peran sistem rekomendasi didalam industri komersil salah satunya di bidang video game, maka dari itu proyek ini dibuat untuk mengembangkan sistem rekomendasi menggunakan _machine learning_ yang dapat memberikan rekomenasi video game yang relevan kepada pengguna.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang diatas, masalah yang ingin diselesaikan dalam proyek ini antara lain:
- Karakteristik item apa yang dapat dijadikan patokan dalam membuat rekomendasi yang relevan bagi pengguna?
- Bagaimana cara melakukan pra pemrosesan data pengguna sebelum data dilatih ke model _machine learning_?
- Bagaimana cara mengembangkan sistem yang dapat memberikan rekomendasi video game yang relevan bagi pengguna?

### Goals

- Mengidentifikasi karakteristik video game tertentu yang dapat menentukan preferensi pengguna.
- Melakukan pra pemrosesan data pada _dataset_ dengan tepat agar dapat melatih model dengan baik.
- Mengembangkan sistem rekomendasi yang dapat memberikan rekomendasi produk video game yang relevan.
- Mengevaluasi sistem rekomendasi untuk mengetahui seberapa akurat rekomendasi yang diberikan kepada pengguna.

### Solution statements

Solusi yang dapat diterapkan untuk menyelesaikan masalah yang telah dipaparkan sebelumnya antara lain:
-	Memahami dan menganalisis fitur pada data vide game untuk mengetahui seberapa relevan video game tertentu terhadap preferensi pengguna?
-	Melakukan pra pemrosesan pada data menggunakan beberapa teknik seperti menangani keberadaan nilai null dan menyesuaikan tipe data.
-	Mengembangkan model _machine learning_ regresi untuk memprediksi rekomendasi data video game menggunakan teknik content based filtering dengan metode _cosine similiarity_.

## Data Understanding

 _dataset_ yang dipakai dalam mengembangkan proyek ini berjudul [Steam store games](https://www.kaggle.com/datasets/nikdavis/steam-store-games).Dataset _Steam store games_ menyediakan informasi penting mengenai video game yang terdapat di platform steam. _Dataset Steam Store Games_ memiliki informasi mengenai genre, kategori, dan tag game yang lengkap dan dapat menjadi patokan preferensi pengguna. 

Tabel berikut memaparkan rincian mengenai file yang terdapat pada _dataset Steam store games_ :

|nama file|baris|kolom| ukuran file (mb)|
|-|-|-|-|
|steam.csv| 27075 | 17| 5.55|
|steam_description_data.csv| 27334| 4| 9035|
|steam_media_data.json| 27332| 5| 87.36|
|steam_requirements_data.csv| 27319| 6| 34.29|
|steam_support_info.csv| 27136| 4| 1.85|
|steamspy_tag_data.csv| 29022| 372| 20.97|

File yang akan dipakai dalam pengembangan sistem rekomendasi game adalah file steam.csv. File steam.csv berisi informasi mengenai rincian video game.

Variabel-variabel yang terdapat pada file steam.csv adalah sebagai berikut:
- appid: id unik dari video game atau aplikasi pada steam.
- name: nama atau judul dari video game.
- release_date: The date when the game was released.
- english: 1 jika game tersebut berbahasa inggris, 0 jika tidak.
- developer: The company or individual responsible for developing the game.
- publisher: The company or entity that published and distributed the game.
- platforms: sistem operasi atau perangkat yang dapat menjalankan video game
- required_age: usia minimal yang disarankan untuk memainkan video game
- categories: kategori dari video game
- genres: genre dari video game
- steamspy_tags: tag pada video game
- achievement: jumlah pencapaian yang dapat diraih oleh pemain pada video game
- positive_ratings: jumlah pengguna yang merekomendasikan game
- negative_ratings: jumlah pengguna yang tidak merekomendasikan game.
- average_playtime: rata-rata lama pemain menghabiskan waktu pada game
- median_playtime: nilai tengah data lama pemain menghabiskan waktu pada game
- owners: jumlah pengguna yang memiliki game
- price: harga video game dalam USD

## Exploratory Data Analysis
Pemahaman data perlu dilakukan sebelum data dipersiapkan untuk dilatih ke model _machine learning_. 

||appid|	english|	required_age|	achievements|	positive_ratings|	negative_ratings|	average_playtime|	median_playtime|	price|
|-|-|-|-|-|-|-|-|-|-|
|count|	2.707500e+04|	27075.000000|	27075.000000|	27075.000000|	2.707500e+04|	27075.000000|	27075.000000|	27075.00000|	27075.000000|
|mean	|5.962035e+05|	0.981127|	0.354903|	45.248864|	1.000559e+03|	211.027147|	149.804949|	146.05603|	6.078193|
|std	|2.508942e+05|	0.136081|	2.406044|	352.670281|	1.898872e+04|	4284.938531|	1827.038141|	2353.88008|	7.874922|
|min|	1.000000e+01|	0.000000|	0.000000|	0.000000|	0.000000e+00|	0.000000|	0.000000|	0.00000|	0.000000|
|25%	|4.012300e+05|	1.000000|	0.000000|	0.000000|	6.000000e+00|	2.000000|	0.000000|	0.00000|	1.690000|
|50%	|5.990700e+05|	1.000000	|0.000000	|7.000000|	2.400000e+01|	9.000000|	0.000000|	0.00000|	3.990000|
|75%	|7.987600e+05|	1.000000	|0.000000|	23.000000|	1.260000e+02|	42.000000|	0.000000|	0.00000	|7.190000|
|max|	1.069460e+06|	1.000000|	18.000000|	9821.000000|	2.644404e+06|	487076.000000|	190625.000000|	190625.00000|	421.990000|

Melalui fungsi describe() dapat diketahui deskripsi numerik dari masing-masing data. Terdapat beberapa hal yang dapat disimpulkan dari deskripsi pada data game diantaranya 
- Usia minimal untuk memainkan video game berada di rentang angka 0 sampai dengan 18 tahun, namun rata-rata usia hanya 0.3. Dengan kata lain mayoritas game memiliki usia pemain minimal 0 tahun.
- Mayoritas game memliki bahasa inggris, dilihat dari nilai rata-rata english sebesar 0.98
- jumlah positive rating jauh lebih banyak dibanding negative rating. Dengan kata lain kemungkinan pengguna menyukai suatu game dan merekomendasikannya ke pengguna lain cukup besar dibanding tidak merekomendasikannya.
- Nilai tengah atau median lama waktu bermain menceng kekanan, yang dilihat dari selisih rata-rata dan median yang cukup besar. Dengan kata lain mayoritas pengguna lebih suka menghabiskan waktu untuk memainkan sedikit game. 

Diantara semua fitur, yang dapat dijadikan patokan untuk menentukan preferensi pengguna adalah fitur yang berisi informasi mengenai konten dari game tersebut. Fitur-fitur tersebut antara lain nama, developer, publisher, platform, categories, genres, steamspy_tags, dan price. Fitur developer dan publisher dapat menjelaskan apakah pengguna menyukai video game hasil produksi perusahaan tertentu atau tidak. Fitur nama dapat menjelaskan secara tidak langsung mengenai konten yang dapat tersedia pada game. Fitur platform menjelaskan apakah pengguna memiliki preferensi tertentu untuk memainkan video game di sistem atau perangkat teretentu. Fitur categories, genres, steamspyt_tags dapat menandakan bahwa pengguna menyukai sekelompok game tertentu. Sementara itu fitur price dapat menjelaskan apakah pengguna menyukai game gratisan, ataupun berbayar.

Melihat banyaknya fitur yang berpotensi menjadi patokan untuk memprediksi preferensi pengguna, dalam proyek ini hanya akan diambil tiga fitur yang dianggap paling menggambarkan preferensi pengguna untuk mengurangi penggunaan memori saat dilakukan pemrosesan data. Fitur tersebut antara lain fitur categories, genres, dan steamspy_tags. Alasan diambilnya ketiga fitur ini dikarenakan ketika pengguna melakukan _browsing_ untuk mencari video game, mayoritas pengguna mencari game dengan genre atau tag tertentu terlebih dahulu. Ketiga fitur ini juga yang paling dapat memberikan gambaran bagi pengguna mengenai konten yang terdapat di dalam video game tertentu.

Menggunakan fungsi unique() dapat dilihat beberapa jenis data unik yang terdapat pada fitur kategorik. Pada fitur categories terdapat 3333 jumlah data unik. Pada fitur genre terdapat 1552 jumlah data unik. Sementara pada fitur genre terdapat 6423 jumlah data unik.

Untuk dapat mengolah data tersebut menjadi data yang dapat dilatih ke algoritma _machine learning_ perlu dilakukan persiapan data. Ketiga fitur akan digabung menjadi satu, kemudian data yang berformat dataframe akan dibah menjadi matrix untuk dilatih ke algoritma.

## Data Preparation

### Menggabung fitur
Fitur yang telah dipilih untuk mendeskripsikan konten dari video game diantaranya fitur categories, genres, dan steamspy_tags. Fitur-fitur tersebut digabung ke dalam fitur baru bernama fitur tag. 

### Membuat matriks TF-IDF
Selanjutnya data yang baru akan diubah menjadi matriks hasil vektoriassi TF-IDF atau _Term Frequency Inverse Document Freqeuency_ yang bertujuan untuk mengukur seberapa penting suatu kata terhadap kata lain pada data. TF-IDF dapat mengetahui kumpulan tag yang paling sering muncul pada data game yang pernah dimainkan pengguna. Tag ini akan dipakai untuk memprediksi rekomendasi game kepada pengguna. Pada proyek ini digunakan fungsi tfidfVectorizer() dari library sklearn.


## Modeling
### Content Based Filtering
_Content based filtering_ atau sistem rekomendasi berbasis konten merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai atau dilihat kepada pengguna. Algoritma yang dipilih dalam pengembangan sistem rekomendasi berbasis konten adalah _cosine similiarity_

Matriks yang dihasilkan dari TF-IDF, akan dilatih pada model _cosine similiarity_. _Cosine similiarity_ menghitung kemiripan antar item dengan cara menghitung sudut antar vektor. Rumus dari _cosine similiarity_ adalah sebagai berikut:
$$Cosine Similiarity = \frac{A \cdot B}{||A|| \cdot ||B||}$$ 

||A|| = magnitude dari vector A
    
||B|| = magnitude dari vector B

_Cosine similiarity_ menghasilkan _sparse matriks_ yang menunjukkan kemiripan antar video game berdasarkan konten tag yang dimiliki.  

## Memberikan Hasil Rekomendasi
Fungsi content_recommender menemukan dafar game rekomendasi menggunakan matriks _cosine similiarity_ yang didapatkan pada hasil sebelumnya. Funsi ini bekerja dengan mencari 5 game teratas dengna nilai kemiripan terbesar.

Berikut adalah game yang akan dicari rekomendasinya:
appid|	name|	release_date|	english|	developer|	publisher|platforms|required_age|achievements|	positive_ratings|	negative_ratings|average_playtime|median_playtime|	owners|	price|	tag|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
	911400|	Assassin's Creed® III Remastered	|2019-03-29|	1	|Ubisoft Entertainment|	Ubisoft Entertainment\t\t\t\t|	windows	|0|	0	|475|	983|	80|	80|	50000-100000|	33.99|	Single-player;Partial Controller Support; Acti...

Dan hasil rekomendasi dari game tersebut adalah sebagai berikut:
||name|	tag|
|-|-|-|
0	|Assassin's Creed Freedom Cry|	Single-player; Action;Adventure; Action;Advent...|
1|	Assassin’s Creed® Rogue|	Single-player;Partial Controller Support; Acti...|
2|	Assassin’s Creed® Chronicles: China	|Single-player;Steam Trading Cards;Partial Cont...|
3	|Assassin's Creed® Syndicate|	Single-player;In-App Purchases;Partial Control...|
4	|Hitman: Contracts	|Single-player; Action; Stealth;Action;Assassin|



Hasilnya, rekomendasi dari game Assassin's Creed® III Remastered tentu saja didominasi oleh video game dengan dari seri yang sama yaitu Assassin's Creed. Dan keseluruhan game rekomendasi memiliki tema yang hampir sama.

## Evaluasi
Evaluasi model dilakukan guna memeriksa tingkat akurasi yang dimiliki oleh tiap model. Hasil rekomendasi menunjukan item teratas yang mungkin disukai pengguna. Karena patokan preferensi pengguna berasal dari kolom tag, maka untuk mengevaluasi hasil rekomendasi, akan dihitung seberapa mirip tag hasil rekomendasi dengan item dari pengguna.

Hasil rekomendasi tersebut dapat digolongkan kedalam kategori berikut:
- True Positive: hasil rekomendasi yang benar-benar disukai pengguna
- False Positive: hasil rekomendasi yang tidak disukai pengguna
- True Negative: hasil yang tidak direkomendasikan dan tidak disukai pengguna
- False Negative: hasil yang tidak direkomendasikan namun disukai pengguna


Model evaluasi yang cocok untuk menentukan akurasi dari hasil rekomenadsi adalah _precision_, _recall_, dan _f1-score_. Berikut adalah penjelasan mengenai masing-masing metrik evaluasi:
- _Precision_ mengukur jumlah proporsi data positif yang diprediksi benar oleh sistem dengan jumlah total jumlah prediksi. Nilai _precision_ yang tinggi dapat mengurangi hasil prediksi yang merekomendasikan item yang tidak seharusnya direkomendasikan.
$$Precision = \frac{TP}{TP+FP}$$ 

    TP = prediksi _true positive_
    
    FP = prediksi _false positive_

- _Recall_ mengukur proporsi data positif yang diprediksi benar oleh sistem dengan semua data  yang seharusnya direkomendasikan. Nilai _recall_ yang tinggi dapat meningkatkan jumlah item yang memang seharusnya direkomendasikan kepada pengguna.
$$Precision = \frac{TP}{TP+FN}$$ 
    
    FN = prediksi _false negative_

- _F1-score_ mengukur rata-rata harmonik dari _precision_ dan _recall_ yang dapat merepresentasikan keseimbangan dari hasil kedua jenis evaluasi. 
$$F_{1} = 2\times\frac{Recall \times Precision}{Recall + Precision}$$ 


Hasil evaluasi dilakukan dengan membandingkan tag dari item pengguna yang menjadi patokan preferensi pengguna, dengan tag hasil rekomendasi sistem. Pertama buat _list_ yang berisi tag dari item yang akan direkomendasikan. _List_ ini akan menjadi patokan preferensi sebenarnya bagi evaluasi.

Fungsi evaluate menerima _list_ yang berisi tag dari item preferensi pengguna, dan juga hasil 5 rekomendasi teratas dari _cosine similiarity_. Menggunakan proses iterasi pada seluruh tag hasil rekomendasi, fungsi akan menghitung jumlah _true positive_, dengan mengecek apakah tag hasil rekomendasi ada pada tag preferensi asli. Fungsi kemudian akan mengembalikan nilai rata-rata _recall_, _precision_, dan nilai _f1-score_.

Hasil evaluasi dari prediksi terhadap item diatas dapat dilihat pada tabel berikut.
||result|
|-|-|
precision|	0.831429|
recall|	0.8|
f1_score|	0.815412|


## Referensi
[1] Pramesti, D. A. P. D., & Santiyasa, I. W. (2022). Penerapan Metode Content-Based Filtering dalam Sistem Rekomendasi Video Game. JNATIA, 1, 229-34.