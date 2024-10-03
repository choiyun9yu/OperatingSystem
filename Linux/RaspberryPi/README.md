# Raspberry Pi

## 1. Raspberry Pi OS 설치
### 1-1. Install
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

### 1-2. Setting
    % vim /etc/lightdm/lightdm.conf
    // #xserver-command=X => xserver-command=X -s O -dpms
    % sudo /etc/init.d/lightdm restart


<br>

## 2. NAS
- Synology 는 웹상에서 서버 운영 및 모니터링이 가능하고, 윈도우 환경에서 SAMBA 로 저장공간을 공유할 수 있고,
  기타 미디어 서버도 제공하지만 너무 비싸다.
- 집에 있는 구형 컴퓨터도 가능하지만 NAS 서버 특성상 24시간 켜 놓기 때문에 전기 요금이 걱정이다.
- 그래서 저전력 라즈베리파이가 가장 적당하다.

### 3-2. FTP vs NFS vs SMB
#### FTP, File Transfer Protocol
- **주로 서버와 클라이언트 간 파일 전송을 위한 프로토콜**이다.
- FTP 는 파일을 업로드하거나 다운로드하는 데 사용되며, 파일을 직접 열어서 수정하지는 않는다.
- 기본 FTP 는 데이터를 암호화하지 않아 보안에 취약하다. 이를 해결하기 위해 FTPS, SFTP 가 사용된다.

#### NFS, Network File System
- 네트워크를 통해 파일 시스템을 공유하고, 클라이언트가 원격 서버의 파일을 로컬 파일처럼 사용할 수 있게 하는 프로토콜이다.
- NFS 는 **주로 유닉스/리눅스 환경에서 사용**되며, 원격 파일 시스템을 마운트하여 로컬 파일 시스템 처럼 사용할 수 있도록 해준다.
- 기본적으로 보안에 취약할 수 있으므로, NFSv4 에서는 보안이 강화되어 인증 및 암호화 기능을 제공한다.
- 파일 시스템 수준에서 작동하여 네트워크를 통해 서버의 특정 디렉토리를 클라이언트에 마운트한다.

#### SMB, Server Message Block
- 네트워크 사엥서 파일, 프린터, 포트, 및 기타 리소스를 공유하기 위한 프로토콜이다.
- **주로 윈도우 환경에서 사용**되며, CIFS(Common InternetFile System)로도 알려져있다.
- 사용자가 네트워크 자원을 쉽게 찾고 사용할 수 있게 해준다.
- 최신 버전인 SMB3 는 데이터 암호화 및 무결성 검증 기능을 제공하여 보안을 강화하였다.
- SMB 는 클라이언트-서버 모델로 동작하여, 네트워크 상의 리소스를 공유하고 해당 리로스를 액세스하는 클라이언트에게 제공한다.
