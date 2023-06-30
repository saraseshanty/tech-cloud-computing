Latihan Praktikum Teknologi Cloud Computing - Minggu 8
Rahadiyan Bondan Permadi
215411119
Materi
Docker Network

membuka menu docker network
$ sudo docker network
1.jpg

melihat daftar jaringan yang ada menggunakan perintah ls
$ sudo docker network ls
2.jpg

menambahkan network baru
$ sudo docker network create --subnet 192.176.60.56/24 tcc-rbp-pertemuan-ke8
3.jpg

cek kembali daftar jaringan setelah adanya penambahan
$ sudo docker network ls
4.jpg

jika sukses selanjutnya ke tahap running kontainer dengan menggunakan image httpd seperti dibawah
$ sudo docker run -d --network tcc-rbp-pertemuan-ke8 --ip 192.176.60.56 httpd
5.jpg 6.jpg

pastikan kontainer tidak ada error menggunakan perintah
$ sudo docker network ps
7.jp

pastikan status sudah UP dengan mengeceknya dg perintah
$ sudo docker network inspect tcc-rbp-pertemuan-ke8
8.jpg

Menghapus network
$ sudo docker network rm "nama network"
9.jpg

membuat Container dengan nama node1 dan node2 dari image engine stable-alpine yang udah tersedia
$ docker run -d --name node1 --network tcc-net nginx:stable-alpine
$ docker run -d --name node2 --network tcc-net nginx:stable-alpine    
10.jpg

memeriksa network yang kita buat menggunakan perintah :
$ docker network inspect tcc-net
11.jpg

memeriksa koneksi container node1 dan node2 didalam network yang kita buat menggunakan perintah :
$ docker exec node1 ping node2 
12.jpg

memeriksa koneksi birdge sebagai default network menggunakan perintah :
$ docker network inspect bridge
13.jpg

membuat container nodeX untuk pengujian selanjutnya menggunakan perintah :
$ docker container create --name nodeX nginx:stable-alpine
14.jpg

Start container nodeX untuk pengujian selanjutnya menggunakan perintah :
$ docker start nodeX 
15.jpg 16.jpg

menghubungkan container nodeX ke network tcc-net dengan perintah :
$ docker network connect tcc-net nodeX 
17.jpg

uji konektivitas antar node / container nodeX dengan node1 dan node2 dengan perintah :
$ docker network connect tcc-net nodeX 
18.jpg 19.jpg

melihat masing - masing network dan container yang berhasil ditambahkan dan dijalankan :
$ docker network connect tcc-net nodeX 
20.jpg

Sekian untuk management Docker Network
