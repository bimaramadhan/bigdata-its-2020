# Dokumentasi Spark Compiled Model Predictor (KNIME)

# Daftar Isi
- [Business Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#business-understanding)
- [Data Understanding](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#data-understanding)
- [Data Preparation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#data-preparation)
- [Modeling](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#modeling)
- [Evaluation](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#evaluation)
- [Deployment](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#deployment)
- [Workflow KNIME](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas6/Spark%20Compiled%20Model%20Predictor#workflow-knime)

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

- Pertama membaca file dataset iris dengan node **File Reader**  
<br>![](gambar/node-preparation.PNG)<br/>
- Melakukan konfigurasi pada node tersebut
<br>![](gambar/konfig-reader-train.PNG)<br/>
- Kemudian menambahkan node **Decision Tree Learner** dan lakukan konfigurasi
<br>![](gambar/konfig-decision-tree-learner.PNG)<br/>
- Kemudian menambahkan node **RProp MLP Learner** dan lakukan konfigurasi
<br>![](gambar/konfig-rprop-mlp-learner.PNG)<br/>
- Hubungkan kedua node learner tersebut dengan node **PMML to Cell** untuk mengubah pmml port menjadi tabel yang berisi pmml cell

- Melakukan konfigurasi pada node tersebut dengan memberikan row identifier sebagai row0
<br>![](gambar/konfig-pmml-to-cell.PNG)<br/>

# Modeling

- Menggabungkan model dengan dua learner yang berbeda dengan node **Concatenate** 
<br>![](gambar/node-modeling.PNG)<br/>
- Melakukan konfigurasi pada node tersebut 
<br>![](gambar/konfig-concatenate.PNG)<br/>
- Menambahkan node **Table to PMML Ensemble** untuk menggabungkan tabel dokumen pmml menjadi satu dokumen pmml dengan model mining
<br>![](gambar/kofig-table-to-pmml-ensemble.PNG)<br/>
- Menambahkan node **PMML Compiler** untuk menerjemahkan model pmml ke java bytecode agar bisa dijalankan oleh node **Compiled Model Predictor** nantinya
<br>![](gambar/pmml-compiler.PNG)<br/>

# Evaluation

- Kemudian pertama membaca file dataset iris yang sudah disiapkan untuk testing
<br>![](gambar/node-evaluation.PNG)<br/>
- Melakukan konfigurasi pada node tersebut
<br>![](gambar/konfig-reader-test.PNG)<br/>
- Lalu membuat spark context menggunakan node **reate Local Big Data Environment** dan lakukan konfigurasi
<br>![](gambar/konfig-big-data.PNG)<br/>
- Menambahkan node **Table to Spark** untuk membuat spark dataframe dari tabel data

- Menambahkan node **Compiled Model Predictor** dan lakukan konfigurasi dan mengubah kolom prediksi seperti gambar di bawah
<br>![](gambar/konfig-spark-compiled-model-predictor.PNG)<br/>
- Menambahkan node **Spark to Table** untuk memuat data dari spark dataframe menjadi sebuah tabel data 
<br>![](gambar/konfig-spark-to-table.PNG)<br/>
- Menambahkan node **Scorer** untuk melakukan perhitungan
<br>![](gambar/hasil-scorer.PNG)<br/> 
- Berikut hasil perhitungan scoring yang dilakukan
<br>![](gambar/hasil-scorer.PNG)<br/> 

# Deployment

- Menambahkan node **CSV Writer** untuk deploy output dalam bentuk csv
<br>![](gambar/node-write.PNG)<br/> 
- Berikut hasilnya
<br>![](gambar/hasil-write-csv.PNG)<br/> 

# Workflow KNIME
![](gambar/workflow.PNG)<br/>
