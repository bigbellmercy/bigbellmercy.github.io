---
title: "JetsonNano 2GB 사용 관련"
date: 2021-1-27 01:21:00 +09:00
categories: JetsonNano
---

# 1. JetsonNano 2GB에서 한글 입력이 되도록 설정하기
JetsonNano 2GB는 운영체제가 Ubuntu가 아니라 LXDE 18.04를 쓰므로 한글 입력 설정이 좀 다르다.

1. 시작 > Preferences > Language Support 실행
2. Keyboard Input Method System: fcitx로 설정하고 창을 닫기
3. 재부팅
4. 화면 오른쪽 아래에 키보드 모양의 아이콘을 오른쪽 단추 누르고 Configure를 실행 
5. Global Config / Trigger Input Method의 첫째 단추를 누르고, 한영 전환하려는 키를 누름. 예) Shift + Space
6. 창을 닫고, 웹 브라우저나 오피스(LibreOffice Writer)를 실행하여 시험해 볼 것.
