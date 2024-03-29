## Docker 
- [Instalation](https://docs.docker.com/engine/install/ubuntu/)
- After Instalation
  ```
  sudo service docker start
  docker info
  docker version
  container registry : hub.docker.com
  docker images --> list image
  ```
## Problem list
- Jika ada error `docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post '.`
  ```
  sudo groupadd docker ------> buat grup bernama 'docker'
  sudo usermod -aG docker $USER  -----> tambahkan user pada grup
  reboot
  docker run hello-world  ---> coba jalankan
  
  sudo systemctl restart docker
  sudo chmod 666 /var/run/docker.sock
   
  ```
- Docker pada aws, permasalahan tidak bisa nyambung ip public
  ```
  # Firewall
  sudo ufw status
  sudo ufw enable
  sudo ufw disable
  sudo ufw status verbose
  sudo ufw allow 80/tcp
  
  sudo netstat -tulpn | grep LISTEN    ----------> cek port yang tersedia
  sudo nmap 127.0.0.1  ------> scan port yang dipunyai 127.0.0.1
  ```
  - Ternyata permasalahan ada pada cara menjalankan container dari image langsung membuat container tanpa memfoward port yang ada di aws.
  - cara yang benar:
  
  ```
  
  matikan firewall
  pada AWS security group, tambahkan port yang dibutuhkan misal: 80, 8080 dll
  
  docker images --> pastikan image sudah ada
  docker run -d -p 80:80 --name nginx_aris nginx:latest
  docker ps
  
  cek koneksi port:
  netstat -pln  --> #pastikan port ada dalam list
  
  curl http://localhost:80 
  #jika gagal
  docker exec nginx_aris curl http://localhost  --> untuk cek curl didalam docker
  

  ```

## Docker Image
- Membuat image
  - buat dockerfile
  - `docker build --tag app-golang:ver1.0 . --> build image (pada directory file)`
  - `docker images`

- environment variable

- Upload image ke registry docker / hub
  - hub.docker.com --> create a repository --> aris/app-golang:ver1.0
  - `docker login` --> akun docker hub
  - `docker push aris/app-golang:ver1.0` --> jika menggunkan ini akan error karena nama image di local() dan di repo tidak sama --> app-golang:ver1.0 vs aris/app-golang:ver1.0

  - `docker tag app-golang:ver1.0 aris/app-golang:ver1.0` --> akan membuat image baru aris/app-golang:ver1.0
  - `docker push aris/app-golang:ver1.0`
  - cek di hub.docker

- mengambil images
  - `docker pull mongo:4.1` --> mengambil dari hub.docker
  - `docker images` --> cek list images
- menghapus images
  - `docker image rm mongo:4.1` --> pastikan kondisi tidak sedang digunakan container
  - `docker rmi hello`
  - `docker rmi -f hello` --> menghapus force, menghilangkan network dsb
  - `docker system prune` --> menhapus image/container/network yang nonaktif--hati2
## Docker Container
- Membuat container
  ```
  docker container ls --> list container yang run
  docker container ls --all --> list semua container
  docker container create --name mongoserver1 mongo:4.1
  docker container create --name mongoserver2 mongo:4.1
  docker container create --name mongoserver3 -p 8080:27017 mongo:4.1 --> jika diakses dari luar menggunakan 8080, akan di forward ke port intern docker 27017
  docker container create --name mongoserver3 -p 8181:27017 mongo:4.1 --> jika diakses dari luar menggunakan 8181, akan di forward ke port intern docker 27017
  port internal 27017 sama ndak pa2 yang penting nama docker beda
  ```
- Membuat Container - dengan custom environment
```
buat image yang mengandung environment ex: hello.name=${NAMA}
docker container create --name java-docker -p 8080:8080 -e NAME=Docker -e APP=Java -e PASSWORD=rahasia mongo:4.1 --> menggunakan environment variable
docker container logs java-docker --> log proses instalasi
docker container inspect java-docker --> mengecek file2/object yang telah terinstall
```
- Container Start/stop
```
docker container start mongoserver1
docker container stop mongoserver1
```
- Menghapus Container
```
docker container rm mongoserver1 --> (pastikan kondisi off)
```

## Docker container  Best Pracice
- Docker container Postgresql
```
# port default psql = 5432, jika ingin merubah, tambahkan: -p <PORT_TCP>:<PORT_DOCKER>

# Create (cara 1: sudah punya image, cara 2: download image baru dari hub)
1. docker container create --name postgres_aris -e POSTGRES_PASSWORD=aris1985 postgres:latest
2. docker run --name postgres_aris -e POSTGRES_PASSWORD=aris1985 -d postgres

docker container ls --all
docker container start posgres_aris

docker exec -it postgres_aris psql -U postgres --> menjalankan postgres didalam docker



# Create - Cara alternatif dari docs resmi docker
docker run --rm -P --name postgres_aris -e POSTGRES_PASSWORD=aris1985 postgres:latest
docker run --rm -t -i --link postgres_aris:pg postgres:latest bash --> linking

```

## Integrasi container dengan network
- integrasi beberapa container
 - connect ke 2 dbase - mongodb & redis
 - pastikan punya image mongo dan redis, kalau ndak punya - pull dari registry
 - `docker container create --name mongo -p 27017:27017 mongo:4-xenial`
 - `docker container create --name redis -p 6379:6379 redis:5`
 - Buat file env java
    ```
      hello.name=${NAME}

      # Mongo config
      spring.data.mongodb.host=${MONGO_HOST}
      spring.data.mongodb.port=${MONGO_PORT}

      # Redis Config
      spring.redis.host=${REDIS_HOST}
      spring.redis.port=${REDIS_PORT}

      # Manajement Config
      management.endpoint.health.show-details=always

    ```
- Gabungkan container
  - `docker container create --name java-docker -p 8080:8080 -e NAME=Docker -e MONGO_HOST=mongo -e MONGO_PORT=27017 -e REDIS_HOST=redis -e REDIS_PORT=6379 java-docker:1.0`

## Docker Network
- Cara lain menggabungkan container dengan docker network
- Membuat Docker Network
  - `docker network`
  - `docker network --help`
  - `docker network create java_network`
  - `docker network ls`

- Memasukkan beberapa container ke dalam satu network
  ```
  docker network connect java_network mongo
  docker network connect java_network redis
  docker network connect java_network java-docker

  docker container inspect java-docker

  docker container ls --all
  docker container start mongo redis java-docker
  docker container logs java-docker
  ```

## Docker Compose

- file : docker-compose.yml

  ```
  version: "3.7"

  services:
    mongo:
      container_name: mongo
      image: mongo:4-xenial
      ports:
      - 27017:27017
      network:
      - java_network
    redis:
      container_name: redis
      image: redis:5
      ports:
      - 6379:6379
      network:
      - java_network
    java-docker:
      container_name: java-docker
      image: java-docker:1.0
      ports:
      - 8080:8080
      depends_on:
      - redis
      - mongo
      environment:
      - NAME=Docker
      - MONGO_HOST=mongo
      - MONGO_PORT=27017
      - REDIS_HOST=redis
      - REDIS_PORT=6379
      network:
      - java_network
  networks: 
    java_network:
      name: java_network

  ```

- `docker-compose up -d`
	- `docker container logs java-docker`
- `docker-compose stop` --> menghentikan service 
- `docker-compose down` --> menghentikan service dan menghapus container

## Volume
- `docker volume`
- `docker volume create mongo_data`
- lihat dokumentasi mongo ketika create mongo dan mounting ke directory
- `docker container create --name mongo -p 27017:27017 -v mongo_data:/data/db mongo:4-xenial`
- coba hapus container mongo
  ```
  docker container stop mongo
  docker container rm mongo
  ```
- ulangi create: `docker container create --name mongo -p 27017:27017 -v mongo_data:/data/db mongo:4-xenial`
- maka database diawal tadi tetep ada karena db tersimpan di volume mongo_data

## Backup
- `docker inspect -f '{{ json .Mounts }}' 007dabafcad8 | python -m json.tool` --> mencari path mounts
- `docker run --rm --volumes-from 007dabafcad8 -v $(pwd):/backup ubuntu tar cvf /backup/backup_static.tar /opt/services/djangoapp/static`
## Restore
- create new container - db_store2
- `docker run --rm --volumes-from dbstore2 -v $(pwd):/backup ubuntu bash -c "cd /dbdata && tar xvf /backup/backup.tar --strip 1"`
- https://www.youtube.com/watch?v=ZEy8iFbgbPA
## Docker Hub
- Buat akun di docker hub --> di terminal local: docker login
- Misal ada image local: `volume-dtabase123`
- Buat repo di docker hub. Misal : `aris/volume-dtabase`
- `docker push aris/volume-dtabase:1.0` ---> maka akan error karena nama image dilocal tidak sama dengan nama image di hub
- solusi buat tag: `docker tag volume-dtabase123:1.0 aris/volume-dtabase:1.0`
- 
