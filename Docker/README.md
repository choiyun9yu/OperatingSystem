# Docker

## 1. What is Docker?
### 1-1. Containers

어플리케이션을 패키징할 수 있는 툴이다. Container라고 불리는 하나의 소프트웨어 유닛 안에 어플리케이션, 시스템 툴 그리고 환경설정(의존성, 환경변수 등)을 하나로 묶어서 다른 서버 다른 PC에 쉽게 배포하고 안정적으로 구동할 수 있게 도와주는 도구이다.

VM과 다른 점은 VM은 Infrastructure 위에 Hypervisor을 쌓고 그위에 가상의 Guest OS를 포함하고 있다. 하지만 운영체제를 포함하고 있기 때문에 무겁고, 리소스를 많이 잡아 먹는다. 이 VM에서 많이 경량화된 것이 Container이다. Infrastructure위 Host OS에 Container Engine만 설치하면 사용할 수 있다. OS를 포함하지 않기 때문에 더 가볍다.

### 1-2. Building Containers
Container를 만들기 위해서는 Dockerfile과 Image가 필요하다. 

Dockerfile은 Container의 설계도와 같다. 어플리케이션을 구동하기위해 반드시 필요한 파일은 무엇인지, 외부 의존성 명시, 필요한 환경변수 설정 그리고 어떻게 구동해야하는지 스크립트까지 포함되어 있다. 

Image는 Dockerfile을 통해 만들 수 있다. Image 안에는 코드, 런타임 환경, 시스템 툴, 시스템 라이브러리 등 모든 세팅들이 들어있다. 실행되고 있는 어플리케이션 상태를 스냅샷 처럼 남겨두는 것이라고 할 수 있다. 이렇게 만들어진 Image 변경이 불가능하다.

마지막으로 Container는 샌드 박스 처럼 우리가 잘 캡쳐해둔 Image를 고립된 환경에서 실행할 수 있게 해준다. 즉, Image를 이용해서 어플리케이션을 구동하게 되는 것이다. 

### 1-3. Shipping Containers
Local Machine에서 Dockerfile을 만들고 Image를 생성한다. 그런 다음 깃의 외부 저장소 같은 Container Registry에 PUSH 한다. 그리고 필요한 곳에서 PULL로 Image를 가지고 온다. 물론 구동할 곳에도 Docker가 설치되어 있어야한다.

<br>

