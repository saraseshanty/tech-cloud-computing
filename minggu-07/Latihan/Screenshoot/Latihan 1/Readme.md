Install Docker on Ubuntu 22.04
Latihan
Install Docker sesuai petunjuk pada Materi dan Pembahasan di atas, sesuaikan dengan OS yang anda gunakan.
Kerjakan no 4 pada Materi dan Penjelasan di atas.
Teknologi Virtualisasi dan Container - Docker

Pengertian container dan keterkaitannya dengan Docker
Instalasi Docker
Download Software yang Diperlukan
Docker.
Latihan Install
Artikel tentang Docker di Wikipedia
Instalasi Docker
Get Started - Docker
Dokumentasi DockerHub
Download dan Install Docker
Donwload Docker.

Install using the repository
Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

Set up the repository
1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

sudo apt-get update

sudo apt-get install \
ca-certificates \
curl \
gnupg \
lsb-release

2. Add Docker’s official GPG key:
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

3. Use the following command to set up the repository:
$ echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Install Docker Engine
Install Docker Engine $ sudo apt-get update
Install Docker Engine, containerd, and Docker Compose. $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
Verify that the Docker Engine installation is successful by running the hello-world image: $ sudo docker run hello-world
