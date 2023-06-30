Tugas
Container Docker Repository Ubuntu
DockerHub

Build Status

Tutorial Cara Install Docker dan membuat Container Docker di Ubuntu Server 22.04 Lts
Docker adalah Perangkat (PaAS) -Platform as A Service- Virtulasisasi Tingkat OS untuk mengirimkan perangkat lunak dalam bentuk container. Pertama - tama kita lakukan :

Install docker
$ sudo apt install docker
1.jpg

Install docker-compose
$ sudo apt install docker-compose
2.jpg

Cek status running docker
$ sudo service docker status
3.jpg

Mencari Citra dari Ubuntu
$ sudo docker search ubuntu
4.jpg

Pull atau menambahkan/download docker container dari dockerhub repository Ubuntu
$ sudo docker pull ubuntu
5.jpg

Menampilkan image ubuntu yang sudah di download
$ sudo docker images
6.jpg

Untuk menjalankan container ubuntu
$ sudo docker run -it ubuntu 
7.jpg

Kita coba install apache2
$ apt install apache2
8.jpg

9.jpg

Untuk cek status running paket apache2 container ubuntu
$ service apache2 status
10.jpg

-- DONE --


