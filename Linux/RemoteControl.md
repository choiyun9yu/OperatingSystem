# Remote Control

## 1. NoMachine

### 1-1. nomachine server 터미널에서 설치
  % sudo apt update
  % sudo apt upgrade

  % sudo apt -y install wget

  // https://downloads.nomachine.com/download/?id=1 에서 최신 링크 얻을 수 있음 
  % wget https://download.nomachine.com/download/8.11/Linux/nomachine_8.11.3_4_amd64.deb

  // 다운 받은 파일 명으로 교체
  % sudo dpkg -i nomachine_8.11.3_4_amd64.deb

### 1-2. 열려있는 포트번호 확인
   % sudo apt install net-tools
   % netstat -tnlp

### 1-3. 화면이 검게 나오는 경우
- 모니터를 연결하지 않고 부팅하면 화면이 검게 나옴
- 모니터를 연결하고 부팅 이후 모니터 연결을 해제하면 제대로 나옴

<br>
<br>

## 2. Chrome remote desktop

### 2-1. install
[download url](dl.google.com/linux/direct/chrome-remote-desktop_current_amd64.deb)

    // 종속성 패키지 설치
    % sudo apt-get install -f
    % sudo apt-get install xvfb xserver-xorg-video-dummy xbase-clients

    // 다운로드 경로에서
    % sudo dpkg -i chrome-remote-desktop_current_amd64.deb

    // 가상 데스크톱 세션 맞춤 설정
    % cd /usr/share/xsessions/
    % vim ubuntu.desktop 
      (Exec= 뒤에 있는 모든 부분 복사)

    // home 디렉토리로 이동 
    % cd /home
    % sudo vim .chrome-remote-desktop-session  
      (exec /etc/X11/Xsession '<YOUR_EXEC_COMMAND>')  
      YOUR_EXEC_COMMAND 안에 위에서 복사한 내용을 붙여 넣고 저장한다.


### 2-2. start
- 크롬에서 원격 데스크톱 검색
- 화면 공유 클릭하여 코드 생성
- 접속할 컴퓨터에서 액세스 코드 입력


    
