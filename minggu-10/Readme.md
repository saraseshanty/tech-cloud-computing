Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 10
Saras Eshanty
225611025
Materi
** Docker Networking Hands-on Lab **

Tujuan
Pada pertemuan ini, kita akan mempelajari konsep utama Docker Networking dan beberapa contoh konsep jaringan dasar, bridge danyang terakhir jaringan overlay.

Pembahasan
Dalam praktikum ini ada beberapa tahapan diantaranya adalah :

Section #1 - Networking Basics

Docker Network Command

  $ docker network
1.jpg

Daftar docker network

  $ docker network ls
2.jpg

Inspect a network

  $ docker network inspect bridge
3.jpg

Docker info

  $ docker info
4.jpg

Section #2 - Bridge Networking

daftar docker network

  $ docker network ls
5.jpg

Selanjutnya kita mulai install dulu brctl dengan perintah

  $ sudo apt-get install bridge-utils
6.jpg

  $ brctl show
6.jpg

menampilkan detail dari docker0

  $ ip a
7.jpg

Membuat container baru dengan menjalankan perintah :

  $ docker run -dt ubuntu sleep infinity
8.jpg

8.jpg

Memverivikasi container

  $ docker ps
9.jpg

Kembali kita tampilkan bridge-utils menggunakan

  $ brctl show
10.jpg

kita inspect kembali menggunakan perintah

  $ docker network inspect bridge
11.jpg

Lakukan ping dengan 172.17.0.2

  $ ping -c5 172.17.0.2
12.jpg

Docker ps

  $ docker ps
13.jpg

sekarang kita coba menjalankan didalam shell container ubuntu dengan perintah :

  $ docker exec -it fa39e102f0a4 /bin/bash
14.jpg

Selanjutnya kita install program ping dengan menjalankan perintah dibawah ini :

  $ apt-get update && apt-get install -y iputils-ping
15.jpg

selanjutnya kita coba koneksi dengan ping ke github

  $ ping -c5 www.github.com
16.jpg

Konfigurasi NAT untuk koneksi luar dengan memulai membuat container baru nginx

  $ docker run --name web1 -d -p 8080:80 nginx
17.jpg

  $ docker ps
18.jpg

kita buka web dengan durl

  $ curl 127.0.0.1:8080
19.jpg

Section #3 - Overlay Networking Cleaning Up

Pada langkah ini kita akan menginisialisasi swarm baru konek dengan node dan memverivikasinya.

Jalankan perintah berikut ini :

  $ docker swarm init --advertise-addr $(hostname -i)
20.jpg

Jalankan docker-swarm-join

  $ docker swarm join --token SWMTKN-1-28egcsrt15whmx4a5i9n6u3d7blnhip4bik468xm95l9kuuaxr-68l5e9lr62nyscynu9ui3ewym 192.168.0.27:2377

$ docker node ls
21.jpg

Membuat jaringan overlay

$ docker network create -d overlay overnet
$ docker network ls
22.jpg 23.jpg

Jalankan juga di terminal kedua

$ docker network ls
24.jpg

Kita inspect overnet

$ docker network inspect overnet
25.jpg

Step 3 Saatnya membuat layanan menggunakan jaringan yang sudah terinisialisasi
$ docker service create --name myservice \
--network overnet \
--replicas 2 \
ubuntu sleep infinity	
26.jpg

$ docker service ls
26.jpg

Memverifikasi single task (replika)

$ docker service ps myservice
27.jpg

$ docker network ls
28.jpg

$ docker network inspect overnet
29.jpg

Test jaringan

$ docker network inspect overnet
30.jpg

$ docker ps
31.jpg

install

$ docker exec -it e345aed47cba /bin/bash
32.jpg

$ apt-get update && apt-get install -y iputils-ping
33.jpg

test ping 10.0.0.3

$ ping 10.0.0.3 
34.jpg

$ cat /etc/resolv.conf
35.jpg

ping myservice

$ ping -c5 myservice
36.jpg

docker inspect myservice

$ docker service inspect myservice
37.jpg

cleaning up
$ docker service rm myservice
38.jpg

$ docker ps
39.jpg

$ docker kill 3ae8a2ac8297
40.jpg

$ docker swarm leave --force
41.jpg

Software yang Diperlukan
Linux, Docker, Docker Network, Docker Swarm


containerid

node1 3ae8a2ac8297
node2 ff36aa7e91e7

# Selesai
