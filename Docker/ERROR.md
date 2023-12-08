# DOCKER ERROR

### Error: permission denied while trying to connect to the Docker daemon socket at unix://var/run/docker.sock:...
>[해법1] sudo로 권한 부여  
######    
    % sudo chmod 0777 /var/run/docker.sock
######
>[해법2] 권한 그룹에 지금 로그인한 사용자를 포함 시키기
######
    % sudo usermod -aG docker $USER

<br>

### Error: Python packaging tool 'setuptools' not found

>[해법1] 패키지 업데이트   
######
    % pip install --upgrade setuptools

>[해법2] Dockerfile에 'setuptools' 설치 추가    
######    
    RUN apt-get update && apt-get install -y python3-setuptools

>[해법3] Docker이미지 갱신, 이미지 변경 사항을 적용하고 Docker 이미지를 다시 빌드
