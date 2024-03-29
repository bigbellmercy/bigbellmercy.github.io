---
title: "Docker 유용한 사용법들"
date: 2021-2-26 11:54:00 +09:00
categories: Docker
---

# Docker란?
Docker[도커/다커]라는 소프트웨어는 우분투(Ubuntu) 등의 리눅스 운영체제(OS)에서, 소프트웨어 프로그램들의 실행 환경들을 저장해 두었다가 다시 사용함으로써,
매번 프로그램 실행 환경들을 다시 설치 및 설정할 필요 없이, 원하는 실행 환경으로 바로 바꿀 수 있는 기술을 가진 컨테이너(container) 소프트웨어이다. 

# 기본 개념
## Image란?
프로그램 실행 환경을 파일로 저장해 둔 것. 인터넷에 올려 둘 수도 있고 컴퓨터에 내려 받을 수도 있다.

## Container란
컴퓨터에 내려 받은 이미지(image)를 가지고 실제로 사용되는 프로그램 실행 환경으로 만든 것. 하나의 이미지로 여러개의 다른 컨테이너들을 만들 수 있고, 그 컨테이너들은 하나의 같은 이미지의 실행 환경에서 비롯되었지만, 사용되면서 실행 환경이 서로 다르게 바뀔 수 있다. 

# Docker 설치 및 사용 준비
도커(docker)를 설치하는 방법 중의 하나는 다음 두 명령을 실행하는 것이다.  
curl -fsSL get.docker.com -o get-docker.sh  
sudo sh get-docker.sh  

만약, 도커를 사용하는 명령들 앞에 sudo를 쓰지 않아도 되게 설정하려면, 다음 두 명령을 실행한다. 따라서, 뒤의 설명에서는 `sudo`를 명령 앞에 붙이는 것을 생략한다.  
>sudo groupadd docker  
>sudo usermod -aG docker $USER

운영체제를 로그아웃 한 뒤에 다시 로그인 한다. 

# Image 사용 관련 명령들
## Image 검색 명령
누군가 프로그램 실행 환경을 이미지(image) 파일로 만들어서 인터넷에 올려 놓은 것을 다음의 명령으로 찾을 수 있다. 아래 예는, ubuntu라는 검색어로 이미지를 찾는 명령이다.  
`docker search ubuntu`

## Image 설치 명령
인터넷에서 원하는 이미지를 내 컴퓨터에 받아서 설치하는 명령이다. 아래 예는, ubuntu 이미지를 설치하는 명령이다.  
`docker pull ubuntu`  

위 명령은 태그(tag)(일종의, 버전)를 지정하지 않았기에, 가장 최근(latest)의 버전을 설치한다.  
아래는 bionic(Ubuntu 18.04) 태그(tage)를 지정하여 설치하는 방법이다.  
`docker pull ubuntu:bionic`

## 설치된 Image 목록 보기 명령
아래 명령으로 설치된 이미지들의 목록을 볼 수 있다.  
`docker images`

## 설치된 Image 제거 명령
아래 명령으로 특정 이미지를 제거할 수 있다.  
`docker rmi <image_name>`

단, 그 이미지를 쓰는 컨테이너가 있다면 지울 수 없다. 따라서, 한 이미지를 지우고 싶다면, `docker ps -a` 명령으로 그 이미지를 쓰는 컨테이너들을 모두 지워야 지울 수 있다.

# Container 사용 관련 명령들

## Container 생성 명령

**숙지사항**
- **도커 이미지를 가지고 컨테이너를 만들고(docker run 명령) 종료해도 그 컨테이너는 사라지는 것이 아니라 다시실행(docker start 명령 사용)해서 연속해서 쓰는 것임에 유의해야 한다.**  
- **물론, 하나의 이미지를 가지고 여러 컨테이너들을 만들 수는 있지만, 지우지 않으면 계속 저장 장치에 남아 있으니 안 쓰는 건 지워야 한다(docker rm 명령 사용).**  

