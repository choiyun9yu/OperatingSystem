# Linux

![](https://velog.velcdn.com/images/yun9yu/post/34f842dd-11bc-4926-b210-1fd52a3947c5/image.png)
|디렉터리|저장 내용|
|------|------|
|/| 파일 시스템이 있는 최상위 디렉터리, 모든 디렉터리의 출발점인 동시에 다른 시스템과의 연결점이 되는 디렉터리|
|/boot| 부트 디렉터리로 부팅 시 커널 이미지와 부팅 정보 파일 전달|
|/proc| 시스템 정보 디렉터리이며 커널 기능을 제어하는 역할, 현재 실행되는 프로세스와 실제 사용되는 장치, 하드웨어 정보 저장|
|/lib| 공유 라이브러리 디렉터리, 커널 모듈 파일들과 프로그램 실행을 지원해주는 라이브러리 저장|
|/dev| 시스템 디바이스 파일들을 저장하는 디렉터리, 하드 디스크 장치 파일, CD-ROM 장치파일 같은 파일 저장|
|/etc| 시스템 환경 설정 파일 저장 디렉터리|
|/root| 시스템 관리자용 홈 디렉터리(루트 사용자용)|
|/sbin| 관리자용(s) 시스템 표준 명령 및 시스템 관리와 관련된 실행 명령어 저장|
|/usr| 사용자 디렉터리로 사용자 데이터나 애플리케이션 저장|
|/home| 일반 사용자들이 로그인 시 처음으로 위치하게 되는 디렉터리|
|/var| 가변 자료 저장 디렉터리로 로그 파일이나 메일 데이터 저장|
|/tmp| 각종 프로그램이나 프로세스 작업을 할 때 임시로 생성되는 파일 저장, 모든 사용자에 대해서 읽기와 쓰기가 허용|
|/mnt| 파일 시스템을 일시적으로 마운트할 때 사용|
|/lost+found| 결함이 있는 파일에 대한 정보가 저장되는 디렉터리|

# Ubuntu

터미널창 열기: ctrl + alt + T  

    % cat /etc/issue     // 현재 우분투 버전 확인
    
    % echo $SHELL        // 현재 SHELL 확인
    % cat /etc/shells    // 설치된 SHELL 확인

    % cat /proc/cpuinfo    // cpu정보
    % nproc                // 코어수
    
    % cat /proc/meminfo    // 메모리 정보
    % free
    
    % df -h       // 논리 디스크 파티션
    % fdisk -l    // 물리 디스크

    // 시리얼넘버 포함한 디스크 상세정보
    % sudo apt install hdparm
    % hdparm      

    

#### Upgrade
우분투는 메이저 버전업시 OS 업그레이드를 지원한다.

    $ apt update && apt upgrade -y
    $ apt dist-upgrade
    (재부팅)
    $ sudo apt install update-manager-core

    $ sudo apt list --upgradable
    $ sudo apt upgrade 
    (재부팅)
    
    $ sudo do-release-upgrade 

## zsh 변경

    $ sudo apt install zsh
    $ chsh -s /usr/bin/zsh    // 로그아웃 해야 변경된다. 다시 터미널을 열면 이상한 글씨들이 나오는데 0번을 눌러준다.

    # Oh-My-Zsh
    % sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    % vim .zshrc    // ZSH_THEME='rubbyrussell'를 ZSH_THEME='agnoster' 으로 바꾼다.
    # 폰트가 깨질 경우
    % sudo apt install fonts-powerline

    # 폰트 적용
    % mkdir ~/.local/share/fonts
    % cd ~/.local/share/fonts
    % wget https://github.com/naver/d2codingfont/releases/download/VER1.3.2/D2Coding-Ver1.3.2-20180524.zip
    % unzip D2Coding-Ver1.3.2-20180524.zip

    % fc-cache -f -v

    % fc-list | grep "D2Coding"

## 1. 변수
#### 쉘 변수 : 지역 변수(현재 쉘만 적용)

    $ [변수]=[할당 값]
    $ set|grep [변수명]    # 쉘 변수 확인
    (bash Shell 은 ctrl + shift + v 가 붙여넣기)
    
#### 환경변수 : 전역 변수(터미널 다시 시작하면 사라짐)
변수 이름은 대소문자 구분 O  
등호(=) 주위에는 공백 X  
따옴표("")는 공백이 있는 값을 지정할 때 사용  
콜론(:)은 변수에 여러 값을 할당할 때 사용  

    $ export 변수명=값    # 변수를 환경변수로 등록
    $ printenv 변수명    # 등록된 환경변수 확인
    $ unset 변수명       # 변수 설정 해제

#### 영구 환경변수
**/etc/bash.bashrc** 파일 수정

    $ vi ~/.bashrc         # ~ 사용하면 현재 사용자 자동 입력됨
    $ export 변수명="경로"    # 마지막 줄에 삽입 - ESC - :wq

#### 별칭

    $ alias           # 현재 등록된 별칭보기
    $ alias intelij='/opt/idea-IU-232.9559.62/bin/idea.sh'    # alias 별칭='명령어'
    $ unalias intelij     # 별칭 해제
    $ vi ~/.bashrc        # vi편집기로 .bashrc 켜서 등록
    $ source ~/.bashrc    # 동기화

## 2. VI 편집기 
명령 모드 : 처음 vi 명령어로 vi 편집기로 들어간 경우 (i or a를 누르면 입력모드 전환)
입력 모드 : 자유롭게 코드나 글을 작성할 수 있는 코드 (ESC를 누르면 명령모드로 전환)
마지막 행 모드 : 명령모드에서 콜론(:)을 입력하고 어떻게 종료할지 결정

### 2-1. 명령 모드 명령어

- i : 현재 커서 위치에 삽입
- a : 커서 바로 다음 위치에 삽입
- dd : 커서 위치한 곳 한 줄 삭제(ctrl + x)
- yy : 현재 줄을 버퍼로 복사(ctrl + c)
- p : 현재 커서가 있는 줄 아래 붙여넣기(ctrl + v)
- u : 방금 한 명력 취소
- k : 위쪽
- j : 아래쪽
- l : 오른쪽
- h : 왼쪽
- 0 : 커서가 있는 줄 맨 앞
- $ : 커서가 있는 줄 맨 뒤
- G : 파일의 끝으로 이동

### 2-2. 마지막 행 모드 명령어

- w : 저장
- w [파일명] : 파일명으로 저장
- q : 종료(저장안됨)
- wq : 저장 후 종료
- f [파일명] : 파일 이름을 [파일명]으로 변경
- e! : 마지막 저장 이후 모든 편집 취소
- set nu : 라인번호 출력
- set nonu : 라인번호 출력 취소
- 뒤에 ! 붙이면 강제 수행

## 3. apt 

    $ sudo apt-get update       # 패키지 정보 업데이트
    $ sudo apt-get upgrade      # 설치된 패키지 업데이트
    $ sudo apt-get dist-upgrade # 의존성 검사하면서 업데이트
  
    $ sudo apt-get install [패키지 이름] 
    $ apt-get --reinstall install [패키지 이름]
    $ sudo apt-get remove [패키지 이름]
    $ sudo apt-get --purge remove [패키지 이름] # 설정파일까지 모두 지움
  
    $ sudo apt-get source [패키지 이름]     # 패키지 소스코드 다운
    $ sudo apt-get build-dep [패키지 이름]  # 소스코드 의존성 있게 빌드
  
    $ sudo apt-cache search [패키지 이름]   # 패키지 검색
    $ sudo apt-cache show [패키지 이름]     # 패키지 정보 보기
 
### install 

#### cmake

    $ sudo apt-get install cmake
    $ cmake --version
 
#### pyenv

    # python3 is python
    $ sudo apt install python-is-python3

    $ curl https://pyenv.run | bash
    $ sed -Ei -e '/^([^#]|$)/ {a \
    export PYENV_ROOT="$HOME/.pyenv"
    a \
    export PATH="$PYENV_ROOT/bin:$PATH"
    a \
    ' -e ':a' -e '$!{n;ba};}' ~/.profile
    
    $ echo 'eval "$(pyenv init --path)"' >>~/.profile
    $ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
    $ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

    $ pyenv install --list    # 설치가능한 리스트
    $ pyenv install 3.7.13    # 파이썬 3.7.13 설치
    $ pyenv install 3.8.13    # 파이썬 3.8.13 설치
    $ pyenv versions          # 설치된 버전 리스트

    $ pyenv virtualenv 3.7.13 [envName]   // 가상환경 생성
    $ pyenv uninstall [envName]           // 가상환경 제거
    $ pyenv global 3.8.13                 // global 설정
    $ pyenv local [envName]               // loval 설정 (해당 경로에서)

