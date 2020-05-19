# Dokumentasi Analisis Time Series Electricity Production (KNIME)

# Daftar Isi

- [Business Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#business-understanding)
- [Data Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#data-understanding)
- [Data Preparation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#data-preparation)
- [Modeling](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#modeling)
- [Evaluation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#evaluation)
- [Deployment](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#deployment)
- [Workflow KNIME](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugaseas/Electricity%20Production#workflow-knime)

# Business Understanding

Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
- Klasifikasi jumlah produksi 
- Analisa produksi listrik dengan periode waktu tertentu : 
    - Produksi listrik total
    - Produksi listrik tiap tahun
    - Produksi listrik tiap bulan
    - Produksi listrik tiap minggu
    - Produksi listrik berdasarkan hari dalam Seminggu
    - Produksi listrik tiap hari
    - Produksi listrik pada saat weekend dan weekday

# Data Understanding

- Dataset Electricity Production adalah kumpulan data nilai produksi listrik dari tahun 1981 hingga 1990.

- Dataset ini terdiri dari 2 kolom yaitu :
    - Date in string, data tanggal
    - IPG2211A2N in double, nilai data listrik

# Data Preparation

- Pertama yang dilakukan adalah memformat data tanggal pada dataset ini agar nantinya dapat dilakukan proses query di dalam program. Tools yang digunakan adalah Microsoft Excel
<br>![](gambar/convert1.PNG)<br/>
<br>![](gambar/convert2.PNG)<br/>
<br>![](gambar/convert3.PNG)<br/>
- Karena dataset ini juga ini belum memiliki ID, maka perlu ditambahkan juga ID dengan asumsi nilai ID adalah dari 1 sampai 100
<br>![](gambar/dataset.PNG)<br/>
- Berikut workflow pada data preparation
<br>![](gambar/preparation.PNG)<br/>
- Membaca data dengan menggunakan node file reader
<br>![](gambar/node-file-reader.PNG) ![](gambar/konfig-reader.PNG) <br/>
- Karena proses menggunakan spark maka perlu menambahkan node create local big data environment untuk membuat local spark context
<br>![](gambar/node-big-data-env.PNG) ![](gambar/konfig-big-data-env.PNG) <br/>
- Membuat metanode load data untuk load ke data ke dalam hive
<br>![](gambar/node-load-data.PNG) ![](gambar/isi-load-data.PNG) <br/>
    - Membuat tabel database dari file reader yang sudah di load sebelumnya
    <br>![](gambar/node-table-creator.PNG) ![](gambar/konfig-db-table-creator.PNG) <br/>
    - Load tabel database yang sudah dibuat ke dalam hive
    <br>![](gambar/node-db-loader.PNG) ![](gambar/konfig-db-loader.PNG) <br/>

# Modeling

- Berikut workflow pada modeling
<br>![](gambar/modeling.PNG) <br/>
- Mengimpor hasil dari query Hive yang masuk ke Spark sebagai DataFrame/RDD.
<br>![](gambar/node-hive-to-spark.PNG) <br/>
- Metanode extract date-time attributes, metanode ini dilakukan untuk mendapatkan atribut waktu yang spesifik
<br>![](gambar/node-extract-time.PNG) ![](gambar/isi-extract-time.PNG) <br/>
    - Menginisiasi konversi data waktu
    <br>![](gambar/node-spark-sql-query-1.PNG) ![](gambar/konfig-spark-sql-query-1.PNG) ![](gambar/hasil-spark-sql-query-1.PNG) <br/>
    - Mengekstrak fitur data waktu baru
    <br>![](gambar/node-spark-sql-query-2.PNG) ![](gambar/konfig-spark-sql-query-2.PNG) ![](gambar/hasil-spark-sql-query-2.PNG) <br/>
    - Menetapkan atribut waktu weekday dan weekend
    <br>![](gambar/node-spark-sql-query-3.PNG) ![](gambar/konfig-spark-sql-query-3.PNG) ![](gambar/hasil-spark-sql-query-3.PNG) <br/>
- Metanode aggregation and time series, metanode ini bertujuan untuk agregasi data penggunaan listrik berdasarkan waktu
<br>![](gambar/node-agregation-time-series.PNG) ![](gambar/isi-agregation-time-series.PNG)
    #### a. Total Usage
    <br>![](gambar/total.PNG)

    - Mencari nilai Penggunaan Listrik Total menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**-nya. 

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **electricity(sum)** diubah menjadi **total**. 
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-total.PNG)

    #### b. Usage By Year
    <br>![](gambar/year.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik tiap Tahun menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, dan **year**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark GroupBy** untuk mencari nilai rata-ratanya dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id.)

    - Supaya mudah dibedakan maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **mean(sum(electricity))** diubah menjadi **avgYearly**.
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-year.PNG)

    - Selanjutnya melakukan Join untuk nilai Penggunaan Listrik Total dan Rata-rata Penggunaan Listrik per Tahun menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner1.PNG)

    #### c. Usage by Month
    <br>![](gambar/month.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik per Bulan menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, **year**, dan **month**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark GroupBy** untuk mencari nilai rata-ratanya dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id.

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **mean(sum(electricity))** diubah menjadi **avgMonthly**.
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-month.PNG)

    - Kemudian melakukan Join untuk Rata-rata Penggunaan Listrik per Bulan dengan hasil join sebelumnya menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner2.PNG)

    #### d. Usage by Week
    <br>![](gambar/week.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik per Minggu menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, **year**, dan **week**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark GroupBy** untuk mencari nilai rata-ratanya dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id.

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **mean(sum(electricity))** diubah menjadi **avgWeekly**.
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-wekk.PNG)

    - Kemudian melakukan Join untuk Rata-rata Penggunaan Listrik per Minggu dengan hasil join sebelumnya menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner3.PNG)

    #### e. Usage by Day of Week
    <br>![](gambar/dayweek.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik berdasarkan hari dalam Seminggu menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, **year**, **week**, dan **dayOfWeek**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark Pivot** untuk mencari nilai rata-rata pada setiap pivot-nya (**dayOfWeek**) dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id dan pilih pivot column **dayOfWeek**.

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **[Hari] + mean(sum(electricity))** diubah menjadi **avg[Hari]**.
    
    - Berikut hasilnya 
    <br>![](gambar/hasil-column-rename-dayweek.PNG)

    - Kemudian melakukan Join untuk Rata-rata Penggunaan Listrik berdasarkan hari dalam Seminggu dengan hasil join sebelumnya menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner4.PNG)

    #### f. Usage by Day
    <br>![](gambar/day.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik per Hari menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, dan **eventDate**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark GroupBy** untuk mencari nilai rata-ratanya dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id.

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **mean(sum(electricity))** diubah menjadi **avgDaily**.
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-day.PNG)

    - Kemudian melakukan Join untuk Rata-rata Penggunaan Listrik per Hari dengan hasil join sebelumnya menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner5.PNG)

    #### g. Usage by Day Classifier
    <br>![](gambar/dayclassifier.PNG)

    - Mencari nilai Rata-rata Penggunaan Listrik per Hari menggunakan node **Spark GroupBy** dengan melakukan penjumlahan **(SUM)** pada kolom **electricity**, lalu di Group By berdasarkan **Id**, **year**, **month**, **week**, dan **dayClassifier**-nya. 

    - Hasilnya kemudian akan di proses ke node **Spark Pivot** untuk mencari nilai rata-rata pada setiap pivot-nya (**dayClassifier**) dengan melakukan agregasi Average (AVG) pada kolom sum(electricity) lalu di GroupBy berdasarkan Id dan pilih pivot column **dayClassifier**.

    - Supaya mudah dibedakan, maka perlu diubah nama kolomnya menggunakan node **Spark Column Rename** untuk mengubah nama kolom yang semula **[dayClassifier] + mean(sum(electricity))** diubah menjadi **avg[dayClassifier]**.
    
    - Berikut hasilnya
    <br>![](gambar/hasil-column-rename-dayclassifier.PNG)

    - Kemudian melakukan Join untuk Rata-rata Penggunaan Listrik pada saat Weekend dan Weekday dengan hasil join sebelumnya menggunakan node **Spark Joiner**.

    - Berikut hasilnya
    <br>![](gambar/hasil-spark-joiner6.PNG)

# Evaluation

- Berikut workflow pada evaluation
<br>![](gambar/evaluation.PNG) <br/>
- Menghitung presentase dari penggunaan listrik berdasarkan agregasi data dan segmentasi yang telah dilakukan sebelumnya
<br>![](gambar/node-spark-sql-query.PNG) ![](gambar/konfig-spark-sql-query.PNG) <br/>
- Metanode PCA, kmeans, dan scatterplot bertujuan untuk mengelompokkan dan memvisualisasikan hasil perhitungan presentase agregasi data
<br>![](gambar/node-pca.PNG) ![](gambar/isi-pca.PNG) <br/>
    - Menormalisasikan data agregasi
    <br>![](gambar/node-spark-normalizer.PNG) ![](gambar/konfig-spark-normalizer.PNG) <br/>
    - Melakukan principal component analysis dari 96% data untuk memilih 96% data yang tidak direduksi
    <br>![](gambar/node-spark-pca.PNG) ![](gambar/konfig-spark-pca.PNG) <br/>
    - Clustering dengan algoritma kmeans
    <br>![](gambar/node-spark-kmeans.PNG) ![](gambar/konfig-spark-kmeans.PNG) <br/>
    Berikut hasil clustering
    <br>![](gambar/hasil-spark-kmeans.PNG) <br/>
    - Memfilter dan tetap menyimpan Id dan label cluster
    <br>![](gambar/node-spark-column-filter.PNG) ![](gambar/konfig-spark-column-filter.PNG) <br/>
    - Menggabungkan hasil principal component analysis dengan label cluster 
    <br>![](gambar/node-spark-joiner.PNG) ![](gambar/konfig-spark-joiner.PNG) <br/>
    - Mengubah format menjadi tabel untuk visualisasi
    <br>![](gambar/node-spark-to-table.PNG) ![](gambar/konfig-spark-to-table.PNG) <br/>
    - Mendenormalisasikan data dengan model pmml
    <br>![](gambar/node-denormalizer.PNG) <br/>
    - Mengubah format nomor cluster ke string agar lebih jelas untuk warna visualisasi
    <br>![](gambar/node-number-t-string.PNG) ![](gambar/konfig-number-t-string.PNG) <br/>
    - Menetapkan warna untuk cluster
    <br>![](gambar/node-color-manager.PNG) ![](gambar/konfig-color-manager.PNG) <br/>
    - Menampilkan hasil cluster dengan metode scatter plot
    <br>![](gambar/node-scatter-plot.PNG) ![](gambar/konfig-scatter-plot.PNG) <br/>
    - Berikut hasilnya
    <br>![](gambar/hasil-scatter-plot.PNG)<br/>
    - Menampilkan hasil cluster dengan tabel view
    <br>![](gambar/node-table-view.PNG) ![](gambar/konfig-table-view.PNG) <br/>
    - Berikut Hasilnya
    <br>![](gambar/hasil-table-view.PNG) <br/>
    - Membuat spark dataframe/rdd dari tabel data untuk dilanjutkan pada deployment
    <br>![](gambar/node-table-to-spark.PNG) <br/>
    - Menghapus spasi dari nama kolom untuk ekspor tabel hive
    <br>![](gambar/node-spark-column-rename.PNG) ![](gambar/konfig-spark-column-rename.PNG) <br/>

# Deployment
- Berikut workflow pada deployment
<br>![](gambar/deployment.PNG)<br/>
- Melakukan deploy hasil agregasi data keseluruhan pada tabel hive
<br>![](gambar/node-spark-to-hive.PNG) ![](gambar/konfig-spark-to-hive.PNG) <br/>
- Hasilnya dapat dilihat dengan menggunakan tools dbheaver seperti berikut
<br>![](gambar/hasil-spark-to-hive.PNG) <br/>
- Melakukan deploy hasil agregasi data keseluruhan pada hdfs dengan format paquet
<br>![](gambar/node-spark-to-parquet.PNG) ![](gambar/konfig-spark-to-parquet.PNG) <br/>
- Berikut hasilnya 
<br>![](gambar/hasil-spark-to-parquet.PNG) <br/>

# Workflow KNIME
![](gambar/workflow.PNG)<br/>
