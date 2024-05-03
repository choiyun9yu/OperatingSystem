# NoMachine

## 1. Install 

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
