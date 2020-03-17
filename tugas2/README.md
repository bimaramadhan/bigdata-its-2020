## Bigdata 2020

# KNIME Big Data

* [Exercise DB](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#Exercise_DB)<br/>
  - [exercise DB Connect](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#01_db_connect)<br/>
  - [exercise DB processing exercise](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#02_DB_InDB_Processing)<br/>
  - [exercise DB modelling exercise](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#03_DB_Modelling)<br/>
  - [exercise DB Writing To DB](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#04_DB_WritingToDB)<br/>
* [Hadoop](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#Hadoop-Exercise)<br/>
  - [exercise Setup Hive](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#00_Setup_Hive_Table)<br/>
  - [exercise Hive Modelling](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#01_Hive_Modelling)<br/>
  - [exercise Hive Writing to DB](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/README.md#02_Hive_WritingtoDB)<br/>

# Exercise DB
### 01_DB_Connect
- Mengubah nama table dilakukan melalui DBeaver<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/rename_table.PNG?raw=true)
- Berikut hasil nama-nama tabel yang telah direname<br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/list_rename_table.PNG?raw=true)
- Menambahkan node **SQLite Connector** untuk menyambungkan dengan database sqlite yang diinginkan<br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/sqlite_connector.PNG?raw=true)
- Menambahkan node **DB Table Selector** untuk melakukan seleksi pada table yang ingin dipakai<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/db_table_selector.PNG?raw=true)
- Melakukan konfigurasi <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/config_table_selector.PNG?raw=true)
- Menambahkan node **DB Reader** untuk membaca data<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/db_reader.PNG?raw=true)
- Hasil data yang terbaca<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/hasil_db_reader.PNG?raw=true)
- Tampilan Workflow KNIME <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/1_DB_Connect/workflow_1_DB_Connect.PNG?raw=true)

### 02_DB_InDB_Processing
- Memasang node **SQLite Connector** untuk menyambungkan dengan database sqlite yang diinginkan<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/sqlite_connector.PNG?raw=true)
- Memasang node **DB Table Selector** agar dapat memilih tabel 05111740000081_ss13pme dan 05111740000081_ss13hme  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/db_table_selector.PNG?raw=true)
- Melakukan configuration pada node **DB Table Selector**<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_select_ss13hme.PNG?raw=true)<br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_select_ss13pme.PNG?raw=true)
 
 #### Joins ss13hme and ss13pme on SERIALNO
- Memasang node **DB Joiner** untuk menggabungkan dua tabel <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/joiner.PNG?raw=true)
- Melakukan konfigurasi untuk menggabungkan berdasarkan serialno  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_joiner.PNG?raw=true)
- Memasang **DB Reader** untuk membaca hasil join  <br/>
- Berikut hasilnya  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_join.PNG?raw=true)
 
 #### Filters all rows from ss13pme where COW is NOT NULL 
- Memasang **DB Column Filter** untuk menghapus kolom puma* dan pwgtp*  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/column_filter.PNG?raw=true)
- Melakukan konfigurasi untuk menghapus kolom puma* dan pwgtp*  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_column_filter.PNG?raw=true)
- Memilih node **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/filter_cow_not_null.PNG?raw=true)
- Melakukan konfigurasi dan memilih cow is not null dalam node **DB Row Filter**<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_row_filter_cownotnull.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_cownotnull.PNG?raw=true)

 #### Filters  all rows from ss13pme where COW is NULL
- untuk pemakaian node sama seperti ss13pme is not null yaitu **DB Row Filter** dan **DB Reader**, yang berbeda hanya di configuration<br> 
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/filter_cow_null.PNG?raw=true)
- Configuration ketika di **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_filter_cownull.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_cownull.PNG?raw=true)

 #### Calculate average AGEP for the different SEX groups
- Memilih node **DB Groupby** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/groupby_average.PNG?raw=true)
- Melakukan konfigurasi berdasar grup sex <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_groupby.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_average_sex.PNG?raw=true)

 #### Optional. Sort the data rows by descending AGEP and extract top 10 only..
- Memasang node **DB Sorter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/sort_data.PNG?raw=true)
- Melakukan konfigurasi pada node **DB Sorter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_dbsorter.PNG?raw=true)
- Memasang node **DB Query** <br/>
- Pada **DB Query** menjalankan syntax ini agar membatasi hanya menampilkan sebanyak 10<br/>
``` SELECT * FROM #table# AS "table" limit 10 ```
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_db_query.PNG?raw=true)
- Menampilkan hasil dengan db reader <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_sorter.PNG?raw=true)

#### Tampilan Workflow
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/workflow.PNG?raw=true)

### 03_DB_Modelling
- Memasang node **SQLite Connector** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/connect_select_filter.PNG?raw=true)
- Memasang node **DB Table Selector** agar dapat memilih tabel 05111740000081_ss13pme <br/>
- Melakukan konfigurasi pada node **DB Table Selector**  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_select_ss13pme.PNG?raw=true)
- Memasang **DB Column Filter** untuk menghapus kolom puma* dan pwgtp* <br/>
- Melakukan konfigurasi untuk menghapus kolom puma* dan pwgtp*  <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_column_filter.PNG?raw=true)

