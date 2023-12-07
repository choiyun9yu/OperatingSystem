# Git Lab Community Edition

## 1. Installation

    # 시스템 업데이트
    % sudo apt update
    % sudo apt upgrade -y

    # gitlab ce 레파지토리 추가
    % curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

    # gitlab 설치
    % sudo apt -y install gitlab-ce

    # gitlab 설정 변경
    % sudo vim /etc/gitlab/gitlab.rb  // external_url부분을 사용할 주소로 변경한다.
    % sudo gitlab-ctl reconfigure     // 설정 변경 반영

    % sudo gitlab-ctl status    // 상태
    % sudo gitlab-ctl stop      // 중지
    % sudo gitlab-ctl restart   // 재시작
    
