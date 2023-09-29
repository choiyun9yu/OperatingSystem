# MacOS

#### [Homebrew](https://brew.sh/)

    # 설치 
    % /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    % vi ~/.zshrc
    % export PATH=/opt/homebrew/bin:$PATH
    % source ~/.zshrc
    
#### iterm2

	# iterm2 설치
	% brew install iterm2
    
    # Oh-my-zsh 설치
    % sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
	
	# 테마변경
	1. open ~/.zshrc 
	2. ZSH_THEME인 부분을 수정 “agnoster”
	3. 테마 소스파일 다운로드  https://iterm2colorschemes.com/     // MaterialDark
	4. 저장 소스파일 확장자 지우기 
	5. term2의 환경설정 → profile - colors - color presets... → Import하고 다운받은 파일을 선택
	
	# 폰트수정
	Term2를 켠 뒤 상태바 좌상단의 iTerm2 > Preference > Profiles > Text > Font

	# 터미널에서 폴더구조 tree로 보기
	% brew install tree
    % tree 

	# 터미널에서 code 실행
	1) 비주얼스튜디오에서  보기 > 명령팔레트 > path검색 > code 명령 설치 선택
	2) term창이나 터미널창에서 code 파일명.확장자

#### pyenv

    % brew install pyenv
    % brew install pyenv-virtualenv
    % echo $SHELL

    % echo 'eval "$(pyenv init --path)"' >> ~/.zprofile  
    % echo 'eval "$(pyenv init -)"' >> ~/.zshrc  
    % echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc  

    % pyenv --version

    % 프로젝트 경로에서
    % pyenv install 3.8.13
  
    # 가상환경
    % pyenv install 3.9.11                  # 파이썬 3.9.11 버전 설치
    % pyenv virtualenv 3.9.11 [venvName]    # venv라는 가상 환경 생성
    % mkdir projectName                     # 프로젝트를 위한 디렉토리(폴더) 생성
    % cd projectName                        # 디렉토리 안으로 이동
    % pyenv local [venvName]                # venv 가상 환경 적용
  
#### yarn

    % brew install yarn


#### git

     % brew install git
     % git config --global core.autocrlf true
     

#### MariaDB

    % brew install mariadb (안되면 arch -arm64 brew install mariadb)
    % brew services start mariadb    # 동작
    % brew services stop mariadb     # 중지
    % mariadb -h호스트명 -u계정명 -p패스워드 DB명    # 접속
          (root 계정 접속 : mariadb -uroot -p)

    # DB관리
    % SHOW databases;    
          CREAT database DB이름;
          DROP database DB이름;
          USE DB이름;