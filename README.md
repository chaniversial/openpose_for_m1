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

