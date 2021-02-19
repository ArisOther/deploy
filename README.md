## WSL - instalasi
- dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
- dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
- atau : windows feature> cekbok windows hypervision dan windows sub linux
- download/install kernel terbaru --> https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
- powershell> wsl --set-default-version 2
- download ubuntu --> windows store

## manage WSL:
- buka power shell
- wsl -l --all  --> list semua wsl
- wsl -l --running --> wsl yang aktif 
- wsl --set-version Ubuntu-18.04 2 --> set distro/upgrade ke ver2
- wsl -s Ubuntu-20.04 --> set distro default
- wsl -t Ubuntu-18.04 --> terminate distro
- wsl --shutdown --> mematikan

## prepare WSL - ubuntu
- Buka ubuntu cli
- Warning : jika dibuka dari windows terminal, gunakan path /home/<user> sebagai base, tidak dianjurkan menggunakan path base drive windows
  - lakukan perubahan di windows terminal setting "startingDirectory": "//wsl$/Ubuntu-18.04/home/wes/"
- buat username/pass --> otomatis saat run ubuntu pertama kali
- sudo apt update && sudo apt upgrade]
- reset password --> passwd
- lupa password --> 
  - powershell>wsl -u root
  - passwd <WSLUsername>
  - exit

## WSL - VS Code
- sudo apt-get install wget ca-certificates --> untuk ssl web
- aris@L420-PC:~$ code .
- install extention wsl



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




