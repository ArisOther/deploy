# Docker di wsl ubuntu
- Instalasi
  - https://docs.docker.com/docker-for-windows/wsl/
  - Win 10 harus 1903 keatas --> winver
  - pastikan aktifkan wsl2 fitur (hyper-v dll) --> windows features
  - Install docker desktop for windows
  - Install https://docs.microsoft.com/windows/wsl/wsl2-kernel

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