아래 예는, ubuntu라는 이미지를 본뜬(copied) 컨테이너(container)를 하나 만든다. 여기서, -it는 interactive, tty(text)의 옵션인데, 이게 없으면 컨테이너가 만들어졌다가 바로 종료된다. 
여기서, ubuntu:v1.0 이런식으로 태그를 붙이면 해당 태그의 이미지로 컨테이너가 만들어지고, 태그를 생략하면 최근의 태그가 사용된다.  
>docker run -it ubuntu  

또는

>docker run -it ubuntu:v1.0  

여기서, -it 옵션은 컨테이너를 만든 뒤에 터미널 창을 연결하라는 뜻이다.  

컨테이너가 실행되면 root 사용자로 로그인 되고 #으로 끝나는 리눅스 프롬프트가 표시된다. 이제부터, 이 프로그램 실행 환경을 사용하면 된다.

참고로, 하나의 같은 이미지로 여러 컨테이너들을 따로 실행하는 것이 가능하다.

### Container 생성 시의 옵션들

### 일시 생성
다음의 옵션을 넣으면 컨테이너가 종료되면 흔적을 모두 지워 사라지게 한다. 이 옵션을 넣지 않으면 컨테이너가 종료되어도 중단 상태로 남아있게 되며, 다시 재개할 수 있다.
>--rm

#### 외부 장치 자동 사용 옵션
다음의 옵션을 추가하면 외부의 장치들(조이스틱 등)을 컨테이너 속에서 자동으로 쓸 수 있다.  
>--privileged

#### Container에 이름을 붙여서 생성하는 옵션
컨테이너에 이름을 붙여서 생성해 놓으면, 나중에 이 이름을 가지고 쉽게 다시 시작할 수 있다.
>docker run -it --name=<container_name> ubuntu

#### 외부 폴더를 사용하는 옵션
하나의 컨테이너는 가상의 독립적인 컴퓨터이기에 컨테이너 밖의 호스트 환경의 폴더는 기본적으로 쓸 수 없다. 
다음의 명령을 쓰면 호스트 환경의 폴더를 컨테이너 속에서 연결하여 쓸 수 있다.  

>-v /external_path:/internal_path

읽기 전용이라면,
>-v /external_path:/internal_path:ro

읽기 쓰기를 명시하려면,
>-v /external_path:/internal_path:rw

#### 사용자 ID를 지정하는 옵션
위에서 외부 폴더를 사용한다면, 그 폴더의 소유자와 같은 ID를 써서 컨테이너로 들어가면 사용자가 일치되어 편리하므로, 아래 명령처럼, 컨테이너 밖의 사용자 ID를 그대로 쓰게 할 수 있다.

>-e LOCAL_USER_ID="$(id -u)"

#### GUI를 쓰게 하는 옵션
하나의 컨테이너는 가상의 실행 환경이 때문에 기본적으로 터미널에서만 작동되고 GUI(Graphic User Interface) 환경을 가지고 있지 않다.  
다음의 옵션을 써야 소프트웨어들의 GUI가 컨테이너 밖의 호스트 컴퓨터의 화면에 나타내질 수 있다. 

>-e DISPLAY=$DISPLAY \
>-v "/tmp/.X11-unix:/tmp/.X11-unix:rw" \

한편, 컨테이너를 실행하기 전에 아래 명령을 실행해 줘야, 컨테이너 속에서 실행된 GUI 창들이 컨테이너 밖의 호스트 컴퓨터의 화면에 나타날 수 있다. 
이 명령은 아무 사용자나 XServer에 접속하게 허용하여 이것이 가능하게 하는 명령이다.  
>xhost +

#### Qt GUI가 쓰인 소프트웨어를 실행하는 옵션
Qt GUI가 쓰인 소프트웨어는 연산량이 크므로 문제가 될 때에는 아래 옵션을 쓴다.  
>--env="QT_X11_NO_MITSHM=1"

##### 컨테이너 속에서 GUI 글 편집기 Gedit 실행
컨테이너 속에서 '글 편집기'(text editor)인 `nano`나 `vi`나 `vim`을 쓸 수도 있지만,
이들은 글(text) 방식의 편집기 이기 때문에 불편한 사람은, 
다음의 방법으로 GUI 방식의 대표적인 글 편집기인 `gedit`를 설치해 쓸 수 있다.  
>sudo apt update

