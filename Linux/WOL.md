# Wake On Lan

## 1. What is WOL
- WOL 은 전원이 꺼진 컴퓨터를 네트워크를 통해 원격으로 켜는 기술이다.

## 2. How to Work?
- 컴퓨터가 꺼져있어도 네트워크 카드(NIC)는 소량의 전력을 계속 공급받는다.
- 이 상태에서 NIC 는 네트워크 상에서 특정한 "매직 패킷"을 기다린다.
- 다른 장치 에서 매직 패킷을 네트워크로 전송한다.
- 꺼져있던 컴퓨터의 NIC 는 매직 패킷을 감지하고 컴퓨터의 전원을 켠다.

> **!참고** - 매직 패킷
> 매지 패킷은 컴퓨터를 깨우기 위해 특별히 고안된 데이터 패킷이다.
> 컴퓨터의 MAC 주소를 포함하고 있어 특정 컴퓨터만 깨울 수 있다.

## 3. How to use WOL?
1. BOIS 설정: 컴퓨터의 BIOS 설정에서 WOL 기능을 활성화해야 한다.
2. 네트워크 카드 설정: 네트워크 카드 드라이버 설정에서 WOL 을 활성화하고, 매직 패킷을 수신하도록 설정해야 한다.
3. 운영 체제 설정: 운영체제 에서 WOL 을 지원하도록 설정해야할 수 있다.
4. 전원 관리 설정: 컴퓨터가 꺼져 있을 때도 네트워크 카드에 전원이 공급되도록 설정해야 한다.

<br>

## 4. WOL Setting 

### 4-1. Main 보드에서 WOL 설정하기
- BIOS 메뉴에 들어가서 Wake On Lan, Wake On Magic Packet 등의 항목을 Enable 로 설정한다.

### 4-2. Ubuntu 에서 WOL 설정하기
- 메인보드에서 설정이 끝났다면 운영체제에서도 설정을 해줘야 한다.

#### 관련 패키지 설치
    % sudo apt-get install net-tools ethtool wakeonlan

### 네트워크 카드 이름 확인
    % ifconfig 
- 위 명령어를 입력하면 나오는 인터페이스이름 확인

####  WOL 을 수동으로 켜고 상태를 확인
    // 수동으로 켜기 
    % sudo ethtool -s 인터페이스이름 wol g
    
    // wol 작동 상태 확인: Wake-on 항목이 'g' 로 설정되어 있으면 정상 작동  
    % sudo ethtool 인터페이스이름
    
    // 부팅할 때마다 해당 설정을 켜주도록 네트워크 인터페이스 설정 파일 수정 
    % sudo vim /etc/systemd/system/wol.service
####
    [Unit]
    Description=Configure Wake-up on LAN
    
    [Service]
    Type=oneshot
    ExecStart=/sbin/ethtool -s 인터페이스명 wol g
    
    [Install]
    WantedBy=basic.target
####
    // 적용
    % sudo systemctl enable /etc/systemd/system/wol.service

### 4-3. 공유기 설정(LG)
- [192.168.219.1] - [네트워크 설정] - [원격제어 설정] -> 사용함
- [Wake On LAN] - [맥주소 검색] - [추가]

