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
    % sudo docker pull nextcloud
    % sudo docker run --name nextcloud -d -p 8080:80 nextcloud

### 1-3. create database
    % sudo docker stop nextcloud && docker rm nextcloud
    % sudo docker pull postgres
- 일반적으로 각 도커 컨테이너는 분리되어 있다. 서로 다른 컨테이너가 들여다 볼 수 있으려면 Docker Network 를 만들어야 한다.
####
    % sudo docker network create --driver bridge nextcloud-net
    % sudo docker run --name postgres -e POSTGRES_PASSWORD=123123 --network nextcloud-net -d postgres
    % sudo docker run --name nextcloud -d -p 8080:80 -v /home/raspberrypi/nextcloud:/var/www/html --network nextcloud-net nextcloud  
####
![image](https://github.com/user-attachments/assets/5112e44e-3760-4e00-a315-3211a44cbed0)  
pw: 123123


### 1-4. 외부 저장소 추가

### 마운트 
    % sudo blkid
    /dev/mmcblk0p1: LABEL_FATBOOT="bootfs" LABEL="bootfs" UUID="9F76-08A2" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="8116ee1c-01"
    /dev/mmcblk0p2: LABEL="rootfs" UUID="4d48c72f-b919-4823-96cc-04d8e6dcc211" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="8116ee1c-02"
    /dev/sda1: BLOCK_SIZE="512" UUID="8002049E02049AF4" TYPE="ntfs" PARTUUID="c2b6aa02-01"
    
    % sudo apt install ntfs-3g exfat-fuse
    
    % sudo mkdir -p /mnt/ssd
    % sudo vi /etc/fstab
      (추가) UUID=8002049E02049AF4    /mnt/ssd    ntfs-3g    rw,nosuid,nodev,noatime,allow_other 0 1
    % sudo mount -a 
    
    // 마운트 확인
    % lsblk
    % df -h
    % sudo reboot


