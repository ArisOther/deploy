## WSL
- Instalasi wsl
  - doenload ubuntu wsl-->install wsl dari windows store lebih simple
  - windows feature> cekbok windows hypervision dan windows sub linux
- cek:
  - buka power shell
  - wsl -l --all  --> list semua wsl
  - wsl -l --running --> wsl yang aktif 
  - wsl --set-version Ubuntu-18.04 2 --> set distro
  - wsl --shutdown --> mematikan



- Install python 3.8 dan menjadikannya default
  ```
  sudo apt update
  sudo apt install software-properties-common
  sudo add-apt-repository ppa:deadsnakes/ppa
  sudo apt install python3.8
  
  sudo update-alternatives --config python --> jika belum ada, buat config
  sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 1

  sudo update-alternatives --config python --> pilih 3.8 sebagai default
  python --version
  ```



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
