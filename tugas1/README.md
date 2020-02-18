# Business Understanding
Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
 - Mencari kata yang sering digunakan dalam dialog.
 - Melihat jumlah episode pada tiap season.
 - Mencari kata yang sering digunakan atau muncul dalam tiap episode.
 - Melihat karakter dengan dialog terbanyak di Game of Thrones.
 - Melihat tahun tayang tiap season Game of Thrones.
# Data Understanding
 - Dataset ini adalah file berformat CSV yang berisi seluruh skrip Game of Thrones untuk semua season. Dataset ini memiliki tipe data berbeda yang dapat digunakan untuk berbagai keperluan.    
 -  Dataset ini berisi 23911 baris dan mempunyai 6 kolom dengan kolom-kolomnya adalah sebagai berikut :
    - Release Date : Tanggal tayang dari episode ini.
    - Season : Nomor season.
    - Episode : Nomor episode.
    - Episode Title : Judul dari setiap episode.
    - Name : Nama karakter dalam Game of Thrones.
    - Sentence : Kalimat diucapkan dalam seri.
# Data Preparation
- Dataset dipisah menjadi dua bagian menggunakan script seperti yang terlampir di bawah
[link script](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/split_data.ipynb)
- Kemudian setelah dipisah terdapat dua data CSV. Salah satu data CSV tersebut akan dimasukkan pada database phpmyadmin.
- Sebagai contoh disini dimasukkan data GOT_new1.csv. Convert menjadi sql dengan bantuan converter online [https://www.convertcsv.com/csv-to-sql.htm](https://www.convertcsv.com/csv-to-sql.htm) 
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/convert-csv-to-sql.PNG?raw=true)
- jika sudah berhasil import data GOT_news1.sql pada phpmyadmin.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/import-sql.PNG?raw=true)
- Hasil data mysql.
![Alt text](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/tabel-sql.PNG?raw=true)

# Modeling
### Proses Membaca dari MySQL
- Untuk membaca data dari MySQL, pertama koneksikan dulu dengan menggunakan MySQL connector nodes. 
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/mysql-connector.PNG?raw=true)
- Kemudian melakukan konfigurasi dengan MySQL yang sudah disiapkan sebelumnya di atas dan lakukan setting untuk hostname, database name, username dan password dari database.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-sql-connector.PNG?raw=true)
- Menggunakan DB Table Selector untuk memilih database dan tabel yang ingin dikoneksikan.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-table-selector.PNG?raw=true)
- Konfigurasi DB Table Selector dan pilih database dan tabel yang ingin dipilih untuk dikoneksikan.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-sql-selector.PNG?raw=true)
- DB Reader untuk melihat hasilnya ke dalam tabel Knime.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-reader.PNG?raw=true)
- Hasil data MySQL yang sudah terhubung dan terbaca di tabel Knime.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-reader-sql.PNG?raw=true)
### Proses Membaca dari CSV
- Untuk membaca data dari CSV dapat langsung menggunakan CSV Reader.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-reader.PNG?raw=true)
- Kemudian melakukan konfigurasi seperti gambar di bawah dan masukan lokasi input data CSVnya
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-csv-reader.PNG?raw=true)
- Hasil data CSV
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-reader-knime.PNG?raw=true) 

### Proses Modeling
 - Untuk melakukan proses modeling menggunakan Column Appender untuk meng-append data dari csv dan database.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/column-appender.PNG?raw=true)
 - Kemudian melakukan execute pada Column Appender maka hasil tabel yang sudah diappend akan nampak seperti gambar di bawah.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/hasil-append.PNG?raw=true)
# Evaluation
- Untuk evaluasi menggunakan online compare tools yaitu [https://extendsclass.com/csv-diff.html](https://extendsclass.com/csv-diff.html)
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/tampilan-csv-compare.PNG?raw=true)
- Berikut hasilnya saat dimasukkan dataset asli dan data hasil append ketika dibandingkan hasilnya seperti terlihat pada gambar di bawah.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-comparison.PNG?raw=true)
- Apabila nampak perbedaan makan akan terdapat bagian tabel berwarna merah yang mana berarti bagian tersebut adalah berbeda.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/contoh-compare-salah.PNG?raw=true)
# Deployment
### Menyimpan ke Database
 - Menggunakan DB Writer untuk men-deploy ke dalam bentuk Database.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-writer.PNG?raw=true)
 - Kemudian melakukan konfigurasi seperti gambar di bawah ini.
 ![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-db-writer.PNG?raw=true)
 - Berikut hasil deploy Database berhasil dilakukan.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/hasil-db-writer.PNG?raw=true)
### Menyimpan ke CSV
 - Menggunakan CSV Writer untuk men-deploy ke dalam bentuk file CSV.
 ![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-writer.PNG?raw=true)
 - Kemudian melakukan konfigurasi seperti gambar di bawah ini.
 ![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-csv-writer.PNG?raw=true)
 - Terlihat sudah muncul file CSV baru yaitu GOT_append_result.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-writer-file.PNG?raw=true)
- Berikut hasil deploy CSV berhasil dilakukan. 
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/hasil-csv-writer.PNG?raw=true)
# Workflow KNIME
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/workflow-knime.PNG?raw=true)
