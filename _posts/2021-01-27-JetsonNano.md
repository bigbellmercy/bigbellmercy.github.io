---
title: "JetsonNano 사용 관련"
date: 2021-1-27 01:21:00 +09:00
categories: JetsonNano
---
# Jetson Nano의 개요
Jetson Nano는 컴퓨터 그래픽 카드 제품으로 유명한 Nvidia[앤비디아] 사가 개발한 초소형 컴퓨터이다. 이 컴퓨터에는 Nvidia 사의 GPU(Graphic Processeing Unit, 그래픽 처리 장치)를 내장하고 있어서, '인공 신경망'(artificial neural network)을 빨리 처리할 수 있는 특징을 갖고 있다. Jeton Nano Devlopment Kit는 이 젯슨 나노의 보드를 캐리어 보드에 장착하여 판매되는 제품이며, 캐리어 보드에는 각종 커넥터들이 제공된다. 젯슨 나노의 기본 운영체제(OS)로는 Ubuntu 18.04가 설치되어 있고, Desktop Environment로는 Unity가 설치된다.

# Jetson Nano의 종류
Jetson Nano는 두 가지가 있는데, 하나는 원래의 제품으로서 메모리가 4GB인 제품이고, 다른 하나는 가격을 낮춘 제품으로서 메모리가 2GB인 제품이다.   

두 제품의 다른 점을 살펴 보면, Jetson Nano 4GB 제품은 USB 포트 4 개가 모두 USB3이고 카메라 커넥터가 2개 인데, Jetson Nano 2GB 제품은 USB 포트 2개는 USB2이고, 1개만 USB3이며, 카메라 커넥터가 1개이다. 또, 다른 점은 전원 단자인데, 4GB 제품은 DC 어댑터 단자이고, 2GB 제품은 USB-C 커넥터이다. 

젯슨 나노 4GB 제품에도 구 버전과 신 버전이 있는데, 구 버전은 카메라 커넥터가 1 개이고, 신 버전은 2 개이다.   

한편, 2GB 제품의 경우, WiFi 동글이 함께 제공된 제품이 있는데, 별도의 드라이버 설치 없이 잘 작동한다.


# Jetson Nano 2GB에서 한글 입력이 되도록 설정하기
JetsonNano 2GB는 운영체제가 Ubuntu가 아니라 LXDE 18.04를 쓰므로 한글 입력 설정이 좀 다르다.

1. 시작 > Preferences > Language Support 실행
2. Keyboard Input Method System: fcitx로 설정하고 창을 닫기
3. 재부팅
4. 화면 오른쪽 아래에 키보드 모양의 아이콘을 오른쪽 단추 누르고 Configure를 실행 
5. Global Config / Trigger Input Method의 첫째 단추를 누르고, 한영 전환하려는 키를 누름. 예) Shift + Space
6. 창을 닫고, 웹 브라우저나 오피스(LibreOffice Writer)를 실행하여 시험해 볼 것.

# 창을 화면의 좌측 또는 우측에 맞추기
맞추려는 창을 고르고 키보드의 Ctrl + Start key + Left 또는 Right key를 동시에 누른다. 여기서, Start key는 키보드 왼쪽 아래의 Window나 애플 로고가 그려져 있는 키이다.

# 키보드 단축키 안내 화면
'시작 키'(start key)(윈도우 로고나 애플 로고가 그려진 키)를 오래 누르면 키보드 단축

# 여러 화면을 쓰는 방법
웍스페이스(workspace)라는 기능을 쓰면 가상으로 여러 화면(screen)을 만들어 옮겨 다니며 쓸 수 있다.

시작 키를 누르고 apperance라는 검색어로 Appearance 앱을 실행한 뒤에, Behavior 탭에서 Enable workspaces를 활성화한다.

이렇게 하면 화면의 왼쪽 세로 메뉴 줄에 웍스페이스 아이콘이 나타나고 누르면 여러 화면들이 나타나고, 원하는 창을 끌어서 다른 화면으로 옮길 수 있으며, 원하는 웍스페이스 화면을 누르면 그 화면이 나타난다.

웍스페이스들을 옮겨다니는 단축키는 Ctrl + Alt + Left 또는 Right 화살표 키로 왼쪽/오른쪽으로 이동할 수 있고, Super (시작키) + Page Up 또는 Down으로 위/아래로 이동할 수 있다. 위/아래 이동도 Ctrl + Alt + Up / Down으로 바꾸고 싶다면, 'Keyboard' 설정에서 Navigation의 맨 아래 항목들에서 바꿀 수 있다.

# SD 메모리 카드 복제하기
리눅스의 `dd` 명령을 쓰면, 생각보다 쉽게, Jetson Nano의 SD 메모리 카드에 설치된 모든 내용을 그대로 떠서 일반 컴퓨터에 이미지 파일로 저장해 둘 수도 있고, 이를 다른 SD 카드에 복제할 수도 있다.
## SD 메모리 카드의 이미지 뜨기
1. 먼저, 원래의 SD 카드를 젯슨 나노에서 빼서 일반 리눅스 컴퓨터에 연결한다.
2. `sudo fdisk -l` 명령으로 이 SD 카드의 장치 이름을 알아 내야 한다. 이에는 `Disks` 소프트웨어도 도움이 된다. 예를 들어, 장치 이름이 `/dev/sdb1`라고 하자.
3. 이 장치 이름을 가지고, `sudo umount /dev/sdb1` 명령으로 장치를 언마운트 시킨다.
4. SD 카드의 이미지를 뜰 때, 빈 공간을 포함해서 SD 카드의 모든 용량을 그대로 뜨려면 아래 a)번을 하고(시간이 오래 걸림), 실제 파일이 차지하고 있는 만큼만 이미지를 뜨려면 아래 b)번을 한다.

a) 이 장치 이름을 가지고, `sudo dd if=/dev/sdb1 of=~/sd.img`처럼 명령하면, 시간이 지난 뒤에 `sd.img`라는 이름으로 컴퓨터의 홈 폴더에 SD 카드의 이미지 파일이 저장된다. 이제, SD 카드를 분리한다.

b) 파일 탐색기로 SD 카드의 디스크 아이콘에서 오른쪽 단추를 눌러서 Property를 실행하여, 이 디스크에 사용되는 용량을 알아 낸다. xxx GB used로 표시된다. (Contents: ... xxx GB가 아님에 유의한다). 그리고 다음의 명령으로 이미지를 뜬다. 여기서, bs=1M는 한번에 읽고 쓰는 용량의 단위이다. 이때, 아래의 `2048` 대신에 앞에서 알아낸 용량의 MB 크기를 입력한다.(아래 예에서는, bs가 1M로 설정되었기에 1M x 2048 = 2048 M = 2.048 GB가 된다)
> dd if=/dev/sdb1 of=~/sd.img bs=1M count=2048

## 이미지 파일로 SD 메모리 카드에 복제하기
1. 위에서 얻은 저장된 이미지를 새로운 SD 카드에 복제하려면, 새로운 SD 카드를 연결하고, `sudo fdisk -l` 명령으로 장치 이름을 알아 내는데, 장치 이름을 잘 못 알아내면 엉뚱한 하드 디스크 등에 덮어 써질 수 있으므로 무척 신중하게 확인해야 한다.
2. 예를 들어, 장치 이름이 `/dev/sda1`라면, `sudo umount /dev/sda1` 명령으로 장치를 언마운트 시킨다.
3. `sudo dd if=~/sd.img of=/dev/sdb1` 명령을 쓰면, 수십분이 지난 뒤에, `sd.img` 이미지 파일이 `/dev/sda1`의 SD 카드에 복제된다.
