---
title: "윈도우 서버 Windows Server"
date: 2022-6-13 11:45:00 +09:00
categories: Windows
---

# 개요
AWS 등의 가상 컴퓨터 환경에서는 일반 Windows 운영체제 대신에 Windows Server를 쓰므로, 그 특별한 사용 방법들을 기술하고자하 함.

# Windows Server 2019의 인터넷 익스플로러 문제
인터넷 익스플로러를 쓰면 보안 문제로 접속이 되지 않아서, 크롬 등의 다른 브라우저도 설치할 수 없는 문제가 있음.   
Server Manager를 실행하고 Properties에서 IE Enhanced Security Configuration을 On에서 Off로 바꾸면, 문제가 해결됨.

