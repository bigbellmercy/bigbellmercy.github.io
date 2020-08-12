---
title: "Realsense 카메라 처음 작동 방법"
date: 2020-8-12 18:56:00 +09:00
categories: ROS
---

# 목적
Intel Realsense 카메라를 처음으로 ROS 상에서 작동시켜서 화면에 카메라의 영상과 깊이 정보를 표시하기.

# 실행 환경
아래 방법은 다음의 실행 환경에서 수행되었습니다.   
Ubuntu 18.04, ROS melodic, realsense SDK, realsense ROS wrapper, D435i depth camera   
실행 환경이 다를 경우 아래 방법이 잘 되지 않을 수도 있습니다.

# 방법
다음의 두 가지 방법 모두 가능하며, 한 방법을 선택해서 실행할 것.   
리얼센스 관련 소프트웨어가 모두 설치가 되어 있어야 하며, 설치 방법은 리얼센스 사이트를 참조.   

## A. Point cloud 영상 보기
1. realsense sdk가 설치된 상태에서, D435i 같은 센서를 PC에 연결.
2. 새 터미널에서 roscore 실행:
> roscore
3. 된 상태에서, 새 터미널에서 다음 명령을 실행:
> roslaunch realsense2_camera rs_camera.launch align_depth:=true
4. 새 터미널에서 rviz(시각화 도구)를 실행:
> rviz
5. rviz의 Displays 영역에서 Global Options/Fixed Frame이 map이 아닌 camera_link이어야 함.
   (이렇게 해야 Global Status가 Error 상태에서 OK 상태가 됨)
6. rviz 왼쪽 아래의 Add를 누르고 By display type/PointCloud2를 고르고 OK를 누름.
7. rviz/Displays/PointCloud2/Topic의 오른쪽 빈 곳을 누르고 /camera/depth/color/points를 입력 또는 선택.
8. rviz의 오른쪽 검은 영역에 point cloud 영상이 나타나야 함
9. 카메라를 얼굴에 비추면 얼굴의 윤곽이 화면에 보이며 컬러로 나타나고 얼굴에 가린 뒤쪽은 그림자가 진 것처럼 검게 나타남.
10. 마우스로 그 영역을 왼쪽/가운데 버튼으로 클릭해서 움직이면 회전/확대/축소가 되고 Shift늘 누른채 드래그 하면 이동이 됨. 

## B. Depth cloud 영상 보기
1. realsense sdk가 설치된 상태에서, D435i 같은 센서를 PC에 연결.
2. 새 터미널에서 roscore 실행:
> roscore
3. 된 상태에서, 새 터미널에서 다음 명령을 실행:
> roslaunch realsense2_camera rs_camera.launch align_depth:=true
4. 새 터미널에서 rviz(시각화 도구)를 실행:
> rviz
5. rviz의 Displays 영역에서 Global Options/Fixed Frame이 map이 아닌 camera_link이어야 함.
   (이렇게 해야 Global Status가 Error 상태에서 OK 상태가 됨)
6. rviz 왼쪽 아래의 Add를 누르고 By display type/DepthCloud를 고르고 OK를 누름.
7. rviz/Displays/DepthCloud/Depth Map Topic의 오른쪽 빈 곳을 누르고 /camera/depth/image_rect_raw를 입력 또는 선택.
8. rviz의 오른쪽 검은 영역에 depth cloud 영상이 흑백으로 나타나야 함.
9. 카메라를 얼굴에 비추면 얼굴의 윤곽이 등고선처럼 화면에 보이며 흑백으로 나타나고 얼굴에 가린 뒤쪽은 그림자가 진 것처럼 검게 나타남.
10. 마우스로 그 영역을 왼쪽/가운데 버튼으로 클릭해서 움직이면 회전/확대/축소가 되고 Shift늘 누른채 드래그 하면 이동이 됨. 
