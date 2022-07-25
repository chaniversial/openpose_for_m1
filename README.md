# M1 MacBook Air에서 Openpose를 수행하는 방법입니다.
제가 수행했던 맥북의 사양은 다음과 같습니다.
OS: Monterey 12.5
CPU: M1(8코어 중 4코어는 성능코어, 4코어는 효율 코어입니다)
RAM: 8G
SSD: 256G

주 작업은 터미널 창에서 진행해야 합니다. 그렇기에 Command + Space 를 자주 사용해주시기 바랍니다.

# 환경 구축
저는 https://take6shin-tech-diary.com/openpose-tensorflow2/ 홈페이지를 참조하여 진행하였습니다.
하지만, 해당 홈페이지에서 오류가 있는 점을 발견하고, 이를 해결하는 방안을 적겠습니다.

가상환경에서 진행해야 하기 때문에, ananconda홈페이지에서 파일을 다운 받습니다.

https://www.anaconda.com/products/distribution#Downloads
<img width="1552" alt="스크린샷 2022-07-25 오전 9 55 34" src="https://user-images.githubusercontent.com/101043303/180673987-3069117a-62fa-42b7-b604-4c25ff93adef.png">

위의 그림에서 본인의 환경에 맞게 고르시면 되겠습니다. 저의 경우 M1 MacBookAir이기 때문에 64-Bit (M1) Graphic Installer를 다운받겠습니다.

설치과정에 있어서는 그냥 확인만 계속 눌러서 설치하시면 됩니다.

추후 설치가 완료되면, 터미널 창을 새롭게 열어보고 다음과 같이 뜨면 성공적으로 설치가 된 것입니다.

<img width="682" alt="스크린샷 2022-07-25 오전 9 58 43" src="https://user-images.githubusercontent.com/101043303/180674189-8f87d0fe-0e1b-4654-9de1-5980dafa5a65.png">

base가상환경에서 터미널 창이 뜬 것을 확인할 수 있습니다.


여기서 부터 새로운 가상환경을 만들 것입니다. 

conda create -n openpose python=3.8
명령어를 입력하면 다음과 같이 실행됩니다. openpose라는 이름의 가상환경을 만들 것인데 python 버전은 3.8로 합니다. 원래 3.7버전을 선호하였는데, m1부터는 python 3.8이 제일 괜찮았습니다. (제 개인적인 피셜이지만, 이 환경을 구축하는데 있어서는 전 3.8이 문제가 없었습니다.)

<img width="697" alt="스크린샷 2022-07-24 오후 12 29 55" src="https://user-images.githubusercontent.com/101043303/180674290-1585c62a-09d7-4361-a69b-10233d43c3d6.png">

<img width="697" alt="스크린샷 2022-07-24 오후 12 30 18" src="https://user-images.githubusercontent.com/101043303/180674763-330f70bf-ab6c-463e-a268-a4002ddf3afd.png">

y를 누르시면 됩니다 ^ㅁ^

가상환경이 다 만들어지면 다음과 같이 창이 뜹니다. 그리고 저는 openpose라는 이름의 가상환경을 만들었기 때문에 conda activate openpose라는 명령어를 통해서 가상환경을 활성화 시켜줍니다.

<img width="697" alt="스크린샷 2022-07-24 오후 12 33 29" src="https://user-images.githubusercontent.com/101043303/180675009-0ac91e34-7474-4eaf-8c34-31f575cc384f.png">

이제부터 실제 필요한 파일을 다운받고 더 필요한 작업을 시작하겠습니다.

우선 brew를 설치해야 합니다. brew를 설치하는 방법은 https://brew.sh/index_ko 에 나와있습니다.

하지만, 이를 직접 읽어보고 나에게 필요한 부분을 찾는 것은 어렵기때문에, 다음의 방안을 따라해주시면 됩니다.

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
이 명령어만 입력하면 brew가 설치되며 설치가 완료되면 터미널 창에 brew를 입력하여 봅니다.
만약  zsh: command not found: brew 관련 오류가 발생할 시 다음의 명령어를 진행해주시면 됩니다.

sudo vim ~/.zshrc

그럼 다른 기존에 있던 내용이 있을 수 있고, 없을 수도 있는데, 신경 쓰지 말고 가장 아랫 줄에 다음의 구문을 추가하시면 됩니다.

export PATH=/opt/homebrew/bin:$PATH

위의 내용을 복사하고 붙여넣기 해도 문제가 없습니다. 해당 명령어를 입력하고 ESC키를 누르고 :wq를 입력하면 저장이 됩니다.

<img width="682" alt="스크린샷 2022-07-25 오후 1 58 27" src="https://user-images.githubusercontent.com/101043303/180701648-a4a283db-ddb7-4889-9050-36951455b370.png">

그리고 sync명령어를 통해 현재 내용이 반영될 수 있도록 합니다.

<img width="682" alt="스크린샷 2022-07-25 오후 1 58 58" src="https://user-images.githubusercontent.com/101043303/180701703-cedd4f87-5c7d-4881-b607-b30aacb4d6b4.png">

그리고 brew install wget를 통해 wget 라이브러리를 설치할 수 있도록 합니다.

새로운 터미널 창을 열고 다음과 같이 입력합니다.

conda activate openpose

mkdir workspace

git clone https://github.com/gsethi2409/tf-pose-estimation.git

cd tf-pose-estimation

conda install numba scipy

pip install -r requirements.txt

conda install -c conda-forge tensorflow

conda install swig

cd tf_pose/pafprocess

swig -python -c++ pafprocess.i && python3 setup.py build_ext --inplace

cd ../..

conda install -c conda-forge opencv

pip3 install git+https://github.com/adrianc-a/tf-slim.git@remove_contrib

cd models/graph/cmu

bash download.sh

cd ../../..

pip3 install tensorflow-macos==2.7.0

pip3 install opencv-python

그리고 저는 웹캠을 이용하여 진행할 것이기에 다음의 명령어를 사용해주시면 됩니다.

python3 run_webcam.py --model=mobilenet_thin --resize=432x368 --camera=0

git 명령어를 사용할 때, git이 깔려있지 않은 경우도 있습니다. 그럴 경우 다음의 창이 뜨게 되는데, 그냥 설치 누르시면 됩니다. 그러고 다시 실행하면 됩니다.

<img width="610" alt="스크린샷 2022-07-24 오후 12 36 41" src="https://user-images.githubusercontent.com/101043303/180701449-5aa6ebc1-8d3d-40d4-bc8f-ee62dda1264a.png">

