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
- Menampilkan hasil dengan **DB Reader* <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/hasil_cownotnull.PNG?raw=true)

 #### Filters  all rows from ss13pme  where COW is NULL
- untuk pemakaian node sama seperti ss13pme is not null yaitu **DB Row Filter** dan **DB Reader**, yang berbeda hanya di configuration<br> 
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/filter_cow_null.PNG?raw=true)
- Configuration ketika di **DB Row Filter** <br/>
![alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/master/tugas2/gambar/2_DB_InDB_Processing/config_filter_cownull.PNG?raw=true)
- Menampilkan hasil dengan **DB Reader* <br/>
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

- memasang node sql connector <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/exercise_2_sql_connector.PNG "sql table")
- memasang node table selector agar dapat memilih table 5116100133_ss13pme <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/memilih_table.PNG "choose table")
- memilih configuration pada node table selector  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/choose_exercise_2.PNG "conf choose table")
- untuk meremove beberapa coloumn puma* dan pwgtp*  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_coloumn_filter.PNG "conf choose table")
- konfigurasi untuk menghapus coloumn puma* dan pwgtp*  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/filter_conf.PNG "conf choose 2 table")

##### memilih data dari 5116100133_ss13pme is null
- memilih node db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_row_filter.PNG "sql table")
- memilih cow is null dalam node db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/conf_exer2.PNG "sql table")
- menampilkan hasil dengan db reader <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_read.PNG "read table")
- hasil dari db reader <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/cow_null.PNG "read cow table")
- memilih node number to string <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/number_string.PNG "sql table")
- mengkonfigurasi sesuai soal <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/config_string.PNG "sql table")
- memilih node decision tree learner <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/node_decision_tree.PNG "read table")
- konfigurasi perhitungan bisa menggunakan gain ratio dan gini index pada konfigurasi, tetapi jangan lupa untuk memilih class yang akan di setting <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/config_string.PNG "read cow table")
- tampilan view tree <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/view_tree.PNG "read table")

##### memilih data dari 5116100133_ss13pme is not null
- untuk pemakaian node sama seperti ss13pme is null, yang berbeda hanya di configuration, configuration ketika di db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/cow_is_not_null.PNG "sql table")
- untuk setting hasil yang didapati dari db reader seperti berikut <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/result_not_null.PNG "sql table")

### hasil
- memilih node decision tree predictor, dan disambungkan dengan data cow is null dan data cow is not null yang telah diolah <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/node_predict.PNG "read table")
- hasil train <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/predict.PNG "read cow table")

### 04_DB_WritingToDB

- memasang node sql connector <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/exercise_2_sql_connector.PNG "sql table")
- memasang node table selector agar dapat memilih table 5116100133_ss13pme <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/memilih_table.PNG "choose table")
- memilih configuration pada node table selector  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/choose_exercise_2.PNG "conf choose table")
- memilih node db connection untuk menyimpan original table  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_connection.PNG "conf choose table")
- untuk meremove beberapa coloumn puma* dan pwgtp*  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_coloumn_filter.PNG "conf choose table")
- konfigurasi untuk menghapus coloumn puma* dan pwgtp*  <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/filter_conf.PNG "conf choose 2 table")

##### memilih data dari 5116100133_ss13pme is null
- memilih node db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_row_filter.PNG "sql table")
- memilih cow is null dalam node db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/conf_exer2.PNG "sql table")
- menampilkan hasil dengan db reader <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_read.PNG "read table")
- hasil dari db reader <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/cow_null.PNG "read cow table")
- memilih node number to string <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/number_string.PNG "sql table")
- mengkonfigurasi sesuai soal <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/config_string.PNG "sql table")
- memilih node decision tree learner <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/node_decision_tree.PNG "read table")
- konfigurasi perhitungan bisa menggunakan gain ratio dan gini index pada konfigurasi, tetapi jangan lupa untuk memilih class yang akan di setting <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/config_string.PNG "read cow table")
- tampilan view tree <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/view_tree.PNG "read table")

##### memilih data dari 5116100133_ss13pme is not null
- untuk pemakaian node sama seperti ss13pme is null, yang berbeda hanya di configuration, configuration ketika di db row filter <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/cow_is_not_null.PNG "sql table")
- untuk setting hasil yang didapati dari db reader seperti berikut <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/result_not_null.PNG "sql table")

### hasil
- memilih node decision tree predictor, dan disambungkan dengan data cow is null dan data cow is not null yang telah diolah <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/node_predict.PNG "read table")
- hasil tree train yang disambungkan ke db update <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/predict.PNG "read cow table")
- db update untuk melakukan update untuk mengisi kolom serial no berdasarkan kolom cow yang sudah diprediksi<br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_update_node.PNG "read table")
- hasil db update <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/db_update.PNG "read cow table")

# Hadoop Exercise
### 00_Setup_Hive_Table

dengan arsitektur ini kita menggunakan local big data environment untuk dapat disambungkan kepada hive serta dapat merename table menjadi format 5116100133..., dan pastikan workflow berjalan semua
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/hive_setup.PNG "read cow table")

- untuk perename an nama dilakukan pada node db table creator
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/rename_hadoop.PNG "read cow table")
- kemudian menyambungkan hive dengan local env big data pada knime dengan mencocokan
``jdbc:hive2://localhost:62895``
- untuk pengecekan dapat menjalankan syntax ini pada dbeaver ``SELECT * FROM 5116100133_ss13hme ``
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/ss13hme_133.PNG "read cow table")
- untuk pengecekan dapat menjalankan syntax ini pada dbeaver ``SELECT * FROM 5116100133_ss13pme ``
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/5116133_pme.PNG "read cow table")

### 01_Hive_Modelling
- untuk arsitektur nya dan fungsi node nya sama, tapi untuk menyambungkan kepada hive . node sqlite connection harus diganti dengan local big data environment yang sudah disesuaikan JDBC NYA `` Connection: URL="jdbc:hive2://localhost:62895/"``
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/hive_01.PNG "read cow table")
- ketika berhasil table selector akan menampilkan seperti ini, pastikan semua node berjalan
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/hive_01.PNG "read cow table")

### 02_Hive_WritingtoDB
- untuk bagian ini mempersiapkan untuk di arahkan kepada hive, table creator akan buat dengan nama baru dan db loader akan mengkonfigurasi
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/hive_02.PNG "read cow table")
- konfigurasi table kreator
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/konf_hive.PNG "read cow table")
- konfigurasi db loader
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/load_hive.PNG "read cow table")
- menjalankan syntax di dbeaver hive dengan syntax ``SELECT * FROM 5116100133_newtable  ``
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_2/picture/syntax_hive_02.PNG "read cow table")


