Tugas
Container Docker Repository Alpine
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

Mencari Citra dari Alpine
$ sudo docker search apline
4.jpg

Pull atau menambahkan/download docker container dari dockerhub repository Alpine
$ sudo docker pull alpine
5.jpg

Menampilkan image alpine yang sudah di download
$ sudo docker images
6.jpg

Untuk menjalankan container alpine
$ sudo docker run -it alpine 
7.jpg

-- DONE --
