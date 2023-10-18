# Git

## 1. Commit Message 작성법 

    [type](optional scope) : [subject] ,  
    [optional body]  
    [optional footer]  

### 1-1. type의 종류
- feat :	새로운 기능 추가
- fix :	버그 수정
- docs : 문서 수정
- style :	코드 formatting, 세미콜론(;) 누락, 코드 변경이 없는 경우
- refactor :	코드 리팩터링
- test :	테스트 코드, 리팩터링 테스트 코드 추가(프로덕션 코드 변경 X)
- chore	: 빌드 업무 수정, 패키지 매니저 수정(프로덕션 코드 변경 X)
- design :	CSS 등 사용자 UI 디자인 변경
- build	: 관련 변경 사항 빌드
- ci : CI 관련 변경 사항
- perf : 성능을 향상시키는 코드 변경
- omment : 필요한 주석 추가 및 변경
- revert : 되돌리기
- rename : 파일 혹은 폴더명을 수정하거나 옮기는 작업만인 경우
- remove :	파일을 삭제하는 작업만 수행한 경우
- !BREAKING CHANGE : 커다란 API 변경의 경우
- !HOTFIX : 급하게 치명적인 버그를 고쳐야 하는 경우

### 1-2. scope
- 선택사항이며, 변경된 부분을 표기한다.
- 함수가 변경됐으면 함수명을 필드나 메소드가 변경됐으면 클래스 명을 입력한다.

### 1-3. subject
- 변경사항을 나타내는 제목을 입력한다.
- 제목의 첫글자는 대문자로 작성한다.
- 제목줄은 50자 이내가 좋다.
- 제목 줄을 마침표로 끝내지 않는다.

### 1-4. body
- commit messege의 각 line은 72 글자를 넘기지 않아야 한다.
- 명령문, 현재 시제로 작성하는 것이 좋다.
- 변경한 이유, 변경 전과 후의 차이점을 기재한다.
- 어떻게 했는지 보다 무엇을 왜 했는지 작성한다.

### 1-5. footer
- 메세지 하단에는 변경점, 변경 사유, 마이그레이션 지시 기록한다.
- 관련된 이슈를 번호와 함께 언급한다.
- 주로 Closes(종료), Fixes(수정), Resolves(해결), Ref(참고), Related to(관련) 키워드를 사용한다.

### Example

  feat(HeaderAction) : Add dropdown animation,
  div box animation not yet applied
  fixes # 0000


## 2. Token
##### git-hub
> Settings - Developer settings - personal access tokens

#### git-lab
> User Settings -> Access Tokens -> Select scopes(read_repository, write_repository)  
(회사 gitlab인 경우 username과 userpassward 그대로 입력하면 된다.)

## 3. Git 시작하기 

### 3-1. 깃 초기 설정   
**git init** : .git이 숨김파일로 만들어지는 그럼 git clone에서 문제 발생  
**git config --global user.name <이름>**  
**git config --global user.email <깃이메일>**    
**git config --global core.autocrlf true** <맥-윈도우 간 개행문자가 다름으로 인해 텍스트파일 깨지는거 잡아주는 거  
**git remote add <원격저장소별명> <깃주소>**  
**git pull origin main**   
**git push -u <원격저장소별명> <브랜치이름>**   

### 3-2. 깃 저장소 폴더로 내려받는 방법
**git clone <깃 주소>**

### 3-3. 업데이트 
**git pull** 
  
### 3-4. 업로드
**git add <파일명> or <.>**  
**git add -u**   // 수정되거나 사제된 파일 반영  
**git commit -m“메세지”**  
**git commit -a-m”메세지”**  // 수정되거나 삭제된 파일만   
**git push**  
**git pull** 시 현재 브랜치에 추적 정보가 없습니다가 뜨는 경우  
➡️ **git branch —set-upstream-to=origin/<브랜치이름> master**  

❗️git 잔디가 안심어지면 이메일 제대로 작성했는데 확인하자
**git config —global —list**