#### java

    $ sudo apt-get install openjdk-11-jdk
    $ java -verison
    $ javac -version

    # 환경변수 설정
    $ sudo vi ~/.bashrc
    $ export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:bin/java::")
    $ source ~/.bashrc
    $ echo $JAVA_HOME
    
    # 버전 관리
    $ update-alternatives --list java    # 설치된 자바 버전 확인
    $ sudo update-alternatives --config java
    $ sudo update-alternatives --config javac

    $ sudo apt-get purge poenjdk*    $ 자바 삭제

#### node.js

    # npm 특정버전 업그레이드
    $ sudo npm install -g npm@x.x.x

    # nvm 대신 n을 사용
    $ npm install -g n 
    
    # node.js 특정버전 업그레이드
    $ sudo 
    n stable     // 안정 버전 설치
    n latest      //  최신 버전 설치
    n lts            // lts 버전 설치
    n x.x.x        // 특정 버전 설치 ( x.x.x 버전 )

    # 버전관리
    $ n ls          # 설치 목록 보기
    $ sudo n        # 방향키로 버전 선택 후 엔트
    $ n rm x.x.x    # 특정 버전 삭제

#### yarn

    # 설치
    $ sudo npm install -g yarn
    $ yarn --version
    $ export PATH="$PATH:/opt/yarn-[version]/bin"

    # 사용법
    $ yarn init     # 프로젝트 시작 시 초기화 하려면 (package.json 생성)
    $ yarn install  # package.json 으로부터 의존성 모듈 설치

    # 의존성 모듈 설치
    $ yarn add package.json
    $ yarn add [package]
    $ yarn add [package]@[version]
    $ yarn add [package]@[tag]
    
    # 의존성 모듈 업그레이드
    $ yarn upgrade [package]        
    $ yarn upgrade [package]@[version]
    $ yarn upgrade [package]@[tag]

    # 의존성 모듈 제거
    $ yarn remove [package]