#### Memilih data dari 05111740000081_ss13pme dimana Cow is not NULL
- Memasang node **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/cow_not_null.PNG?raw=true)
- Memilih cow is null dalam node **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_row_filter_cownotnull.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/hasil_db_cownotnull.PNG?raw=true)
- Memasang node **Number To String** <br/>
- Melakukan konfigurasi pada node **Number To String**<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_number_string.PNG?raw=true)
- Memasang node **Decision Tree Learner** <br/>
- Melakukan konfigurasi perhitungan bisa menggunakan gain ratio dan gini index pada node **Decision Tree Learner**<br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_dec_tree_learner.PNG?raw=true)
- Tampilan decision tree <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/hasil_dec_tree_learner.PNG?raw=true)

#### Memilih data dari 05111740000081_ss13pme dimana Cow is NULL
- Memasang node **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/cow_null.PNG?raw=true)
- Memilih cow is null dalam node **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_filter_cownull.PNG?raw=true)
- Memasang node **DB Column Filter** untuk menghapus kolom Cow
- Melakukan konfigurasi pada node **DB Column Filter** 
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_column_filter_rmcow.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/hasil_db_cownull.PNG?raw=true)

#### Hasil
- Memasang node **Decision Tree Predictor**, dan disambungkan dengan data cow is null dan data cow is not null yang telah diolah <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/decision_tree_predictor.PNG?raw=true)
- Melakukan konfigurasi pada node **Decision Tree Predictor**
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/config_dec_tree_predictor.PNG?raw=true)
- Tampilan decision tree hasil train <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/hasil_dec_tree_predictor.PNG?raw=true)

#### Tampilan Workflow
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/3_DB_Modelling/workflow.PNG?raw=true)

### 04_DB_WritingToDB
- Disini tinggal melanjutkan workflow sebelumnya di atas dan menambahkan beberapa node untuk melakukan perintah Write
#### Writes original table to ss13pme_original table with a Database Connection Table Writer node ... just in case we mess up with the updates
- Memasang node **DB Connection Table Writer** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_reader_original.PNG?raw=true)
- Melakukan konfigurasi pada **DB Connection Table Writer** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/config_db_connection_table.PNG?raw=true)
- Memasang node **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_reader_original.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/hasil_tabel_original.PNG?raw=true)
#### Writes model and timestamp with a Database Writer node
- Memasang node **Timestamp and Model** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_writer_timestamp.PNG?raw=true)
- Memasang node **DB Writer** <br>
- Melakukan konfigurasi pada **DB Writer** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/config_db_writer_timestamp.PNG?raw=true)
- Memasang node **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_reader_timestamp.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/hasil_tabel_timestamp.PNG?raw=true)
#### Writes COW prediction where COW value is missing through a Database Update node
- Memasang node **DB Update** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_update.PNG?raw=true)
- Melakukan konfigurasi pada **DB Update** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/config_db_update.PNG?raw=true)
- Memasang node **Row Filter** untuk mengecek update status
- Melakukan konfigurasi pada node **Row Filter** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/config_update_status.PNG?raw=true)
- Memasang node **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/db_reader_db_update.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader** <br>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/hasil_tabel_update.PNG?raw=true)

#### Tampilan Workflow
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/4_DB_WritingToDB/workflow.PNG?raw=true)

# Hadoop Exercise
### 00_Setup_Hive_Table

Dengan arsitektur ini kita menggunakan node **Local Big Data Environment** untuk dapat disambungkan kepada hive serta dapat merename table menjadi format 05111740000081..., dan pastikan workflow berjalan semua
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/5_Setup_Hive_Table/workflow.PNG?raw=true)

- Untuk mengganti nama dilakukan pada node **DB Table Creator**
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/5_Setup_Hive_Table/rename_nama_tabel.PNG?raw=true)
- Kemudian menyambungkan hive dengan local environment big data pada knime dengan mencocokkan url jdbc
``jdbc:hive2://localhost:60356``
- Untuk pengecekan dapat menjalankan syntax ini pada dbeaver ``SELECT * FROM 05111740000081_ss13hme ``
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/5_Setup_Hive_Table/dbeaver_ss13hme.PNG?raw=true)
- untuk pengecekan dapat menjalankan syntax ini pada dbeaver ``SELECT * FROM 05111740000081_ss13pme ``
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/5_Setup_Hive_Table/dbeaver_ss13pme.PNG?raw=true)

### 01_Hive_Modelling
- Untuk arsitekturnya dan fungsi node nya sama dengan **DB_Modelling** di atas, tapi untuk menyambungkan kepada hive node **SQLite Connection** harus diganti dengan **Local Big Data Environment** yang sudah disesuaikan url jdbcnya contoh seperti berikut ini ``jdbc:hive2://localhost:60356``
- Ketika berhasil kemudian setelah itu workflow modelling kurang lebih mirip seperti **DB_Modelling** di atas
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/6_Hive_Modelling/workflow.PNG?raw=true)

### 02_Hive_WritingtoDB
- Untuk bagian ini melanjutkan modelling yang sudah dilakukan di atas. Kemudian mempersiapkan untuk di arahkan kepada hive, node **DB Table Creator** akan membuat tabel dengan nama baru dan node **DB Loader** akan mengkonfigurasi
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/7_Hive_WritingToDB/workflow.PNG?raw=true)
- Melakukan konfigurasi node **DB Table Creator**
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/7_Hive_WritingToDB/rename_tabel.PNG?raw=true)
- Melakukan konfigurasi node **DB Loader**
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/7_Hive_WritingToDB/config_dbloader.PNG?raw=true)
- Menjalankan syntax di dbeaver hive dengan syntax ``SELECT * FROM 05111740000081_newtable``
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/7_Hive_WritingToDB/dbeaver_newtable.PNG?raw=true)


