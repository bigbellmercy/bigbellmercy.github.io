---
title: "Docker 유용한 사용법들"
date: 2021-2-26 11:54:00 +09:00
categories: Docker
---

# Docker란?
Docker[다커/도커]라는 소프트웨어는 우분투(Ubuntu) 등의 리눅스 운영체제(OS)에서, 소프트웨어 프로그램들의 실행 환경들을 저장해 두었다가 다시 사용함으로써,
매번 프로그램 실행 환경들을 다시 설치 및 설정할 필요 없이, 원하는 실행 환경으로 바로 바꿀 수 있는 기술을 가진 컨테이너(container) 소프트웨어이다. 

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
설치된 이미지들의 목록을 본다.  
`sudo docker images`

# Image 실행 명령
아래 예는, ubuntu라는 이미지를 실행하여 컨테이너(container)를 하나 만든다. 여기서, -it는 interactive, tty(text)의 옵션인데, 이게 없으면 컨테이너가 만들어졌다가 바로 종료된다.  
`sudo docker run -it ubuntu`

참고로, 하나의 같은 이미지로 여러 컨테이너들을 따로 실행하는 것이 가능하다.

# 실행 중인 Container 목록 보기 명령
실행 중인 컨테이너들의 목록을 본다.  
`sudo docker ps`
