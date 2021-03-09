---
title: "JetsonNano 사용 관련"
date: 2021-1-27 01:21:00 +09:00
categories: JetsonNano
---

# JetsonNano 2GB에서 한글 입력이 되도록 설정하기
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