## 2. Practice
[docker-example](https://github.com/dream-ellie/docker-example)

### 2-1. Create Dockerfile
제일 빈번히 변경되는 것을 제일 아래에 작성하는 것이 좋다.  
[docker example project](https://github.com/dream-ellie/docker-example)  
[docker reference](https://docs.docker.com/engine/reference/builder/)

#### Dockerfile
    # 베이스 이미지 설정
    FROM (baseImage)      // {node, python, gradle} 입력하고 ctrl + click 하면 사용할 수 있는 베이스 이미지 조회 

    # 이미지 생성 과정에서 실행되는 명령어
    RUN npm ci          // 의존성 설치 {npm ci, yarn, }

    COPY package.json pacakage-lock.json ./    // 의존성 복사
    COPY index.js                              // 소스파일 복사

    # 이미지 내에서 명령어를 실행할(현 위치로 잡음) 위치 설정
    WORKDIR /(경로)      // WORKDIR 어떤 디렉토리의 어플리케이션 복사할 것인지 명시

    # 컨테이너 실행시 실행되는 명령어 (컨테이너 실행 시 시작되는 명령어지만 변경할 수 있음)
    CMD ["http-server", "-p", "8080", "./public"]    // WORKDIR에서 문자열 명령어 실행

    # 컨테이너가 실행시 최초에 꼭 동작해야하는 명령어가 있을 때 사용
    ENTRYPOINT ["node","index.js"]     // 실행

### 2-2. Build Image

    % docker build -f Dockerfile -t {도커이미지이름} .    // .은 도커파일이 있는 경로, -f는 사용할 도커파일 명시, -t는 도커 이미지에 이름 부여
    % docker images     // 도커 이미지 확인

### 2-3. Run Image

    % docker run -name {서비스명} -d -v ${pwd}:/(컨테이너에들어갈 경로) -p 8080:8080 {이미지명}   
        // -name은 서비스 이름 설정 옵션
        // -d는 Detached기능 (백그라운드에서 동작해야하므로)
        // -v 옵션은 컨테이너와 특정 폴더를 공유하는 것을 의미, ${pwd}현위치가:/(컨테이너에들어갈 경로)
        // -p포트로서 Host machine의 8080과 : Container의 8080 포트 연결
    % docker ps     // 현재 실행중인 컨테이너 확인

<br>

## 3. 도커 컴포즈 (거시적 설계도)
도커 컴포즈는 시스템 구축과 관련된 명령어를 하나의 YAML파일에 기재해 명령어 한번에 시스템 전체를 실행하고 종료와 폐기까지 한번에 하도록 도와주는 도구이다.

### 3-1. docker-compose.yml

    version: '3.8'    // 도커 컴포즈 버전 (최신버전 권장)
    services:
        # 서비스 이름
        service-name1:
            # 컨테이너 이름 설정
            container_name: service-name1
            # Dockerfile이 있는 위치
            build: 
                dockerfile: Dockerfile    // 도커파일 이름
                context: ./service-name1  // 도커파일 위치
            # 
            entrypoint: []         // Dockerfile의 entrypoint를 덮어쓴다.
            # 호스트 쪽에서는 접근 불가능하게 하고 컨테이너 사이의 통신만 가능하도록 지정
            expose:
                - "8080"           // 도커 내부적 포트
            # 내부에서 개방할 포트 : 외부에서 접근할 포트
            ports:
                - "0000":"0000"
            # 연결할 외부 디렉토리 : 컨테이너 내 디렉토리
            volumes:
                - 내컴퓨터디렉토리 : 컨테이너위치시킬디렉토리
            # 컨테이너 환경변수 설정
            envirionment:
                - DBHOST=database
            # 재시작 여부
            restart: always        // no, unless-stopped, on-failure:exit code
            # 단지 서비스가 시작되는 순서만 컨트롤
            depend_on:
                - service-name1
                - service-name2
                - service-name3
            # 해당 서비스 상태까지 확인
            depend_on:
                service-name:
                    condition: service_healthy(정상적으로 실행되고 있는지 체크, 해당 서비스에 healthcheck 옵션 필요)
                               service_complete(정상적으로 완료되었는지 체크)
<br>

## 4. 기본 명령어 모음

    $ docker -v                    // 도커 버전확인
    $ docker pull {이미지명}:{태그}   // 도커 이미지 다운만 받기
    $ docker images                // 컴퓨터 내 도커 이미지들 보기 
    $ docker ps                    // 동작중인 컨테이너 보기
    $ docker logs {컨테이너아이디}    // 동작중인 특정 컨테이너 로그 보기

    $ docker create {옵션} {이미지명}:{태그}    // 이미지로 컨테이너 생성하기
    $ docker start {컨테이너 id 또는 이름}      // 만들어진 컨테이너 시작하기
    $ docker restart {컨테이너 id 또는 이름}    // 동작중인 컨테이너 재시작
    $ docker attach {컨테이너 id 또는 이름}     // 컨테이너로 들어가기
    
    $ docker run {이미지명}:{태그}  // pull, create, attach 를 한번에 실행하는 것과 같다

    $ exit(또는 ctrl + D)     // 도커 컨테이너의 내부 쉘에서 빠져나오기
    $ ctrl + P,Q             // 컨테이너의 내부 쉘에서 빠져나오기 (컨테이너 종료하지는 않음)

#### 컨테이너 삭제
    $ docker rm {컨테이너 id 또는 이름}
    $ docker rm $(docker ps -a -q)    // 모든 컨테이너 삭제

#### 이미지 삭제
    $ docker rmi {옵션} {이미지id}  // 컨테이너가 있을시 강제삭제는 -f 옵션 사용 

#### 모든 컨테이너와 이미지 등 도커 요소 중지 및 삭제
    $ docker stop $(docker ps -qa)  // 모든 컨테이너 정료
    $ docker kill $(docker ps -qa)  // 모든 컨테이너 강제 종료
    
    $ docker system prune -a        // 사용되지 않는 모든 도커 요소 삭제 

#### 도커 컴포즈
    $ docker-compose up        // 실행
    $ docker-compose down      // 멈춤
  
#### 도커 옵션
|옵션|설명|
|----|----|
|-d|데몬으로 실행 (백그라운드에서 알아서 돌라고 지시)|
|-it|컨테이너로 들어갔을 때 bash로 CLI입출력을 사용할 수 있도록 해줌|
|-name{이름}|컨테이너 이름 지정|
|-p{호스트의 포트 번호}:{컨테이너의 포트 번호}|호스트와 컨테이너의 포트를 연결|
|-rm|컨테이너가 종료되면 컨테이너 제거|
|-v {호스트의 디렉토리}:{컨테이너의 디렉토리}|호스트와 컨테이너의 디렉토리를 연결|

<br>

## 5. Docker Network
Docker container는 격리된 환경에서 돌아가기 때문에 기본적으로 다른 컨테이너와의 통신이 불가능하다. 하지만 여러 개의 컨테이너를 하나의 Docker network에 연결시키면 서로 통신이 가능해진다.

### 5-1. 네트워크 조회
Docker network의 기본은 내 컴퓨터에서 어떤 네트워크가 생성되어 있는지를 아는 것이다. 아래 커맨드를 사용하면 현재 생성되어 있는 Docker 네트워크 목록을 조회할 수 있다.

    % docker network ls

NAME이 bridge, host, none인 네트워크는 Docker daemon이 실행되면서 디폴트로 생성되는 네트워크 이다. 대부분의 경우에는 이러한 디폴트 네트워크를 사용하는 것 보다는 사용자가 직접 네트워크를 생성해서 사용하는 것이 권장된다.

### 5-2. 네트워크 종류
Docker network는 bridge, host, overlay 등의 목적에 따라 다양한 종류의 네트워크 드라이버를 지원한다.
- bridge: bridge 네트워크는 하나의 호스트 컴퓨터 내에서 여러 컨테이너들이 서로 소통할 수 있도록 해준다.
- host: host 네트워크는 컨테이너를 호스트 컴퓨터와 동일한 네트워크에서 컨테이너를 돌리기 위해 사용한다.
- overlay: overlay 네트워크는 여러 호스트에 분산되어 돌아가는 컨테이너들 간에 네트워킹을 위해 사용된다.

### 5-3. 도커 네트워크 관련 기본 명령어

    % docker network create {네트워크명}    // 네트워크 생성
    % docker network rm {네트워크명}        // 네트워크 제거
    
    % docker network inspect {네트워크명}   // 네트워크 상세 정보

    % docker network connect {네트워크명} {컨테이너명}    // 네트워크에 컨테이너 연결
    % docker network disconnect bridge {컨테이너명}    // 네트워크에 컨테이너 연결 해제

    % docker network prune    // 네트워크 청소
    

## 6. Docker Compose Network
기본적으로 docker-compose는 하나의 디폴트 네트워크에 모든 네트워크를 연결한다. 디폴트 네트워크의 이름은 docker-compose.yml이 위치한 디렉토리 이름 뒤에 _default가 붙는다. 

Compose는 먼저 네트워크를 생성해놓고 각 컨테이너를 구동한 후 네트워크에 연결시킨다. 반대로 어플리케이션을 내릴 때는 먼저 컨테이너를 종료/제거하고 제일 마지막에 네트워크를 제거한다.

어플리케이션이 돌아가고 있는 중에 Docker network 목록을 조회하면 네트워크가 확인된다.

### 6-1. 컨테이너 간 통신
디폴트 네트워크 안에서 컨테이너 간의 통신에서는 서비스의 이름이 호스트명으로 사용된다. 

컨테이너 간 통신에서 주의할 점은 접속하는 위치가 디폴트 네트워크 내부냐 외부냐에 따라서 포트가 달라질 수 있다. 예를 들어, docker-compose.yml에 web 서비스의 ports 설정이 아래와 같다면
######
    services:
        web:
            ports:
                - "8001:8000"

호스트 컴퓨터에서 접속할 때는 8001포트를 사용해야하고, 같인 디폴트 네트워크 내의 다른 컨테이너에서 접속할 때는 포트 8000을 사용해야한다.

#### 커스텀 네트워크 추가

    service:
        ...
        # 네트워크 추가
        networks:
            - default
            - mynet
        # 네트워크 DRIVER를 HOST로 설정
        network_mode: host

    networks:
        mynet:
            driver: bridge

#### pring

    # 컨테이너1 에서 pring 명령을 실행시켜 컨테이너2와 연결되어 있는지 확인
    % docker exec {컨테이너1} ping {컨테이너2}
            












