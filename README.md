# Image Interpolation with RIFE HDv3

## 프로젝트 설명  
2장의 이미지를 입력, Pretrained RIFE HDv3 모델로 부드러운 중간 프레임을 생성(= Interpolation)하고, 순방향(1→30) 및 역방향(30→1)으로 두 이미지를 이어붙여 2초 길이의 무한 루프 GIF를 출력하는 Jupyter Notebook(.ipynb) 기반 프로젝트

## Installation
```bash
# 1) 리포지토리 클론
git clone <your-repo-url>
cd <your-repo>

# 2) Conda 환경 생성 & 활성화
conda create -n interpolation python=3.8 -y
conda activate interpolation

# 3) 필수 패키지 설치
pip install torch torchvision pillow opencv-python imageio

# 4) RIFE HDv3 저장소 클론 및 가중치 배치
git clone https://github.com/hzwer/ECCV2022-RIFE.git
mkdir -p ECCV2022-RIFE/train_log
# → 사전학습 가중치(fl ownet.pkl, IFNet_HDv3.py, RIFE_HDv3.py)를
#    ECCV2022-RIFE/train_log 폴더에 복사

# 5) Jupyter Notebook 실행
jupyter notebook imageinterpolation.ipynb
````

## Usage
1. `imageinterpolation.ipynb`에서 순서대로 셀을 실행
2. `1.png`, `30.png` 파일을 노트북이 실행되는 디렉터리에 위치
3. 마지막 셀 실행 후 `Z-Full.gif`가 생성

## 기능 및 의의
* **재귀적 보간**: Vision-Scale Fusion 모델(IFNet 기반 RIFE HDv3)의 `inference()`를 재귀적으로 호출하여 총 28개의 중간 프레임 생성
* **순·역방향 루프**: 1→30→1 프레임 시퀀스를 구성해 자연스러운 왕복 애니메이션
* **자동 패딩/크롭**: 입력 크기를 32의 배수로 맞춰 모델 내부 업/다운샘플 안정성 확보
* **고정 출력 크기**: 최종 GIF를 226×192 픽셀로 리사이즈
* **무한 루프**: `loop=0` 설정으로 GIF가 영구 반복 재생

## Requirements
* Python 3.8
* PyTorch 1.x (+ CUDA 설치 시 GPU 사용 가능)
* OpenCV (`opencv-python`), Pillow (`PIL`), ImageIO (`imageio`)

## License
MIT License
