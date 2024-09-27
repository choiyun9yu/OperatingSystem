# Raspberry Pi

## 1. Raspberry Pi OS 설치
- [download link](https://www.raspberrypi.com/software/)
- Raspberry Pi OS (other) -> Raspberry Pi OS Lite(32-bit)
  (Lite 는 CTL, Full 은 GUI)
#### Hostname 
- Hostname 은 네트워크에 접속된 장치에게 주어지는 이름이다.
- 동일 네트워크 상에 존재한다면 내부 아이피를 몰라도 Hostname 을 통해 정치를 식별할 수 있다.
- 기본 값은 raspberrypi 이다.
#### SSH
- Ctrl + Shift + X : 상세 설정 화면 
- SSH 사용 체크박스만 선택하면 된다. (Enable SSH)
#### 사용자 이름 및 비밀번호 설정
- 사용자 이름과 비밀번호 설정으로 유저명과 비밀번호를 사용할 수 있다.
#### WiFi 설정
- SSID 와 PSK 설정이 가능하다.
- 또한 아래에 WiFi 국가에 대한 설정이 있는데, 국가마다 WiFi 에 사용되는 대역이 조금씩 다르다.
#### 로케일 설정
- locale 은 지역별 표기법 등을 묶어둔 매개변수 집합이다.
- 시간대는 Asia/Seoul, 키보드 레이아웃은 us 를 사용하면 된다.
#### 쓰기
- 설정일 마친 뒤 쓰기 버튼을 눌러 이미지 파일을 저장 장치에 구워주면 된다. (10분 정도 소요)

<br>

## 2. NAS
- Synology 는 웹상에서 서버 운영 및 모니터링이 가능하고, 윈도우 환경에서 SAMBA 로 저장공간을 공유할 수 있고,
  기타 미디어 서버도 제공하지만 너무 비싸다.
- 집에 있는 구형 컴퓨터도 가능하지만 NAS 서버 특성상 24시간 켜 놓기 때문에 전기 요금이 걱정이다.
- 그래서 저전력 라즈베리파이가 가장 적당하다.

### 2-1. OMV(Open Media Vault)  
- NAS 솔루션을 구축하기 위해 설계된 오픈 소스 운영체제이다. OMV 는 가정 사용자와 중소기업을 대상으로 한다.
- 파일 저장, 백업, 미디어 서버 등의 기능을 제공한다.
- [document](https://www.openmediavault.org/)

#### 주요 특징
- 쉬운 설치 및 설정
  - 웹 기반 인터페이스: OMV 는 사용자 친화적인 웹 기반 인터페이스를 제공하여, 설치 후 브라우저를 통해 쉽게 설정 및 관리할 수 있다.
  - 플러그인 시스템: 다양한 플러그인을 통해 기능을 확장할 수 있으며, 이를 통해 사용자는 자신의 필요에 맞게 커스터마이징 할 수 있다.   
- 파일 시스템 및 스토리지 관리
  - 다양한 파일 시스템 지원: ext3, ext4, XFS, Btrfs 등 다양한 파일 시스템을 지원한다.
  - RAID 지원: RAID 0, 1, 5, 6, 10 등의 소프트웨어 RAID 설정을 통해 데이터 보호 및 성능 향상을 구현할 수 있다.
  - LVM 및 S.M.A.R.T.: 논리 볼륨 관리(LVM)와 S.M.A.R.T.모니터링을 통해 디스크 상태를 관리하고,
    스토리지 용량을 유연하게 할당할 수 있다.
- 네트워크 기능
  - SMB/CIFS, FTP, NFS, rsync: 다양한 파일 공유 프로토콜을 지원하여, 다양한 운영 체제와의 호환성을 제공한다.
  - 사용자 그룹 관리: 사용자의 접근 권한을 설정하고, 그룹을 통해 효율적으로 사용자 권한을 관리할 수 있다.
- 백업 및 복원
  - rsync 및 RSnapshot: 정기적인 백업을 설정하고, 파일 및 폴더의 스냅샷을 통해 데이터를 복원할 수 있다.
  - USB 백업: 외부 USB 드라이브를 통해 손쉽게 데이터를 백업할 수 있다.
- 미디어 서버 기능
  - DLNA/UPnP 지원: 미디어 파일을 네트워크 상의 다른 장치에서 스트리밍할 수 있다.
  - Plex 및 Embyu: 플러그인을 통해 Plex 또는 Emby 미디어 서버를 설치하여, 보다 강력한 미디어 관리 및 스트리밍 기능을 사용할 수 있다.
- 모니터링 및 알림
  - 시스템 모니터링: CPU, 메모리, 네트워크 사용량 등을 실시간으로 모니터링 할 수 있다.
  - 알림 시스템: 이메일 알림을 통해 시스템 상태 및 중요한 이벤트에 대해 통보받을 수 있다.

#### 설치 및 설정
    // OMV 설치 
    sudo apt update && sudo apt upgrade  // 라즈베리파이 CTL 에서 
    sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash

    // 설치 중간에 화면이 꺼진 경우
    sudo dpkg --configure -a

    sudo omv-confdbadm populate

#### OpenMediaVault 접속하기
- 브라우저 열고 라즈베리 파이 주소를 입력한다.
- 초기 설정을 하는데 포트 번호를 바꾸어줘야 한다.
