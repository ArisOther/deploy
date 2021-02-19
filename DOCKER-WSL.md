# Docker di wsl ubuntu
- Docker Engine --> WSL2 Backend
- Instalasi
  - https://docs.docker.com/docker-for-windows/wsl/
  - Win 10 harus 1903 keatas --> winver
  - pastikan aktifkan wsl2 fitur (hyper-v dll) --> windows features
  - Install docker desktop for windows
  - Install [kernel terbaru](https://docs.microsoft.com/windows/wsl/wsl2-kernel)

- Setting docker desktop for windows
  - Run docker desktop
  - Settings > General --> Use WSL 2 based engine
  - Settings > resources > WSL Integration --> enable distro
  - Untuk merubah distro, powershell --> wsl --set-default ubuntu

- operation docker
  - Run docker desktop --> bisa di manage/stop/run melalui desktop
  - atau via terminal:
  - ubuntu: `docker ps` --> masih kosong
  - `docker run -d -p 80:80 docker/getting-started`
  - ubuntu: `docker ps` --> list image run
  - localhost:80 --> web akan run
  - Jika di cek di powershell -> wsl -l -v juga akan terlihat docker run sebagai VM

- coba run nginx
  - docker run -dp 8081:80 --name arisWebsite nginx
  - http://localhost:8081/

# Docker note
- Docker File --> [docs](https://docs.docker.com/engine/reference/builder/)
- Docker Compose --> [docs](https://docs.docker.com/compose/compose-file/#compose-file-structure-and-examples)
- Docker image
  - Docker image merupakan template dasar untuk docker container.
  - Image ini berisi sistem operasi ataupun aplikasi yang sudah selesai.
  - Docker image ini berfungsi untuk menjalankan container.
  - `docker image ls --all`
- Docker Container
  - Docker container merupakan sebuah image yang bersifat read-write.
  - Pada setiap perubahan yang disimpan pada container akan menyebabkan terbentuknya layer baru di atas image.
  - Developer dapat melakukan instalasi aplikasi didalamnya dan melakukan penyimpanan.
  - docker container [documentation](https://code.visualstudio.com/docs/remote/devcontainerjson-reference)
  - `docker container ls --all` atau `docker ps -a`
  - Docker container VS Code
  -  
- Docker Registries
  - Docker registries merupakan tempat penyimpanan (public atau private) di mana developer dapat mengunggah dan mengunduh image.
  - Docker registries bersifat public disebut dengan Docker Hub.
  - Disini, terdapat banyak image yang sudah dibuat atau image yang lain.
- Docker File
  - Dockerfile merupakan script yang yang berisi dari serangkaian perintah yang akan dieksekusi secara otomatis dan berurutan untuk membuat sebuah image.

- command penting
  - docker --> list command docker
  - docker info

# Docker-WSL di VS Code (best pactice)
- Instalasi
  - install docker desktop
  - install WSL2
  - Visual studio-WSL2 > Install Python linter dll
  - Visual studio-WSL2 > Install [Remote-WSL](https://aka.ms/vscode-remote/download/wsl)
  - Visual studio-WSL2 > Install [Remote-Containers](https://aka.ms/vscode-remote/download/containers)
- Run
  - --> Ubuntu$home> code .
  - pada remote explorer bisa dilihat list directory wsl yang tersambung ke vscode
  - new terminal > tampil bash ubuntu
  - hubungkan ke git

- Remote-Container
- 
