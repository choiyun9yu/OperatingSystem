# Vim (Terminal Editor)
- 명령 모드 : 처음 vi 명령어로 vi 편집기로 들어간 경우 (i or a를 누르면 입력모드 전환)
- 입력 모드 : 자유롭게 코드나 글을 작성할 수 있는 코드 (ESC를 누르면 명령모드로 전환)
- 마지막 행 모드 : 명령모드에서 콜론(:)을 입력하고 어떻게 종료할지 결정

## 1. 명령 모드 명령어
- i : 커서 현재 위치에 삽입
- a : 커서 바로 다음에 삽입
- o : 커서 바로 아래에 삽입

- u : 방금 한 명력 취소

- h : 왼쪽
- j : 아래쪽
- k : 위쪽
- l : 오른쪽

- 0 : 커서가 있는 줄 맨 앞
- $ : 커서가 있는 줄 맨 뒤
- (원하는 줄) shift + G : 해당 줄로 이동 
- G : 파일의 끝으로 이동

- dd : 커서 위치한 곳 한 줄 삭제(ctrl + x)
- yy : 현재 줄을 버퍼로 복사(ctrl + c)

- p : 현재 커서가 있는 줄 아래 붙여넣기(ctrl + v)


## 2. 마지막 행 모드 명령어
- set nu : 라인번호 출력
- set nonu : 라인번호 출력 취소
- w : 저장
- w [파일명] : 파일명으로 저장
- q : 종료(저장안됨)
- wq : 저장 후 종료
- f [파일명] : 파일 이름을 [파일명]으로 변경
- e! : 마지막 저장 이후 모든 편집 취소
- 뒤에 ! 붙이면 강제 수행
  
<br>

# tmux (Teminal Multiflexer)
- 일반적으로 ssh로 접속해서 사용하는 경우 ssh 접속이 끊어지면 ssh 서버는 해당 프로세스를 중단한다.
- tmux 를 ssh 클라이언트가 접속을 끊더라도 서버에서 해당 작업을 계속하도록 하기 위해 사용할 수 있다.

## 1. What is tmux?
- tmux 를 실행하면 하나의 window를 가지는 새로운 session 을 만들고 이것을 화면에 출력한다.
- 화면 아래에 상태 표시줄에 현재 session 정보가 표시되며 이는 interactive commands를 입력하는데 사용된다.
- session 은 tmux가 관리하는 가상의 터미널 집합이다. 각각의 세션은 그것과 연결된 하나 또는 2개 이상의 윈도우를 갖고 있다.
- window 는 모니터 화면 전체를 차지하고 있고, 이 윈도우는 몇개의 패널로 나눌 수 있으며 각각의 패널은 분리된 가상의 터미널 이다.

![image](https://github.com/choiyun9yu/OperatingSystem/assets/110392046/ad281751-ec44-4dc0-abad-55309413f689)

## 1-1. Session
- tmux 는 tmux 서버, tmux 클라이언트로 나눌 수 있다.
- 이때 서버에서 실행되는 프로세스를 session 이라고 한다.
- session 은 tmux가 관리하는 가상의 터미널로 1개 이상의 클라이언트가 접속할 수 있다.
- 여러 클라이언트가 접속해서 이를 보며 동시에 작업도 가능하다. 

## 1-2. Window
- session 안에 무조건 1개 이상의 window 가 있다.
- window 는 index 로 구분하는데 번호는 0번 부터 시작한다.
- session 을 Chrome 이라고 한다면 window 는 Chrome의 탭이라고 할 수 있다.

## 1-3. Pane
- pane 은 window 내에 1개 이상 존재한다.
- pane이 실제 입력하는 단일 가상 터미널이라고 할 수 있다.

<br>

## 2. How to use tmux?

## 2-1. 시작하기
    // for Ubuntu
    % sudo apt install tmux   
    
    // for macOS
    % brew install tmux

    // 실행
    % t mux new -s 세션이름     

    // 세션에서 나가기 (세션을 종료하지 않고 기존 shell로 이동)
    Ctrl-b d  

    // 세션 조회
    % tmux ls

    // 세션 다시 접속
    % tmux attach -t 세션이름(세션번호)

    // 세션 종료
    % tmux kill-session -t 세션이름(세션번호)

## 2-2. 단축키
- 수직 분할: Ctrl-b %
- 수평 분할: Ctrl-b "
- 화면 간 이동: Ctrl-b 화살표
######
- 현재 세션 종료하지 않고 나가기: Ctrl-b d
- 현재 세션 종료: Ctrl-d

<br>

# ZelliJ (Teminal Multiflexer)

## 1. Install

    // Rust 설치
    % curl https://sh.rustup.rs -sSf | sh
    % 터미널 재시작 
    
    // zellij 설치 
    % cargo install --locked zellij  // 안되면 러스트 업데이트 % rustup update

## 2. Command

### 2-1. session
    // 세선 목록 조회
    % zellij list-sessions

    // 세선 접속
    % zellij attach {세션 번호 or 세션 이름}

   // 세션 나가기
   Ctrl + q
  
    // 활성중인 세선 종료
    % zellij kill-session   {세션 번호 or 세션 이름}
    % zellij ka   // 모든 세션 강제 종료 

    

### 2-2. tab
- [Ctrl + t]: tab 창 선택
- [Ctrl + t + 번호 or 방향키]: 탭 이동
- [Ctrl + t + n]: 새로운 탭 생성 


### 2-3. pane
- [Ctrl + p]: pane 창 선택


### 2-4. strider
    % zellij --layout strider
    // Alt + [ + 방향키


### 2-5. 
- [Alt + 방향키]: pane 간의 이동
- [Alt + = or -]: pane 사이즈 조절

