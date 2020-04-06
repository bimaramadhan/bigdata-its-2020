# Dokumentasi Movie Recommendation Engine menggunakan Apache Spark (KNIME)
## Daftar Isi
- [Business Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#business-understanding)
- [Data Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#data-understanding)
- [Data Preparation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#data-preparation)
- [Modeling](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#modeling)
- [Evaluation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#evaluation)
- [Deployment](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#deployment)
- [Workflow KNIME](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#workflow-knime)
- [Perbandingan Waktu yang Diperlukan File Reader dan CSV to Spark untuk Membaca File](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas3#perbandingan-waktu-yang-diperlukan-file-reader-dan-csv-to-spark-untuk-membaca-file)

# Business Understanding
Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
- Melihat daftar film terbaik berdasar data rating yang ada
- Mengelompokkan film berdasarkan genre yang diinginkan
- Melihat daftar film populer pada tiap genre
- Membuat sistem rekomendasi film

# Data Understanding

- Dataset yang digunakan adalah kumpulan data yang menampung rating berbasis 5-bintang berjumlah 20000263 rating, dan 465564 tag dari keseluruhan 27278 film. Data menampung rating dari 138493 user sejak tanggal 9 Januari 1995 sampai 31 Maret 2015. Dataset ini sendiri dibuat pada 17 Oktober 2016.
- Dataset ini berisi 6 genome-scores.csv, genome-tags.csv, links.csv, movies.csv, ratings.csv and tags.csv
- Ratings Data File Structure (ratings.csv)
  - Semua peringkat ada di file ratings.csv. Setiap baris file ini setelah baris tajuk mewakili satu peringkat satu film oleh satu pengguna, dan memiliki format berikut: userId, movieId, rating, timestamp
  - Baris-baris di dalam file ini diurutkan terlebih dahulu dari userId, lalu, di dalam pengguna, oleh movieId.
  - Peringkat dibuat pada skala 5 bintang, dengan peningkatan setengah bintang (0,5 bintang - 5,0 bintang).
  - Timestamp mewakili detik sejak tengah malam Waktu Universal Terkoordinasi (UTC) 1 Januari 1970.
- Tags Data File Structure (tags.csv)
  - Semua tag terdapat dalam file tags.csv. Setiap baris file ini setelah baris tajuk mewakili satu tag yang diterapkan pada satu film oleh satu pengguna, dan memiliki format berikut: userId, movieId, tag, cap waktu
  - Baris-baris di dalam file ini diurutkan terlebih dahulu dari userId, lalu, di dalam pengguna, oleh movieId.
  - Tag adalah metadata yang dibuat pengguna tentang film. Setiap tag biasanya satu kata atau frasa pendek. Arti, nilai, dan tujuan dari tag tertentu ditentukan oleh setiap pengguna.
  - Timestamp mewakili detik sejak tengah malam Waktu Universal Terkoordinasi (UTC) 1 Januari 1970.
- Movies Data File Structure (movies.csv)
  - Informasi film terdapat dalam file movies.csv. Setiap baris file ini setelah baris tajuk mewakili satu film, dan memiliki format berikut: movieId, judul, genre
  - Judul film dimasukkan secara manual atau diimpor dari https://www.themoviedb.org/, dan termasuk tahun rilis dalam tanda kurung. Kesalahan dan ketidakkonsistenan mungkin ada dalam judul-judul ini.
- Links Data File Structure (links.csv)
  - Pengidentifikasi yang dapat digunakan untuk menautkan ke sumber data film lain terkandung dalam file links.csv. Setiap baris file ini setelah baris tajuk mewakili satu film, dan memiliki format berikut: movieId, imdbId, tmdbId
  - movieId adalah pengidentifikasi untuk film yang digunakan oleh https://movielens.org. E.g., film Toy Story memiliki tautan https://movielens.org/movies/1.
  - imdbId adalah pengidentifikasi untuk film yang digunakan oleh http://www.imdb.com. E.g., film Toy Story memiliki tautan http://www.imdb.com/title/tt0114709/.
  - tmdbId adalah pengidentifikasi untuk film yang digunakan oleh https://www.themoviedb.org. E.g., film Toy Story memiliki tautan https://www.themoviedb.org/movie/862.
- Tag Genome (genome-scores.csv and genome-tags.csv)
  - Tag Genome adalah struktur data yang berisi skor relevansi tag untuk film. Strukturnya adalah matriks padat: setiap film dalam genom memiliki nilai untuk setiap tag dalam genome.
  - Seperti yang dijelaskan dalam artikel ini, tag genome mengkodekan seberapa kuat film menunjukkan properti tertentu yang diwakili oleh tag (atmosfer, pemicu pemikiran, realistis, dll.). Tag genome dihitung menggunakan algoritma pembelajaran mesin pada konten kontribusi pengguna termasuk tag, peringkat, dan ulasan tekstual.
  - Genome dibagi menjadi dua file. File genome-score.csv berisi data relevansi tag-film dalam format berikut: movieId, tagId, relevansi
  - File kedua, genome-tags.csv, memberikan deskripsi tag untuk ID tag dalam file genome, dalam format berikut: tagId, tag
  - Nilai-nilai tagId dihasilkan ketika set data diekspor, sehingga mereka dapat bervariasi dari versi ke versi set data MovieLens.
- Sumber : [MovieLens 20M Dataset](https://grouplens.org/datasets/movielens/)

# Data Preparation

- data disiapkan dengan dua cara, yang satu menyiapkan data yang didownload dari link di atas, <br/>
  karena berbentuk csv dan menyiapkan data   yang menggunakan spark. dua persiapan tersebut dilakukan<br/> 
  dengan menyiapkan node di KNIME.

### File Reader File

- yang pertama membaca data dari file yang sudah di download dari file terlampir. yang dibaca hanya <br/>
  movies.csv<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/file_reader.PNG "file reader")<br>

- dengan melakukan konfigurasi seperti ini, dengan memastikan movieID terbaca<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/file_reader_conf.PNG "file reader conf")<br>

- dari ini kita melakukan konfigurasi di dalam node add fields untuk menambahkan userid dan timestamp.<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/add_fields.PNG "add field")<br>

- di dalam add field terdapat workflow yang dapat menyeting userid dan timestamp<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/node_add_fields.PNG "add field")<br>

- melakukan konfigurasi di dalam node constant value untuk menyeting timestamp dan node selanjutnya untuk menyeting 
  userid<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/node_timestamp.PNG "add field")
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/timestamp.PNG "add field")<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/node_userid.PNG "add field")
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/userid.PNG "add field")<br>

- melakukan penambahan node row splitter untuk memecah data untuk keperluan mentraining data serta memilih 20 film<br/>
  yang dipilih secara acak.<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/row_splitter.PNG "add field")<br>