>sudo apt install gedit  
설치 중간에 사용 언어와 키보드 종류를 물어보면 엔터 키를 눌러 넘긴 뒤에 English (US)를 고른다.  

그리고, 컨테이너를 종료한 뒤에 다음 명령으로 GUI 화면이 나타날 수 있게 해 줘야 한다.  
>xhost +

`docker start` 명령으로 그 컨테이너를 다시 실행한 뒤에,

빈 파일을 열려면 다음 명령을,
>gedit

어떤 파일을 열려면 다음 명령을 실행한다.
>gedit file_name

#### GPU를 쓰게 하는 옵션
>--gpus all

#### Host 이름 지정 옵션
다음 명령으로 컨테이너의 호스트 컴퓨터의 이름을 그대로 컨테이너에 적용시킬 수 있다.
>--hostname $(hostname)

#### 인터넷 포트 번호 연결 옵션
아래 명령으로 호스트의 14570 UDP 포트를 컨테이너 속에 같은 번호로 연결시킬 수 있다.
>-p 14570:14570/udp

아래 명령으로 호스트의 127.0.0.1 (로컬 호스트) 주소의 80번 TCP 포트를 컨테이너의 8080 번으로 연결시킬 수 있다.   
> -p 127.0.0.1:80:8080/tcp

#### bash 셸 사용 옵션
다음처럼 마지막에 bash라고 적으면 컨테이너가 생성된 뒤에 터미널에 bash 셸이 사용된다.
>docker run -it ubuntu bash  

## Container 종료 명령
그 컨테이너 속의 터미널에서 `exit` 명령을 그 컨테이너를 종료할 수 있다.

또는, 다른 터미널에서 다음 명령으로 특정 컨테이너를 종료할 수 있다. 여기서, <container_id/name>는 `sudo docker ps` 명령으로 알 수 있으며, id는 앞의 몇 글자만 적어도 된다. 
`docker stop <container_id/name>`

**주의. 종료된 컨테이너는 아예 사라지는 것이 아니라, 그 마지막 환경 그대로 디스크에 남아 있고, 나중에 다시 재개(재실행)하여 이어서 작업할 수 있다.**

## Container 목록 보기 명령
터미널을 따로 시행한 뒤에 아래 명령을 치면, 현재 실행 중인 컨테이너들의 목록을 불 수 있다.  
`docker ps`

아래 명령은, 현재 실행 중이지는 않지만 중단된 컨테이너들의 목록도 보여 준다.
`docker ps -a`

## Container 재개(재실행) 명령
아래 명령으로 중단(stop)된 컨테이너를 이어서 다시 실행할 수 있다. 여기서, <container_id/name>는 `sudo docker ps -a`로 알 수 있고, id는 앞의 몇 글자만 적어도 된다. 이때, 앞에서 컨테이너 생성 시에 이름을 붙였다면 id 대신에 쓸 수 있다.  
`docker start -i <container_id or name>`

## Container 제거 명령
아래 명령으로 특정 컨테이너를 제거할 수 있다. 여기서, <container_id/name>는 `sudo docker ps -a`로 알 수 있고, id는 앞의 몇 글자만 적어도 된다.
`docker rm <container_id/name>`

## Container 재시동 명령
컨테이너 속 Ubuntu를 재시동(reboot)하고 싶으면, 컨테이너에서 exit 명령으로 나온 뒤에, 아래 명령을 한다.
>docker restart <container_name>

다음 명령으로 터미널을 컨테이너에 접속시킨다.
>docker start -i <container_name>

## Container 안이나 밖으로 파일 복사하기
호스트에 있는 파일을 컨테이너로 복사하는 방법은 다음과 같다.
>docker cp <복사할 파일 경로> <컨테이너 이름>:<컨테이너 내부 파일 경로>

반대로, 컨테이너의 파일을 호스트로 복사하는 방법은 다음과 같다.  
>docker cp <컨테이너 이름>:<컨테이너 내부 파일 경로> <복사할 파일 경로> 

## 컨테이너에 새 터미널 하나 더 접속하기
실행중인 컨테이너에 이미 터미널이 연결되어 있더라도, 다음의 명령으로 새 터미널을 접속하게 할 수 있다.  
루트 계정으로 접속하려면 아래와 같다.  
>docker exec -it <container_name_or_id> bash

