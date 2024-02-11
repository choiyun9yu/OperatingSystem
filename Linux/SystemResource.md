# System Resource

## 1. CPU

#### cpu 점유율 확인

    % top

#### cpu 전체 정보 확인

    % cat /proc/cpuinfo

#### cpu 코어 수 확인

    % cat /proc/cpuinfo | grep processor | wc -l

#### cpu 논리 코어 수 확인

    % grep -c processor /proc/cpuinfo

#### 물리 cpu 개수 확인

    % grep "physical id" /proc/cpuinfo | sort -u | wc -l

#### cpu 당 물리 코어 수 확인

    % grep "cpu cores" /proc/cpuinfo | tail -1

## 2. RAM

####  ram 사용량 확인

    % free -h

## 3.  SSD/HDD

#### 저장 공간 확인

    % df -h 

## 4. GPU

#### GPU 카드 확인 (둘 중 하나)
    % lspci | grep -i VGA

    % nvidia-smi --query | fgrep 'Product Name'
