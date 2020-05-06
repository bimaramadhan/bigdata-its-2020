# Dokumentasi MLlib model to PMML (KNIME)

# Daftar Isi
- [Business Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#business-understanding)
- [Data Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#data-understanding)
- [Data Preparation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#data-preparation)
- [Modeling](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#modeling)
- [Evaluation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#evaluation)
- [Deployment](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#deployment)
- [Workflow KNIME](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/MLlib%20model%20to%20PMML#workflow-knime)

# Business Understanding
Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
- Klasifikasi spesies bunga iris dengan berbagai algoritma
- Latihan untuk mencoba machine learning
- Data pembelajaran untuk data mining

# Data Understanding

Dataset Iris adalah kumpulan data multivariat yang diperkenalkan oleh ahli statistik dan biolog Inggris Ronald Fisher dalam makalahnya tahun 1936 "The Use of Multiple Measurements in Taxonomic Problems."  Dataset ini adalah salah satu yang paling populer untuk latihan machine learning. Dataset ini isinya tentang 3 macam spesies bunga beserta ukuran petal dan sepal.

<br>![](gambar/dataset.png)<br/>

1. sepal length in cm
2. sepal width in cm
3. petal length in cm
4. petal width in cm
5. class:
    - Iris Setosa
    - Iris Versicolour
    - Iris Virginica

- Sumber : [Iris Dataset](https://archive.ics.uci.edu/ml/datasets/Iris)

# Data Preparation

- Pertama membuat spark context menggunakan node **Create Local Big Data Environment**
<br>![](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas3/gambar/create-local-big-data.PNG?raw=true)<br/>

- Melakukan konfigurasi pada node tersebut
<br>![](gambar/konfig-big-data-environment.PNG)<br/>

- Kemudian disini membangun profil user dengan id misal adalah 999999 untuk menilai 20 film acak
<br>![](gambar/build-current-user-profile.PNG)<br/>
- Melakukan konfigurasi pada node **File Reader** untuk membaca data movies.csv
<br>![](gambar/konfig-file-reader.PNG)<br/>
- Menambahkan node **add fields**. Didalam **add fields** terdapat beberapa proses seperti gambar di bawah ini
<br>![](gambar/add-fields.PNG)<br/>
  - node **Shuffle** untuk mengacak urutan baris pada data
  - melakukan konfigurasi pada node **Constant Value Column** untuk menambahkan kolom timestamp=123 dan userID=999999
  <br>![](gambar/konfig-timestamp.PNG)<br/>
  <br>![](gambar/konfig-userid.PNG)<br/>
- Melakukan konfigurasi pada node **Row Splitter** untuk mengambil 20 film yang akan dinilai oleh user sedangkan film sisanya nanti akan digunakan saat proses **Deployment**
<br>![](gambar/konfig-row-splitter.PNG)<br/>
- Menambahkan node **no rating** yang di dalamnya terdapat beberapa node seperti berikut
<br>![](gambar/no-rating.PNG)<br/>
- Proses pada node tersebut untuk menyiapkan data saat **Deployment** nanti
- Kemudian menambahkan node **Ask User for Movie Ratings** yang mana terdapat beberapa node di dalamnya yang intinya adalah untuk memberikan rating pada 20 film yang sudah diambil
<br>![](gambar/ask-user-rating.PNG)<br/>
- Berikut hasilnya jika kita klik interactive view
<br>![](gambar/interactive-view-movie-rating.PNG)<br/>
- Menambahkan node **Table to Spark** untuk membuat dataframe spark dari data table yang sudah ada rating dari user untuk digunakan saat proses **Training**
<br>![](gambar/table-to-spark-rated.PNG)<br/>
- Proses selanjutnya yaitu membaca file ratings.csv dengan node **CSV to Spark** untuk kemudian digunakan saat proses **Training**
<br>![](gambar/csv-to-spark.PNG)<br/>
- Melakukan konfigurasi pada node **CSV to Spark** untuk membuat dataframe spark dari file ratings.csv
<br>![](gambar/konfig-csv-to-spark.PNG)<br/>
- Melakukan konfigurasi pada node **Spark Partitioning** untuk mempartisi file dan menggunakan 80% untuk **Training** dan 20% untuk **Testing**
<br>![](gambar/konfig-spark-partitioning.PNG)<br/>

# Modeling

- Proses **Modeling** diawali dengan menggabungkan dua data menggunakan node **Spark Concatenate** yaitu data rating dan data film yang sudah diberi rating oleh user dengan konfigurasi training set=80% original movies + 20 movies rated by user
<br>![](gambar/modeling-training.PNG)<br/>
- Lalu Menambahkan node **Spark Collaborative Filtering Learner (MLlib)** dan lakukan konfigurasi untuk training dengan model algoritma ALS 
<br>![](gambar/konfig-spark-collaborative-training.PNG)<br/>

# Evaluation

- Kemudian melakukan **Testing** untuk Proses **Evaluasi** model dengan test set=20% original movies yang didapat dari proses partisi node **Spark Partitioning** 
<br>![](gambar/testing-evaluating.PNG)<br/>
- Melakukan konfigurasi node **Spark Predictor (MLlib)** untuk melakukan prediksi rating pada test set dan meletakkannya pada kolom prediction
<br>![](gambar/konfig-spark-predictor.PNG)<br/>
- Berikut tampilan contoh hasil dari prediksi pada test set
<br>![](gambar/hasil-prediction.PNG)<br/>
- Melakukan konfigurasi pada node **Spark Missing Value** untuk menghapus NaN dan prediksi yang kosong
<br>![](gambar/konfig-spark-missing-value.PNG)<br/>
- Melakukan konfigurasi pada node **Spark Numeric Scorer** menghitung kesalahan numerik antara original ratings dan predicted ratings
<br>![](gambar/konfig-spark-numeric-scorer.PNG)<br/>
- Berikut hasil perhitungan dapat dilihat pada gambar di bawah
<br>![](gambar/hasil-spark-numeric-scorer.PNG)<br/> 

# Deployment

- Terakhir yaitu proses **Deployment** untuk membuat prediksi 20 terbaik film untuk user
<br>![](gambar/deployment.PNG)<br/> 
- Pertama menambahkan node **Table to Spark** untuk membuat dataframe spark dari data film sisa yang tidak diambil dan tidak diberikan rating oleh user pada step **Data Preparation**. Data ini digunakan untuk proses prediksi pada node **Spark Predictor (MLlib)** langkah selanjutnya
<br>![](gambar/table-to-spark-unrated.PNG)<br/> 
- Melakukan konfigurasi node **Spark Predictor (MLlib)** untuk melakukan prediksi rating pada unrated movies dan meletakkannya pada kolom prediction
<br>![](gambar/konfig-spark-predictor.PNG)<br/> 
- Menambahkan node **Spark to Table** untuk memuat data dari dataframe spark ke data table 
- Menambahkan node **Top 20 recommended movies** yang di dalamnya terdapat node-node seperti berikut
<br>![](gambar/top-20.PNG)<br/> 
- Proses pada node-node di atas adalah untuk mengurutkan rekomendasi film berdasarkan rating yang terbaik dan mengekstraknya sebanyak 20 film terbaik
- Menambahkan node **Display Recommendations** yang mana terdapat beberapa node di dalamnya
<br>![](gambar/display-recommendation.PNG)<br/> 
- Fungsi node tersebut adalah untuk menampilkan daftar film yang direkomendasikan pada portal web dan hasilnya adalah seperti berikut
<br>![](gambar/hasil-web.PNG)<br/> 
- Menambahkan node **CSV Writer** dan melakukan konfigurasi untuk menyimpannya dalam bentuk file csv
<br>![](gambar/konfig-csv-write.PNG)<br/> 
- Berikut file telah terbuat
<br>![](gambar/hasil-csv-write.PNG)<br/> 

# Workflow KNIME
![](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas3/gambar/workflow.PNG?raw=true)<br/>
