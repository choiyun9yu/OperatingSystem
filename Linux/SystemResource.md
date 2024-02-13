# System Resource

## 1. CPU

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

    % top -E g (shift + m 누르면 정렬된다.)    
        o PID: 프로세스 ID. 각 프로세스에 할당된 고유한 식별자이다.
        o USER: 프로세스를 실행한 사용자 이름이다.
        o PR: 프로세스의 우선 순위를 나타낸다. 값이 높을수록 더 높은 우선 순위이다.
        o NI: 프로세스의 nice 값이다. 높은 nice 값은 우선 순위를 낮추고, 낮은 nice 값은 우선 순위를 높인다.
        o VIRT: 가상 메모리 크기이다. 프로세스가 사용하는 실제 물리 메모리보다 더 큰 가상 메모리 공간을 나타낸다.
        o RES: 실제로 사용 중인 물리 메모리 크기이다. 이것은 프로세스가 실제로 시스템의 물리 메모리에서 차지하는 양을 나타낸다.
        o SHR: 공유 메모리 크기이다. 여러 프로세스가 공유하는 메모리 영역의 크기를 나타낸다.
        o S: 프로세스의 상태이다. 보통 "S"는 슬리핑을 나타내고, "R"은 실행 중을 나타낸다.
        o %CPU: CPU 사용량의 백분율이다. 이는 프로세스가 CPU를 얼마나 사용하고 있는지를 나타낸다.
        o %MEM: 메모리 사용량의 백분율이다. 이는 프로세스가 시스템 메모리 중 얼마나 사용하고 있는지를 나타낸다.
        o TIME+: 프로세스가 CPU를 사용한 누적 시간이다.
        o COMMAND: 실행 중인 명령어 또는 프로세스 이름이다.
    
## 3.  SSD/HDD

#### 저장 공간 확인

    % df -h 

## 4. GPU

#### GPU 카드 확인 (둘 중 하나)
    % lspci | grep -i VGA

    % nvidia-smi --query | fgrep 'Product Name'