### 3-5. 대용량 업로드
1. git-lfs 설치 : **brew install git-lfs**
2. (해당 디렉토리로 이동후) **git las install**
3. (만약 이전에 해당 디렉토리에서 git add기록이 있다면 unstaging 후) **git rm -r —cached**
4. 업로드하려는 파일 선택 : **git las track “파일명”**
5. **git add .gitattributes**

## 4. Git 언로드
### 4-1. git add 취소하기 
**git reset HEAD 파일명**

### 4-2. git commit 취소하기
**git reset HEAD^**

### 4-3. git commit 메세지 변경 
**git commit --amend**

### 4-4. 경고 무시하고 강제로 push하기
**git pusho origin 브랜치명 -f**

## 5. git명령어 

### 5-1. Git 시작하기 
- **git init** : 현재 폴더에 Git 로컬 저장소 생성 (최초 1회만 생성)
❗️프롬프트 끝에 브랜치명이 보인다면 이는 Git 작업 폴더라는 의미
- **git status** : Git 워킹트리*의 상태를 보는 명령
❓워킹트리 : 작업 폴더와 같은 말로 사용자가 파일과 하위폴더를 만들고 결과물을 저장하는 곳
- **git status -s** : git status 명령보다 짧게 요약해서 상태를 보여주는 명령, 변경된 파일이 많을 때 유용

### 5-2. 옵션 설정하기
**--system** : pc 전체 사용자를 위한 시스템옵션
**--golbal** : 현재 사용자를 위한 전역옵션
**--local** : 현재 git 저장소에서만 유효한 지역옵션
(우선순위 : 지역 > 전역 > 시스템)
- **git config --system core.editor** : 기본 에디터 조회
- **git config --global <옵션명>** : 전역옵션 조회
- **git config --global <옵션명> <새로운값>** : 전역옵션 지정
- **git config --global --unset <옵션명>** : 지정 전역옵션 삭제

### 5-3. Git 기본 명령어
- **git add 파일1 파일2 ...** : 파일들을 스테이지에 추가
  **git add .** : 현재 폴더에 있는 변경된 파일과 삭제된 파일 모두 스테이징
- **git commit** : 스테이지에 있는 파일들을 커밋
  **git commit -a** : add 명령을 생략하고 바로 커밋하고 싶을 때 사용
❗️untracked 파일은 커밋되지 않으니 주의
- **git reset [파일명]** : 스테이징 영역에 있는 파일들을 스테이지에서 내리기 (언스테이징)
- **git push [-u] [원격저장소별명] [브랜치이름]** : 현재 브랜치에서 새로 생성한 커밋을 원격저장소에 업로드
❗️-u 옵션으로 업스트림을 한번만 해두면 git push만 입력해도 업로드 가능
- **git pull** : 원격저장소의 변경사항을 워킹트리에 반영 
- **git fetch [원격저장소별명] [브랜치이름]** : 원격저장소의 브랜치와 커밋들을 로컬 저장소와 동기화 
❗️옵션을 생략하면 모든 원격저장소의 모든 브랜치 동기화 
- **git merge <브랜치이름>** : 지정한 브랜치의 커밋들을 현재 브랜치 및 워킹트리에 반영  

💫Tip) 커밋 시 vim 에디터가 실행된다면 
ESC - :q!(입력) - Enter - git 기본 에디터 변경(VScode로 변경하거나 재설치해서 VScode 설정)

### 5-4. log 살펴보기
- **git log -n<숫자>** : 숫자 만큼의 최신 커밋만 반환
- **git log --oneline** : 간단히 커밋 해시와 제목만 반환
- **git log --oneline --graph --decorate** : --graph는 브랜치 흐름 표시, --decorate는 브램치 태그 참조 표시
- **git log --oneline --graph --all --decorate** : 모든 브랜치를 보고 싶을 때 사용하는 명령
 
💫Tip) 커밋히스토리에 보이는 앞의 16진수 7자리 숫자는 커밋 체크섬 혹은 커밋 아이디