- melakukan konfigurasi di dalam row splitter seperti ini<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/row_splitter_conf.PNG "add field")<br>

- open vie node tersebut untuk melihat hasilnya<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/node_rating.PNG "add field")<br>

- hasil rating didapati seperti ini, dengan keterangan tertera pada gambar, hasil ini sesuai dengan userid yang <br/>
  disetting<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/hasil_ratings.PNG "add field")<br>

### File Reader versi SPARK

- memulai dengan memasang node local big data environment untuk disambung ke node spark<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/local_bigdata.PNG "add field")<br>

- pastikan konfigurasi seperti ini<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/conf_local_bigdata.PNG "add field")<br>

- sambungkan local environment big data dengan spark, sehingga dapat membaca file dari directory yang tertera<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/spark.PNG "add field")
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/conf_spark.PNG "add field")<br>

- pasang node spark partitioning untuk melakukan partisi 80-20 pada data, setelah itu datanya digunakan untuk<br/> 
  training model dataset<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/partition.PNG "add field")<br>

- pastikan memilih persen dan memilih draw randomly.<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/conf_partition.PNG "add field")<br>

# Modeling

- proses modeling dimulai ketika menggabungkan data di node spark concatenate, dan node dari ini untuk<br>
  menjalankan algoritma buat modeling dengan memakai data training set, yang nantinya akan di tes dengan test-set.<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/model.PNG "add field")<br>

# Evaluation

- data yang sudah diprediksi berupa seperti ini
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/hasilprediksi.PNG "add field")<br>

- dari data yang sudah di modeling dan dari proses evaluasi ini menghapus juga data NAN.setalah itu terdapat hasil<br>
  untuk menghitung kesalahan antar peringkat film yang awal dan film yang diprediksi.<br/>
 ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/evaluation.PNG "add field")<br>
 
 - didapati hasil evaluasi dari percobaan seperti berikut<br>
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/hasil_prediksi.PNG "add field")<br>
 

# Deployment

- workflow ini akan mendisplay 10 peringkat prediksi film rekomendasi<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/deploy.PNG " asli csv")<br/>

### konfigurasi node top 20
- tidak lupa menjalankan file reader untuk di join dengan file prediksi<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/deploy_read.PNG " asli csv")<br/>

- jalankan spark predictor dan akan mendapati hasil seperti ini<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/spark_deploy.PNG " asli csv")<br/>

- kemudian jalankan spark to table untu mengubah spark ke dalam table, kemudian masuk ke konfigurasi movies recommended<br>
  dan di dalamnya ada file reader dan joiner, untuk menggabungkan data yang awal dengan data yang telah diprediksi.<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/recom.PNG " asli csv")<br/>

- row filter disini untuk menghapus hasil prediksi yang hasilnya NAN<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/row_predik.PNG " asli csv")<br/>

- dan untuk mengurutkan data hasilnya dipilih ascending untuk nilai kolom prediction<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/asc.PNG " asli csv")<br/>

- row filter dipakai dua kali, untuk row filter terakhir digunakan untuk mengambil best 10 nya, dan outputnya<br>
  disimpan ke direktori ke yang sudah kita pasang menggunakan csv writer.<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/best.PNG " asli csv")<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/excel.PNG " asli csv")<br/>

## hasil deploy
- hasil yang didapati adalah sebagai berikut sesuai dengan arahan untuk memberi best 10 movie<br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/hasil_done.PNG " asli csv")<br/>

# Workflow KNIME
susunan KNIME seperti berikut
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/arsitek.PNG " asli csv")<br/>

# Perbandingan Waktu yang Diperlukan File Reader dan CSV to Spark untuk Membaca File

- untuk melakukan perbandingan antara csv to spark dengan reader, kita harus menambahkan node seperti berikut<br> 
  dan mengarahkan kepada data csv yang sama<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/timer.PNG " asli csv")<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/konfi.PNG " asli csv")<br/>

- perbedaan data sebagai berikut<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/spark_time.PNG " asli csv")<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_3/picture/read_time.PNG " asli csv")<br/>

- dari data diatas sangat jauh perbedaan antara csv to spark dengan file reader, file reader hanya melakukan pengambilan<br/>
  data yang sangat besar dan ketika melakukan eksekusi, komputer hanya melakukan itu  sendiri tanpa bantuan framework<br/>
  computing apapun, tidak seperti spark yang merupakan open source cluster framework, spark itu untuk pemrosesan data<br/>
  yang lebih cepat, karena data yang dipakai juga besar, jadi terdapat perbedaan waktu yang mencolok.<br/>
