---
title: "Catkin 유용한 사용법들"
date: 2021-2-22 15:33:00 +09:00
categories: ROS
---

# Catkin 빌드 방식의 두 종류
Catkin의 소스 코드를 빌드하는 방법이 여러가지가 있는데, 하나는 `catkin buil`이고, 다른 하나는 `catkin_make`임. 또, `catkin make`인가도 있음.
   
특정 ROS 패키지가 둘 중의 어느 하나에서만 빌드가 된다면, catkin_ws 말고 그 옆에 catkin_ws2 이런식으로 폴더를 하나 더 만들고, 다른 빌드 방식으로 빌드를 해 보면 될 수 있음.

모든 ROS 패키지들을 처음부터 빌드하고 싶으면 catkin_ws 밑의 빌드 폴더를 지우고 빌드할 것.

특정 ROS 패키지를 지우고 싶으면 catkin_ws/src 밑의 해당 폴더를 지우던가 다른 임시 폴더로 옮기면 됨.

굳이, ROS 패키지를 항상 소스 코드로 받아서 빌드할 필요는 없음. 그 패키지의 소스 코드를 수정할 필요가 없다면, `sudo apt install ros-melodic-rviz` 등의 명령으로 설치 파일을 바로 설치해서 쓸 수 있음.
단, 내가 수정하지는 않지만, 다른 소스 코드가 빌드가 되려면 특정 패키지를 소스 코드로 요구하는 경우가 있음. 예를 들어, rviz의 소스 코드가 다른 패키지들에서 필요할 때가 있음.

`rviz`의 경우 빌드 시에 오류가 난 적이 있는데, GitHub에 가서 최신의 코드를 catin_ws/src 밑에 복제(clone)한 뒤에 빌드하니 됨.