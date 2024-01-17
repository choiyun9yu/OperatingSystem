# tmux
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
