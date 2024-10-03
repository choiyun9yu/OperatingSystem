# Next Cloud

## 1. Install 

### 1-1. setup docker
####
    % sudo apt update
    % sudo apt install docker.io
    
    % sudo systemctl start docker
    % sudo systemctl enable docker
    
    % sudo usermod -aG docker 사용자이름
    % sudo reboot now

### 1-2 download nextcloud
    % docker pull nextcloud
    % docker run --name nextcloud -d -p 8080:80 nextcloud

### 1-3. create database
    % docker stop nextcloud && docker rm nextcloud
    % docker pull postgres
- 일반적으로 각 도커 컨테이너는 분리되어 있다. 서로 다른 컨테이너가 들여다 볼 수 있으려면 Docker Network 를 만들어야 한다.
####
    % docker network create --driver bridge nextcloud-net
    % docker run --name postgres -e POSTGRES_PASSWORD=123123 --network nextcloud-net -d postgres
    % docker run --name nextcloud -d -p 8080:80 -v /home/raspberrypi/nextcloud:/var/www/html --network nextcloud-net nextcloud  
####
![image](https://github.com/user-attachments/assets/ce190bff-c1df-4538-86bb-c308c8b5f290)

### 1-4. 외부 저장소 추가

### 마운트 
    % sudo mkdir /mnt/ssd
    % sudo mount /dev/sda1 /mnt/ssd

    // 부팅 시 자동 마운트 설정
    % sudo vi /etc/fstab
      (추가) /dev/sda1 /mnt/ssd ext4 defaults,noatime 0 2

    % sudo moun -a 
    
    // 마운트 확인
    % lsblk
    % df -h
    /
    
#### 외부 저장소 추가 
- [우측 상단 프로필] - [+앱] - [좌측 네비게이션바 비활성화된 앱] - External storage support
- [우측 상단 프로필] - [관리자 설정] - [외부 저장소] - 로컬, 
