# CUDA
- CUDA 를 설치하지 않아도 Pytorch 를 설치하고 사용할 수 있다.
- 그러나 이 경우 연산에 CPU 만을 사용하기 때문에 병렬적인 연산이 많이 필요한 작업에 어려움이 있다.

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

    // Driver Installer
    % sudo apt-get install -y cuda-drivers-535
    
    // CUDA 환경변수 설정 (bash)
    % echo 'export PATH=/usr/local/cuda-12.2/bin:$PATH' >> ~/.bashrc
    % echo 'export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
    % source ~/.bashrc

    // CUDA 환경변수 설정 (zsh)
    % echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.zshrc
    % echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.zshrc
    % source ~/.zshrc
    
    // CUDA 설치 확인
    % nvcc --version
  
### 1-3. cuDNN(CUDA Deep Neural Network library)
- cuDNN(큐딘)은 NVIDIA 에서 개발한 딥러닝 라이브러리이다.
- cuDNN 은 병렬 컴퓨팅 플랫폼ㅇ르 기반으로 딥러닝 알고리즘의 효율적인 실행을 지원한다.
- cuDNN 은 TensorFlow, Pytorch,Caffe,Theano 등 다양한 딥러닝 프레임워크와 호환된다.
####
- cuDNN 은 CUDA 와 함게 사용되며, CUDA 설치 후 cuDNN 라이브러리를 설치하여 사용할 수 있다.
- 딥러닝 프레임워크 내에서 cuDNN 을 활성화하면 해당 프레임워크에서 제공하는 고수준 API 를 통해
  cuDNN 의 성능을 활용할 수 있다.
- cuDNN 은 딥러닝 모델의 학습과 추론 성능을 크게 향상시키는 도구로, NVIDIA GPU 를 사용하는 경우
  필수적인 라이브러리 이다.
####
- cuDNN 의 주 목적은 딥러닝 프레임워크에서 사용되는 신경망 연산을 가속화하는 것이다.
- 이를 통해 GPU 를 활용하여 딥러닝 모델의 학습 및 추론 속도를 크게 향상시킬 수 있다.
####
- 하드웨어 최적화: 최신 NVIDIA GPU 의 특성을 최대한 활용하도록 설계되었다.
- 메모리 관리: GPU 메모리 사용을 최적화하여 더 큰 모델을 처리할 수 있게 한다.
- 병렬 처리: 병렬 연산을 극대화하여 연산 속도를 높인다.
####
- [cuDNN download](https://developer.nvidia.com/cudnn)
####
    // cuDNN 설치
    % wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
    % sudo dpkg -i cuda-keyring_1.1-1_all.deb
    % sudo apt-get update
    % sudo apt-get -y install cudnn-cuda-12

    // 환경 변수 설정
    % vim ~/.zshrc
          export CUDNN_PATH=/usr/local/cuda-12.0
          export LD_LIBRARY_PATH=${CUDNN_PATH}/lib64:${LD_LIBRARY_PATH}
          export PATH=${CUDNN_PATH}/bin:${PATH}
    % source ~/.zshrc

    // 설정 확인
    % echo $CUDNN_PATH
    % echo $LD_LIBRARY_PATH
    % echo $PATH

    // pytorch 에서 cuDNN 사용 확인
    import torch
    print(torch.cuda.is_available())     // CUDA가 사용 가능한지 확인
    print(torch.backends.cudnn.enabled)  // cuDNN이 사용 가능한지 확인

### 1-4. torch
- cuda toolkit 은 torch 버전과도 호환이 되야 한다. [torch](https://pytorch.org/get-started/previous-versions/)
- [torch install](https://pytorch.org/get-started/locally/)
####
    % pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
    

    // 설치 확인
    % nvcc --version
