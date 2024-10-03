
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
- 초기 로그인 정보 
  - id: admin
  - pw: openmediavault

<br>

## 3. OMV 설정하기
### 3-1. 사용자 설정
#### 관리자 비밀번호 변경
- 우측 상단 [User settings] - [Change password] 

#### 사용자 생성
- 좌측 네비게이션바 [사용자] - [사용자] - +(create)

#### 하드 디스크 마운트
- [저장소] - [파일 시스템] - [재생버튼]

#### 공유 폴더 추가
- [저장소] - [공유 폴더 추가] -

#### SMB 서비스 활성화
- SMB 는 원격 드라이브를 로컬 드라이브처럼 사용할 수 있게 해주는 기능
- [서비스] - [SMB/CIFS] - [설정] - 활성화됨 - 공유폴더 선택
- (연결할 PC 에서) [네트워크 드라이브 연결] - \\ip주소\폴더경로  
  ![image](https://github.com/user-attachments/assets/ac34ec49-f7c7-413d-9721-b2d0a2379d47)
