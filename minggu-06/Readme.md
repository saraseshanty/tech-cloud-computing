Praktikum Teknologi Cloud Computing - Minggu 06
Materi
Data as A Service

Tujuan
Mahasiswa memahami berbagai tipe software DBMS untuk mengelola berbagai model data.
Mahasiswa memahami keterkaitan teknologi Cloud Computing dengan DBMS dalam konteks Data as a Service.
Mahasiswa memahami arsitektur Data as A Service.
Mahasiswa memahami dan mampu mengimplementasikan Data as a Service menggunakan Go dan DBMS.
Pembahasan
Berbagai tipe software DBMS untuk mengelola berbagai model data
Pengertian Data as a Service dan Cloud Database
Arsitektur Data as a Service
Implementasi Data as a Service Menggunakan Go dan DBMS
Software yang Diperlukan
Sistem Operasi: Linux, Windows, Mac, FreeBSD, dan sistem operasi lain yang mendukung.
Compiler Go. bisa diperoleh di halaman download Go.
MySQL Community Edition.
MongoDB Community Server
Pembelajaran
Materi dan Penjelasan
Pada dasarnya ada 2 tipe DBMS: SQL dan NoSQL.
Pelajari Data as a Service di Wikipedia serta Cloud database.
Arsitektur Data as a Service biasanya diwujudukan dengan menggunakan arsitektur microservices. Compiler dan development tools bersama dengan REST atau gRPC atau GraphQL serta berbagai protokol untuk implementasi function as a service digunakan untuk membangun service. Akses ke data biasanya melibatkan DBMS (SQL maupun NoSQL). Untuk Go, bisa digunakan Gin untuk menghasilkan data JSON dalam respon.
Akses ke DBMS di Go dilakukan dengan menggunakan pustaka standar serta driver. Untuk MySQL serta berbagai DBMS SQL (RDBMS), digunakan paket database/sql. Untuk NoSQL (contoh: MongoDB), digunakan driver MongoDB untuk Go.
Latihan
Install Go, MySQL, dan MongoDB
Buat 2 contoh program Go masing-masing untuk koneksi dan membaca data dari MySQL dan MongoDB.
Dengan menggunakan Gin, buatlah RESTful API untuk membaca dara dari MySQL dan MongoDB tersebut.
Tugas
Buat 2 program menggunakan salah satu pustaka yang ada di implementasi GraphQL di Go untuk membaca data dari MySQL serta MongoDB dan memberikan respon GraphQL, 1 program untuk MySQL, 1 program untuk MongoDB.
