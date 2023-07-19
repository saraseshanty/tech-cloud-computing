Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 11
Saras Eshanty
225611025
Materi
Bagian ini menjelaskan tentang Docker Compose untuk App Containerization and Microservice Orchestration
Application Containerization

Application Containerization and Microservice Orchestration
Tujuan
Mahasiswa mampu memahami perintah dasar Docker dan Alur Kerja Docker Build dan Run dan menjalankan berbagai komponen aplikasi sebagai layanan mikro.
Mahasiswa mampu menggunakan docker compose dalam pengembangan.
Mahasiswa mampu memahami JSON Cache Redis yang digunakan dalam API untuk menghindari penumpukan berulang.
Pembahasan
Langkah - langkah Praktikum

Stage Setup

Kita mulai dengan meng-kloning demo kode dari repository git.

$ git clone https://github.com/ibnesayeed/linkextractor.git

$ cd linkextractor

$ git checkout demo
1.jpg

Step 0: Basic Link Extractor Script
cek isi data step0

$ git checkout step0

$ tree
2.jpg

melihat isi dari file linkextractor.py

$ cat linkextractor.py
3.jpg

Kita coba menjalankan script diatas

$ ./linkextractor.py http://example.com/
4.jpg

maka hasilnya error akses ditolak

kita cek file linkextractor.py

$ ls -l linkextractor.py
5.jpg

kita rubah permission menggunakan perintah

$ chmod a+x linkextractor.py
5.jpg

Run Python

$ python3 linkextractor.py
6.jpg

Step 1: Containerized Link Extractor Script
cek isi data step1

$ git checkout step1

$ tree
7.jpg

Cat Dockerfile

$ cat Dockerfile
8.jpg

kita perlu menambahkan dua paket install pip beautifulsoup4 dan requests agar skrip dalam dockerfile dapat berfungsi. Seblumnya pada mesin saya install py3_pip terlebih dahulu.

$ sudo apt install python3-pip
9.jpg

9.2.jpg

9.3.jpg

selanjutnya kita install beautifulsoup4

$ pip install beautifulsoup4
10.jpg

selanjutnya kita install pip requests (sudah tersedia di paket py3)

$ pip install requests
11.jpg

selanjutnya kita membangun Docker Image dengan perintah dibawah ini

$ docker image build -t linkextractor:step1 .
12.jpg

menampilkan Docker Image dengan nama linsextractor:step1

$ docker image ls
13.jpg

selanjutnya menjalankan satu container linkextractor:step1

$ docker container run -it --rm linkextractor:step1 http://example.com/
menghasilkan tautan seperti dibawah ini :

14.jpg

14.jpg

selanjutnya mencoba lebih banyak link didalamnya dengan perintah

$ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
15.jpg

sebelum kita checkout step2 kita lakukan comit menggunakan perintah

$ git stash
Step 2: Link Extractor Module with Full URL and Anchor Text
disini kita akan mencoba lebih banyak lagi, kita checkout step2

$ git checkout step2
$ tree
16.jpg

selanjutnya kita melihat skirp yang sudah update dari step2 ini

$ cat linkextractor.py
17.jpg

sekarang kita akan mencoba membangun docker image pada step2

$ docker image build -t linkextractor:step2 .
18.jpg

$ docker image ls
19.jpg

selanjutnya kita mencoba menjalankan container pada image step2 dengan perintah dibawah

$ docker container run -it --rm linkextractor:step2 https://training.play-with-docker.com/
20.jpg

kita juga mencoba untuk menjalankan container step1

$ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
21.jpg

Sampai dengan langkah kedua ini kita telah belajar dan mempelajari pengemasan script menggunakan dependensi yang dibutuhkan dengan lebih fleksibel, kita mempelajari membuat perubahan dalam aplikasi dan membuat berbagai varian docker image yang berada dalam satu wadah.

Step 3: Link Extractor API Service
Pada langkah ini kita akan mencoba membangun dan menjalankan layanan web menggunakan script ini dalam docker.

$ git checkout step3
$ tree
22.jpg

Selanjutnya kita masuk dockerfile dengan perintah

$ cat Dockerfile
23.jpg

kita lihat isi main.py

$ cat main.py
24.jpg

selanjutnya kita build image dan jalankan docker container :

$ docker image build -t linkextractor:step3 .

$ docker container run -d -p 5000:5000 --name=linkextractor linkextractor:step3

$ docker container ls
25.jpg

Selanjutnya membuat request HTTP dalam bentuk url

$ curl -i http://localhost:5000/api/http://example.com/
26.jpg

setelah servis API berjalan dan mendapatkan respon JSON berupa Link url seperti pada gambar.

kita dapat melihat log menggunakan perintah :

$ docker container logs linkextractor
27.jpg

kita mematikan dan menghapus container log setelah ditampilkan menggunakan perintah dibawah :

$ docker container rm -f linkextractor
Step 4: Link Extractor API and Web Front End Services

Langkah selanjut membuat layanan GUI

kita checkout dulu file step4

$ git checkout step4
$ tree
28.jpg

selanjutnya kita lihat file docker-compose.yml

$ cat docker-compose.yml
29.jpg

kita lihat isi file index.php

$ cat www/index.php
30.jpg

selanjut kita jalankan docker compose

$ docker-compose up -d --build
31.jpg

pastikan bahwa keduanya layanan berjalan docker container

$ docker container ls
32.jpg

selanjutnya kita test service API

reloading

$ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php

$ git reset --hard

$ docker-compose down
33.jpg

32.jpg

Step 5: Redis Service for Caching

$ git checkout step5
$ tree
34.jpg

kita tampilkan Dockerfile

$ cat www/Dockerfile
35.jpg

kita tampilkan main.py

$ cat api/main.py
36.jpg

selanjutnya kita tampilkan docker-compose.yml

$ cat docker-compose.yml
37.jpg

kita booting dan up service

$ docker-compose up -d --build
38.jpg

$ docker-compose exec redis redis-cli monitor
39.jpg

$ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php

$ git reset --hard

$ docker-compose down
40.jpg

Step 6: Swap Python API Service with Ruby Conclusions
$ git checkout step6

$ tree
41.jpg

$ cat api/linkextractor.rb
42.jpg

$ cat api/Dockerfile
43.jpg

$ cat docker-compose.yml
44.jpg

dalam ervice ii kita build dan jalankan docker-compose

$ docker-compose up -d --build 
45.jpg

Akses API dengan port baru

$ curl -i http://localhost:4567/api/http://example.com/
46.jpg

46.jpg

Sekarang kita lakukan shut-down terhadap compose

$ docker-compose down
47.jpg

cek apakah log masih ada setelah service di matikan

$ cat logs/extraction.log
48.jpg

Sejauh ini, kita telah mempraktekan docker-compose untuk mengatur beberapa aplikasi berjalan dalam lingkup pengembangan.

Software yang Diperlukan
Linux, Docker


