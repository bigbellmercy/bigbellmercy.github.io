---
title: "Docker 유용한 사용법들"
date: 2021-2-26 11:54:00 +09:00
categories: Docker
---

# Docker란?
Docker[다커/도커]라는 소프트웨어는 우분투(Ubuntu) 등의 리눅스 운영체제(OS)에서, 소프트웨어 프로그램들의 실행 환경들을 저장해 두었다가 다시 사용함으로써,
매번 프로그램 실행 환경들을 다시 설치 및 설정할 필요 없이, 원하는 실행 환경으로 바로 바꿀 수 있는 기술을 가진 컨테이너(container) 소프트웨어이다. 

# Image란?
프로그램 실행 환경을 파일로 저장해 둔 것. 인터넷에 올려 둘 수도 있고 컴퓨터에 내려 받을 수도 있다.

# Container란
컴퓨터에 내려 받은 이미지(image)를 가지고 실제로 사용되는 프로그램 실행 환경으로 만든 것. 하나의 이미지로 여러개의 다른 컨테이너들을 만들 수 있고, 그 컨테이너들은 하나의 같은 이미지의 실행 환경에서 비롯되었지만, 사용되면서 실행 환경이 서로 다르게 바뀔 수 있다. 

# Image 검색 명령
누군가 프로그램 실행 환경을 이미지(image) 파일로 만들어서 인터넷에 올려 놓은 것을 다음의 명령으로 찾을 수 있다. 아래 예는, ubuntu라는 검색어로 이미지를 찾는 명령이다.  
`sudo docker search ubuntu`

# Image 설치 명령
인터넷에서 원하는 이미지를 내 컴퓨터에 받아서 설치하는 명령이다. 아래 예는, ubuntu 이미지를 설치하는 명령이다.  
`sudo docker pull ubuntu`  

위 명령은 태그(tag)(일종의, 버전)를 지정하지 않았기에, 가장 최근(latest)의 버전을 설치한다.  
아래는 bionic(Ubuntu 18.04) 태그(tage)를 지정하여 설치하는 방법이다.  
`sudo docker pull ubuntu:bionic`

# 설치된 Image 목록 보기 명령
아래 명령으로 설치된 이미지들의 목록을 볼 수 있다.  
`sudo docker images`

# 설치된 Image 제거 명령
아래 명령으로 특정 이미지를 제거할 수 있다.
`sudo docker rmi <image_name>`

# Container 생성 명령
아래 예는, ubuntu라는 이미지를 본뜬(copied) 컨테이너(container)를 하나 만든다. 여기서, -it는 interactive, tty(text)의 옵션인데, 이게 없으면 컨테이너가 만들어졌다가 바로 종료된다.  
`sudo docker run -it ubuntu`

컨테이너가 실행되면 root 사용자로 로그인 되고 #으로 끝나는 리눅스 프롬프트가 표시된다. 이제부터, 이 프로그램 실행 환경을 사용하면 된다.

참고로, 하나의 같은 이미지로 여러 컨테이너들을 따로 실행하는 것이 가능하다.

## Container에 이름을 붙여서 생성하는 방법
컨테이너에 이름을 붙여서 생성해 놓으면, 나중에 이 이름을 가지고 쉽게 다시 시작할 수 있다.
>sudo docker run -it --name=<container_name> ubuntu

# Container 종료 명령
그 컨테이너 속의 터미널에서 `exit` 명령을 그 컨테이너를 종료할 수 있다.

또는, 다른 터미널에서 다음 명령으로 특정 컨테이너를 종료할 수 있다. 여기서, <container_id/name>는 `sudo docker ps` 명령으로 알 수 있으며, id는 앞의 몇 글자만 적어도 된다. 
`sudo docker stop <container_id/name>`

**주의. 종료된 컨테이너는 아예 사라지는 것이 아니라, 그 마지막 환경 그대로 디스크에 남아 있고, 나중에 다시 재개(재실행)하여 이어서 작업할 수 있다.**

# Container 목록 보기 명령
터미널을 따로 시행한 뒤에 아래 명령을 치면, 현재 실행 중인 컨테이너들의 목록을 불 수 있다.  
`sudo docker ps`

아래 명령은, 현재 실행 중이지는 않지만 중단된 컨테이너들의 목록도 보여 준다.
`sudo docker ps -a`

# Container 재개(재실행) 명령
아래 명령으로 중단(stop)된 컨테이너를 이어서 다시 실행할 수 있다. 여기서, <container_id/name>는 `sudo docker ps -a`로 알 수 있고, id는 앞의 몇 글자만 적어도 된다. 이때, 앞에서 컨테이너 생성 시에 이름을 붙였다면 id 대신에 쓸 수 있다.  
`sudo docker start -i <container_id or name>`

# Container 제거 명령
아래 명령으로 특정 컨테이너를 제거할 수 있다. 여기서, <container_id/name>는 `sudo docker ps -a`로 알 수 있고, id는 앞의 몇 글자만 적어도 된다.
`sudo docker rm <container_id/name>`