### 5-5. 원격 저장소 명령
- **git remote add <원격 저장소이름> <원격저장소주소>** : 원격 저장소 등록 시 사용
❗️원격저장소는 여러개 등록 가능, 같은 별명은 하나만 가능, 첫번째 원경저장소는 보통 origin으로 지정
- **git remote -v** : 원격저장소 목록 반환
- **git clone <저장소주소> [새로운폴더명]** :  저장소 복제, 폴더명 생략하면 프로젝트 이름으로 폴더 생성,
주소 뒤에 한 칸 띄고 . 입력하면 폴더 생성 없이 복제, 저장소 주소는 꼭 원격일 필요없고 로컬 저장소도 복제 가능

## 6. 브랜치

**Git remote branch 가져오기**

    $ git remote update  # 원격 저장소 업데이트
    $ git branch -r      # 원격 저장소 브랜치 확인
    $ git checkout -t origin/[원격 저장소 브랜치이름] 

**언제 브랜치를 쓰는가?**
1) 새로운 기능 추가 : master 브랜치에는 정상작동하는 버전만 저장, 기능 추가 시 브랜치 따로 파서 작업
2) 버그 수정 : hotFix, bugFix 같은 브랜치를 따로 파서 수정
3) 이전 코드 개선  
4) 특정 커밋으로 돌아가고 싶을 때
 
- **git branch [-v]** : 로컬 저장소 브랜치 목록 조회, [-v옵션 주면 마지막 커밋도 표시]
- **git branch [-f] <브램치이름> [커밋체크섬]** : 새로운 브랜치 생성, 커밋체크섬 값  없으면 HEAD*로 부터 브랜치 생성 
❓HEAD : 현재 작업중인 브랜치의 최근 커밋
- **git branch -r[v]** : 원격저장소에있는 브랜치를 보고싶을 때 사용 [-v옵션 주면 마지막 커밋도 표시]
- **git chechout <브랜치이름>** : 특정 브랜치로 체크아웃*할 때 사용
❓체크아웃 : 브랜치가 가르키는 커밋의 내용을 워킹트리에 반영
- **git checkout -b <브랜치이름> <커밋체크섬>** : 특정 커밋에서 브랜치 새로 생성과 동시에 체크아웃
- **git merge <대상브랜치>** : 현재 브랜치와 대상 브랜치를 병합할 때 사용
- **git rebase <대상브랜치>** : 내 브랜치의 커밋들을 대상 브랜치에 재배치
- **git branch -d <브랜치이름>** : 브랜치 삭제 (HEAD 브랜치나 병합되지 않은 브랜치는 삭제되지 않음)
- **git branch -D <브랜치이름>** :  브랜치 강제 삭제
                                                                         
💫Tip) 체크아웃에 많은 기능이 몰려 있어서 명령어 분할
- **git switch <브램치이름>** : 브랜치 변경 (기존에 없는 브랜치인 경우 생성하면서 변경)
- **git restore <파일명>** :  변경사항 복원 (작업중인 파일을 기존 마지막 커밋상태로 되돌리기)
 
<hr>

#### 7. 브랜치 되돌리기
- **git reset --hard <이동할커밋체크섬>** : 현재 브랜치를 지정한 커밋으로 옮기고 폴더 내용도 함께 변경
**git reset --hard HEAD~<숫자>** : n번째 위쪽 조상으로 브랜치 되돌리기
**git reset HEAD^** : 바로 이전 커밋으로 돌아감
**git reset HEAD^2** : 병합 커밋처럼 부모가 둘 이상인 커밋에서 두번째부모 지칭 
 
- **git revert <커밋체크섬>** : 해당 커밋만 삭제하는 커밋을 생성 (최신커밋부터 취소하는 것이 좋음) 
**git revert --no-commit <커밋체크섬>** : revert한 결과를 commit하지 않기 위한 옵션
❗️이후 git commit -m "어떤 커밋을 왜 리버트했는지 메모" 한 뒤 git push 하는 것이 좋다. 

<hr>

#### 8. 배포 버전에 태깅하기
- **git tag -a -m <간단한 메세지>  <태그이름> [브랜치 or 체크섬]** : -a로 주석이 있는 태그 생성(브랜치, 체크섬 생략하면 HEAD에 태그 생성)
**git push <원격저장소별명> <태그이름>** : 원격 저장소에 태그 업로드

