# Git Lab Community Edition
- Raspberry pi 4 4GB로 돌리면 메모리가 부족해서 사용하기 어려움

## 1. Installation

    # 시스템 업데이트
    % sudo apt update
    % sudo apt upgrade -y

    # gitlab ce 레파지토리 추가
    % curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

    # gitlab 설치
    % sudo apt -y install gitlab-ce

    # gitlab 설정 변경
    % sudo vim /etc/gitlab/gitlab.rb  // external_url부분을 사용할 주소로 변경가능 / 기본은 자기 ip주소
    % sudo gitlab-ctl reconfigure     // 설정 변경 반영

## 2. Start

    % sudo gitlab-ctl status    // 상태
    % sudo gitlab-ctl stop      // 중지
    % sudo gitlab-ctl restart   // 재시작

    # 최초 접속 ID는 root이고 비밀번호는 아래 명령으로 확인 가능
    % sudo cat /etc/gitlab/initial_root_password 

### 2-1. 초기 비밀번호가 제대로 작동하지 않는 경우
    
