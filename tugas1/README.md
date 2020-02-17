# Business Understanding
Kemungkinan proses yang dapat dilakukan pada dataset ini antara lain :
 1. Kata yang sering digunakan dalam dialog
 2. Jumlah episode pada tiap season
 3. Kata yang sering digunakan dalam tiap episode
 4. Karakter dengan dialog terbanyak di Game of Thrones
 5. Tahun tayang tiap season Game of Thrones
# Data Understanding
- Dataset ini adalah file berformat .csv yang berisi seluruh skrip Game of Thrones untuk semua season. Dataset ini memiliki tipe data berbeda yang dapat digunakan untuk berbagai keperluan.    
- Dataset ini berisi 23911 baris dan mempunyai 6 kolom dengan kolom-kolomnya adalah sebagai berikut :
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
- sebagai contoh disini dimasukkan data GOT_new1.csv. Convert menjadi sql dengan bantuan converter online [https://www.convertcsv.com/csv-to-sql.htm](https://www.convertcsv.com/csv-to-sql.htm) 
- jika sudah berhasil import data GOT_news1.sql pada phpmyadmin.
- hasil data mysql.
# Modeling
## Proses Membaca dari MySQL
- Untuk membaca data dari mysql, pertama koneksikan dulu dengan menggunakan mysql connector nodes.
- Kemudian melakukan konfigurasi dengan MySQL yang sudah disiapkan sebelumnya di atas.
- konfigurasi db table selector untuk mengoneksikan database dan tabel yang ingin diambil.
- db reader untuk melihat hasilnya ke dalam tabel Knime.
- hasil data mysql yang sudah terhubung dan terbaca di tabel Knime.
## Proses Membaca dari CSV
- Untuk membaca data dari CSV dapat langsung menggunakan CSV Reader.
- Kemudian melakukan konfigurasi seperti gambar di bawah dan masukan lokasi input data csvnya
- hasil data csv 
## Proses Modeling
- Untuk melakukan proses modeling menggunakan joiner.
- Kemudian melakukan konfigurasi pada joiner seperti gambar di bawah.
- hasil tabel yang sudah diappend
# Evaluation
Jelaskan apakah hasil join atau append berhasil
# Deployment
Simpan hasil join atau append ke dalam file dan database
