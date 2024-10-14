# CUDA

## 1. Install 
### 1-1. NVIDIA driver
- NNIDIA 드라이버는 우분투의 기본 드라이버 관리 시스템을 통해 설치할 수 있다.
####
    % sudo apt update
    % sudo apt upgrade 

    // 드라이버 추천받기 (일반 데스크탑 사용자라면 550 보다 535가 더 좋을 수 있음)
    % ubuntu-drivers devices

    // 드라이버 설치
    % sudo apt install nvidia-driver-535
    % sudo reboot

    // 드라이버 확인
    % nvidia-smi

### 1-2. CUDA tool kit 
- [CUDA toolkit 12.4](https://developer.nvidia.com/cuda-12-4-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_network)
- [GPU 와 호환되는 cuda toolkit 확인](https://en.wikipedia.org/wiki/CUDA)
  ![image](https://github.com/user-attachments/assets/3127f408-2eca-4198-b0ef-cf2cab8dbfea)

#### 
    // CUDA 툴킷 버전 호환 확인 (4080SUEPR 는 CUDA 12.X 이상)
    // NVIDIA 홈페이지에서 쿠다 툴킷 다운로드

    // Base Installer
    % wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
    % sudo dpkg -i cuda-keyring_1.1-1_all.deb
    % sudo apt-get update
    % sudo apt-get -y install cuda-toolkit-12-4    
    
    // CUDA 환경변수 설정
    % echo 'export PATH=/usr/local/cuda-12.2/bin:$PATH' >> ~/.bashrc
    % echo 'export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
    % source ~/.bashrc

    // CUDA 설치 확인
    % nvcc --version
  
### 1-3. cuDNN 
- 


### 1-4. torch
- cuda toolkit 은 torch 버전과도 호환이 되야 한다. [torch](https://pytorch.org/get-started/previous-versions/)
- [torch install](https://pytorch.org/get-started/locally/)
####
    % pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124


    

    // 설치 확인
    % nvcc --version
