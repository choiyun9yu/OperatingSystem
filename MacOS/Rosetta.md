# Rosetta

## 1. 로제타 사용법
    // 설치
    % softwareupdate --install-rosetta

    // 실행
    % arch -x86_64 /bin/zsh --login
    % arch -arm64 /bin/zsh --login   

    // 현재 실행중인 아키텍처 확인
    % arch

    // arm64 바이너리를 우선적으로 사용하도록 환경 설정 
    % export ARCHPREFERENCE=arm64
    
    // 제거 
    % sudo softwareupdate --remove-rosetta