**Yarn.lock** 파일은 설치된 모듈의 버전을 저장해 어디서나 같은 버전과 구조의 의존성을 가지게 한다.  
Yarn에서 자동으로 yarn install 때마다 yarn.lock이 생성된다.  
package-lock.json과 비슷한 기능을 한다고 생각하면 된다.

#### .NET
[install guide](https://learn.microsoft.com/ko-kr/dotnet/core/install/linux-ubuntu-2204#install-net)

    // .NET SDK 설치
    % sudo apt-get update && \
      sudo apt-get install -y dotnet-sdk-8.0

    // .NET RunTime 설치
    % sudo apt-get update && \
      sudo apt-get install -y aspnetcore-runtime-8.0

    // 설치 버전 확인
    % dotnet --list-sdks
    % dotnet --list-runtimes

    // .NET 설치 시 버전을 찾을 수 없는 경우 가이드에 따라 설치
    
#### git 

    $ sudo apt-get install git
    $ git --version

    $ git init
    $ git config --local user.name [userName]
    $ git config --local user.email [gitEmail]
    $ git config --local --list                 # 작성 확인
    $ git config --global core.autocrlf true    # 맥,윈도우 간 개행문자 다름으로 텍스트 깨지는거 보정

    [git 명령어 정리](https://velog.io/@yun9yu/Git-hub)
    
#### docker 

    # 필요한 패키지 설치
    $ sudo apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

    $ echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
    $ sudo apt-get update

    # 도커 설치
    $ sudo apt-get install -y docker-ce docker-ce-cli containerd.io
    $ sudo apt install docker-compose
    $ docker version
    
    $ sudo systemctl status docker    # 도커 실행상태 확인
    $ sudo docker run hello-world     # 도커 실행

    $ sudo docker stop [containderName]      # 도커 종료
    $ sudo docker kill $(sudo docker ps -qa) # 모든 도커 강제 종료

#### Docker ERROR 

    # Cannot connect to the Docker daemon at unix:/var/run/docker/sock ...
    $ sudo chmod 0777 /var/run/docker.sock  

    % sudo usermod -aG docker $USER    // 도커 그룹에 유저를 추가

#### mariaDB

    $ sudo apt instll mariadb-server
    $ sudo apt-get install mariadb-client
    $ sudo mysql_secure_installation
    
    $ sudo service mysql start 
    $ sudo mysql
    $ sudo service mysql stop
    $ sudo service mysql restart

    [sql 명령어 모음](https://github.com/choiyun9yu/Database)

#### HTTPie

    % curl -SsL https://packages.httpie.io/deb/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/httpie.gpg
    % sudo echo "deb [arch=amd64 signed-by=/usr/share/keyrings/httpie.gpg] https://packages.httpie.io/deb ./" > /etc/apt/sources.list.d/httpie.list
    % sudo apt update
    % sudo apt install httpie

#### MongoDB

    # 인터넷에 검색하여 그때 그때 최신 버전 설치 방법 확인
    
    # MongoDB 시작
    $ sudo systemctl start mongod
    # MongoDB 데몬을 재부팅 시 시작되도록 활성화
    $ sudo systemctl enable --now mongod

    # 버전 및 주소 확인
    $ mongo --eval 'db.runCommand({ connectionStatus: 1 })'

#### MongoDB compass
[Download link](https://www.mongodb.com/try/download/compass)

    # 다운받음 파일이 있는 경로에서
    $ sudo apt install ./{다운받은 파일명}

#### inteliJ

    # 다운로드
    $ wget https://download.jetbrains.com/idea/[다운로드파일명.tar.gz]
    
    # 압출풀기
    $ tar xvfz [압축파일명.tar.gz]

    # 사용할 경로로 이동 (개발툴 opt 경로에 두는 습관 나쁘지 않음)
    $ sudo mv [파일명] /opt/[파일명]

    # 별칭설정
    $ alias intelij='/opt/[경로이동한 파일명]/bin/idea.sh' >>~/.bashrc

    # 실행
    $ intelij