사용자 계정으로 접속하려면 아래와 같다.  
> docker exec -u <user_name> -it <container_name_or_id> bash


# 도커 고급 명령

## 도커 이미지 및 컨테이너 사용 용량 확인 방법
>docker system df -v

## 컨테이너 밖에서 컨테이너 속에 명령하기
만약, 컨테이너 밖의 호스트 환경에서 my_container라는 이름의 컨테이너에서 글 편집기인 gedit를 실행하려면 다음 명령을 쓴다.   
>docker exec my_container gedit

## 컨테이너를 가지고 이미지 만들기
아래 명령은 <container_id_or_name>이라는 id나 이름의 컨테이너로 <image_name>:<tag_name>라는 이미지를 만든다. 여기서, 태그 이름인 :<tag_name>은 뺄 수 있다.  
>docker commit <container_id_or_name> <image_name>:<tag_name> 

참고로, 태그 이름으로서, 이미 있던 latest를 붙여도 commit이 되었고, 대신에 image의 ID가 바뀌었다.  

commit 시의 설명 메시지를 추가하려면 다음과 같이 적는다.  

>docker commit -m "commit message" <container_id_or_name> <image_name>:<tag_name> 

**참고**
이렇게 한 이미지로부터 생성된 컨테이너로 새 이미지를 만들었어도, 이 두 이미지들이 차지하는 용량이 원래보다 두 배가 되지는 않고, 이미지를 공유하는 부분은 그대로 두고 차이가 나는 부분만 새 이미지에 저장된다. 그러나 docker images 명령을 하면 각 이미지의 크기는 공유하는 부분을 모두 포함해서 용량 크기를 보여준다.

# Docker 스크립트 사용 방법
## Docker 스크립트의 개념
한 소프트웨어 환경에 소프트웨어들을 설치하는 명령들을 담은 스크립트 파일을 작성한 뒤에, 이 스크립트 파일을 가지고 이미지를 만들 수도 있다. 이렇게 하면, 설치되는 소프트웨어의 일부를 바꾸어서 다시 이미지를 만들어야 할 때에, 이 일을 자동화할 수 있어서 편리하다.

## Dockerfile 빌드 명령
설치 스크립트를 Dockerfile이라는 글 파일로 저장하였다면 이를 가지고 도커 이미지를 만드는 명령은 다음과 같다.
>docker build - < Dockerfile

## Dockerfile 작성 방법
다른 도커 이미지를 기반으로 이미지를 만든다면, 다음처럼 첫 줄에 적는다.
>FROM ros:foxy-ros-base  

그 뒤에 설치를 위해 필요한 각종 명령들을 다음의 예처럼 RUN 다음에 적는다.
>RUN apt-get update  

이 글 파일을 Dockerfile이라는 이름으로 저장한다.

## 이미지를 파일로 만들기
도커 이미지를 .tar 파일로 만드는 방법으 아래와 같다. 여기서, 이미지 이름은 여러개 적을 수 있다. 아래 명령 중간에 부등호 '>'가 있음에 유의하자.  
>docker save <image_name> > <image_file_name.tar>

## 이미지나 파일을 불러오기
다음 명령으로 이미지 .tar 파일을 도커에 불러온다.  
>docker load < <image_file_name.tar>

## 컨테이너를 파일로 만들기
컨테이너를 파일로 만들 수는 있지만, 다시 불러올 때에는 특정한 명령들을 추가로 넣어주어야 정상 실행이 되므로, 고급 사용자가 아니면 추천하지 않는다. 아래 명령 중간에 부등호 '>'가 있음에 유의하자.
>docker export <container_name_or_id> > <container_file_name.tar>

## 컨테이너 파일을 불러오기
컨테이너 파일을 다시 불러올 때에는 아래 명령으로 되지만, 실행이 정상적으로 되지 않으므로, 아래 명령에 특정한 명령들을 추가로 넣어주어야 하므로, 고급 사용자가 아니면 추천하지 않는다.
>docker import <container.tar> <image_name:sddd_name>

