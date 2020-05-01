# Dokumentasi Create Apache Spark Cluster Menggunakan Docker

## Daftar Isi
- [Tools](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas5#tools)
- [Langkah-langkah](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas5#langkah-langkah)
- [Persiapan](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas5#persiapan)
- [Testing](https://github.com/bimaramadhan/bigdata-its-2020/tree/master/tugas5#testing)


## Tools
Terdapat beberapa tools yang akan digunakan yaitu :
1. Docker Engine, Docker pada perangkat linux
2. Apache Spark, Framework open source yang terutama digunakan untuk analisis Big Data, machine learning, dan real-time processing.

## Persiapan
Terdapat beberapa persiapan yang dilakukan diantaranya :
1. Karena dilakukan pada Docker maka perlu melakukan [Instalasi Docker Engine pada Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
2. Selain itu karena akan digunakan docker image Apache Spark dari Bitnami alangkah baiknya untuk membaca [Dokumentasi Bitnami Spark](https://hub.docker.com/r/bitnami/spark)

## Langkah-langkah
Jika sudah maka dapat dilakukan implementasi berdasarkan pada langkah-langkah pada link berikut : <br>
[Tutorial Membuat Apache Spark Cluster Menggunakan Docker](https://docs.google.com/document/d/1LxGtV1WNKPKeUNwzRNJM7BKapAS1V_7ZWgeG9vwyfPY/edit#)

## Testing
Akan diakukan percobaan dengan parameter-parameter sebagai berikut:
- Jumlah worker: 2, 5
- Jumlah CPU: 2, 4
- Memory: 1G
- Partisi: 100, 1000

Untuk menambahkan worker, memodifikasi jumlah CPU dan memory, dapat dilakukan dengan melakukan modifikasi pada [docker-compose.yml](spark/docker-compose.yml) sesuai dengan parameter yang diinginkan

```
version: '2'

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```
- ### Percobaan 1

![](gambar/docker-image.png)<br/>

- ### Percobaan 2

![](gambar/docker-compose.png)<br/>

- ### Percobaan 3

![](gambar/welcome-conduktor.png)<br/>

- ### Percobaan 4

![](gambar/conduktor-cluster.png)<br/>

- ### Percobaan 5

![](gambar/hasil-akhir-conduktor.png)<br/>
