---
title: "Raspberry Pi에서 ROS 사용 관련"
date: 2020-9-24 17:41:00 +09:00
categories: RPi
---

# 목적
Raspberry Pi 사용 관련 유용한 정보.

# 실행 환경
아래 방법은 다음의 실행 환경에서 수행되었습니다.   
Raspberry Pi 3 Model B v1.2, Ubuntu Mate 64bit 18.04, ROS melodic   
실행 환경이 다를 경우, 시기가 오래 지난 경우, 아래 방법이 잘 되지 않을 수도 있습니다.   

# Raspberry Pi에 Ubuntu 설치하기
## 라즈베리파이 사이트의 '시작하기' 안내에 따라 설치하기   
아래 주소의 안내대로 'Raspberry Pi Imager'라는 소프트웨어로 SD 메모리에 여러 리눅스 종류들을 설치할 수 있음   
https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started   

### 라즈비안(Raspbian) 설치 시도: 실패
라즈비안 설치는 되나 ROS 일부 패키지 오류 발생   
ROS 기본 설치는 되고 usb_cam 패키지도 설치되었으나, image_view가 필요해서 이것도 설치했으나,   
usb_cam 실행 시 Gtk v2.0, v3.0 충돌 관련 오류가 나면서 진행이 안되고, 해결법도 인터넷에 잘 안나옴.   

### Ubuntu Core 18 설치 시도: 실패
설치는 되나 GUI 환경이 안 나타나고 검은 명령 줄로 나타나 포기.   

### Ubuntu 20.04 LTS 설치: 실패
설치는 되나 GUI 환경이 안 나타나고 검은 명령 줄로 나타나 포기.   

### Ubuntu Mate 18.04 설치: 성공. 그러나 성능이 너무 느림.
Ubuntu Mate ARM 64bit, 또는 32bit를 설치 가능. Ubuntu Mate 사이트에서 .img.xz 파일을 받아 dd 명령으로 SD 카드에 복사하여 설치(인터넷 검색할 것).   
ROS melodic 설치는 아래 주소를 사용. Melodic보다 상위 판인 noetic을 설치하면 ROS 패키지들이 현재는 아직 지원이 덜 된다는 얘기가 있음.   
http://wiki.ros.org/melodic/Installation/Ubuntu   
위 주소는 '라즈베리 파이 전용 ROS 설치법' 페이지가 아닌 일반적인 설치법 페이지이며, 패지지 설치시 아래처럼 편하게 설치할 수가 있음   
sudo apt install ros-melodic-usb-cam   
만약, '라즈베리 파이 전용 ROS 설치법'으로 ROS를 설치하면 패키지를 설치할 때, rosinstall_generator 명령을 써서 복잡해지고, 잘 설치가 안될 때도 있음.   
USB 웹 카메라를 연결하고 usb_cam을 실행했는데 컴퓨터가 멎고 반응이 없음. 자체 소프트웨어 갱신 앱에서 부분 업데이트를 한 뒤에 빨라짐 (커널 변경 때문인듯)
