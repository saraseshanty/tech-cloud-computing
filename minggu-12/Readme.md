Laporan, Latihan dan Tugas Praktikum Teknologi Cloud Computing - Minggu 12
Saras Eshanty
225611025
Docker Orchestration Hands-on Lab
Materi
Di lab ini, kita akan bermain-main dengan container orchestration pada Docker. Kita akan menerapkan aplikasi sederhana ke satu host dan mempelajari cara kerjanya. Kemudian, kita mengonfigurasi Docker Swarm, dan belajar menerapkan aplikasi sederhana yang sama di beberapa host. Kemudian kita akan melihat cara menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.
Tujuan
Mahasiswa mampu menerapkan dan memahami aplikasi sederhana ke satu host dan mempelajari cara kerjanya.
Mahasiswa mampu mengkonfigurasikan Docker Swarm dan menerapkan beberapa aplikasi yang sama dalam beberapa host.
Mahasiswa mampu menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.
Pembahasan
Langkah - langkah Praktikum

Section 2

Configure Swarm Mode
Step 2. Menjalankan berbagai hal secara manual pada satu host dan membuat wadah baru di node1 dengan menjalankan
Login Docker : run

$ docker run -dt ubuntu sleep infinity
Node 1
1.jpg

melihat info docker

$ docker ps
docker ps
2.jpg

Step 2.1 - Create a Manager node
Inisialisasi New Swarm
$ docker swarm init --advertise-addr $(hostname -i)

3.jpg

$ docker info

4.jpg

4.jpg

Step 2.2 - Join Worker nodes to the Swarm
Paste On Node 1 and Node 2

$ docker swarm join --token SWMTKN-1-4jyeeeomwfddfbrhwib18kq08m7xisto1l0m3i5n8gpxbj1qy1-a6tizbli7zy4lm9nskm4ulhcw 192.168.0.18:2377
5.jpg

$ docker node ls
5.jpg

Section 3: Deploy applications across multiple hosts
Step 3.1 - Deploy the application components as Docker services
$ docker service create --name sleep-app ubuntu sleep infinity
6.jpg

$ docker service ls
6.jpg

Section 4: Scale the application
$ docker service update --replicas 7 sleep-app
7.jpg

$ docker service ps sleep-app
7.jpg

$ docker service update --replicas 4 sleep-app
8.jpg

$ docker service ps sleep-app
8.jpg

Section 5: Drain a node and reschedule the containers
$ cat Dockerfile
9.jpg

$ docker node ls
10.jpg

Software yang Diperlukan
Linux, Docker


