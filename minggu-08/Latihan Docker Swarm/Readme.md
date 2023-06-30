Latihan Praktikum Teknologi Cloud Computing - Minggu 8
Rahadiyan Bondan Permadi
215411119
Materi
Docker Swarm

inisialisasi docker swarm
$ docker swarm init
1.jpg

status docker swarm
$ docker info | grep -i swarm
2.jpg

status docker node yang sudah join ke swarm dengan perintah
$ docker node ls
3.jpg

add node to swarm, memerlukan join token dari token yang kita dapatkan ketika inisialisasi swarm pada gambar pertama diatas :
$ docker swarm join-token worker
4.jpg
