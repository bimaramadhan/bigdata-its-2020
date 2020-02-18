# Business Understanding
Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
 - Melihat data yang sering digunakan dalam dialog.
 - Melihat jumlah episode pada tiap season.
 - Melihat kata yang sering digunakan atau muncul dalam tiap episode.
 - Melihat karakter dengan dialog terbanyak di Game of Thrones.
 - Melihat tahun tayang tiap season Game of Thrones.
# Data Understanding
 - Dataset ini adalah file berformat .csv yang berisi seluruh skrip Game of Thrones untuk semua season. Dataset ini memiliki tipe data berbeda yang dapat digunakan untuk berbagai keperluan.    
 -   dataset ini berisi 23911 baris dan mempunyai 6 kolom dengan kolom-kolomnya adalah sebagai berikut :
    - Release Date : Tanggal tayang dari episode ini.
    - Season : Nomor season.
    - Episode : Nomor episode.
    - Episode Title : Judul dari setiap episode.
    - Name : Nama karakter dalam Game of Thrones.
    - Sentence : Kalimat diucapkan dalam seri.
# Data Preparation
- Dataset dipisah menjadi dua bagian menggunakan script seperti yang terlampir di bawah
[link script](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/split_data.ipynb)
- Kemudian setelah dipisah terdapat dua data csv. Salah satu data csv tersebut akan dimasukkan pada database phpmyadmin.
- Sebagai contoh disini dimasukkan data GOT_new1.csv. Convert menjadi sql dengan bantuan converter online [https://www.convertcsv.com/csv-to-sql.htm](https://www.convertcsv.com/csv-to-sql.htm) 
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/convert-csv-to-sql.PNG?raw=true)
- jika sudah berhasil import data GOT_news1.sql pada phpmyadmin.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/import-sql.PNG?raw=true)
- hasil data mysql.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/tabel-sql.PNG?raw=true)

# Modeling
## Proses Membaca dari MySQL
- Untuk membaca data dari mysql, pertama koneksikan dulu dengan menggunakan mysql connector nodes. 
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/mysql-connector.PNG?raw=true)
- Kemudian melakukan konfigurasi dengan MySQL yang sudah disiapkan sebelumnya di atas dan lakukan setting untuk hostname, database name, username dan password dari database.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-sql-connector.PNG?raw=true)
- Menggunakan db table selector untuk memilih database dan tabel yang ingin dikoneksikan.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-table-selector.PNG?raw=true)
- Konfigurasi db table selector dan pilih database dan tabel yang ingin dipilih untuk dikoneksikan.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-sql-selector.PNG?raw=true)
- db reader untuk melihat hasilnya ke dalam tabel Knime.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/db-reader.PNG?raw=true)
- hasil data mysql yang sudah terhubung dan terbaca di tabel Knime.

## Proses Membaca dari CSV
- Untuk membaca data dari CSV dapat langsung menggunakan CSV Reader.
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/csv-reader.PNG?raw=true)
- Kemudian melakukan konfigurasi seperti gambar di bawah dan masukan lokasi input data csvnya
![enter image description here](https://github.com/bimaramadhan/bigdata-its-2020/blob/tugas1/tugas1/gambar/konfigurasi-csv-reader.PNG?raw=true)
- hasil data csv 

## Proses Modeling
- Untuk melakukan proses modeling menggunakan column appender untuk meng-append data dari csv dan database.

- Kemudian melakukan execute pada column appender maka hasil tabel yang sudah diappend akan nampak seperti gambar di bawah.

# Evaluation
Jelaskan apakah hasil join atau append berhasil
# Deployment
Simpan hasil join atau append ke dalam file dan database
