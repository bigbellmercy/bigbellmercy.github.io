---
title: "ROS 유용한 사용법들"
date: 2020-8-25 16:40:00 +09:00
categories: ROS
---

# 실행 환경 설정 기본 사항
ROS 설치가 끝난 뒤에는 사용자 home 폴더의 `.bashrc` 파일에 다음 두 줄을 넣어 주는 것이 다. 그렇지 않으면 매번 터미널에서 아래 두 줄을 실행해야 한다.
> source /opt/ros/melodic/setup.bash  
> source ~/catkin_ws/devel/setup.bash

이때, 위 경로들에는 실제 맞는 경로로 넣어 줘야 한다. 첫 줄은 `apt-get`으로 설치한 ROS 패키지에 해당하고, 둘째 줄은 소스 코드로 설치한 ROS 패키지들에 해당한다.

# ROS Topic 이름 바꾸기

## 명령줄(command line)에서 바로 바꾸고 싶다면
이미 발행(publish)되고 있는 ROS 메시지의 주제(topic) 이름을 바꿀 수는 없지만, 다음처럼, 그 주제의 메시지를 다른 이름의 주제에 복사해서 다시 발행할 수 있다.
> rosrun topic_tools relay &lt;input_topic&gt; &lt;output_topic&gt;   
   
그러나, 메시지를 복사해서 새로 만들기 때문에 효율적이지는 못하다. 효율성을 위해서는 아래 방법을 쓴다.

## Launch 파일 속에서 Topic의 이름 바꾸기
한 주제(topic)의 이름을 바꾸는 이유는, 새로운 이름을 갖는 주제를 가지고 다른 소프트웨어(SW)에서 쓰기 위함이다.
따라서, 이름을 바꿀 필요 없이, 그 주제(topic)를 사용하는 ROS SW에서, 다음 문장을 이용해서, 바꾸기 전의 이름 그대로 쓰도록 설정하는 방법이다.
그 ROS SW의 Launch 폴더에 있는 해당 .launch 파일 속에서 원하는 <node> 단락 속에 다음 문장을 적는다:
> &lt;remap from="image" to="/usb_cam/image_raw" /&gt;
   
이렇게 하면, 이 SW는 /image라는 주제 대신에, /usb_cam/image_raw 주제를 사용한다(구독(subscribe)하거나 발행(publish)한다). 이 방법은 위 방법보다 더 처리가 빠르다.

# Topic 발행 속도 바꾸기
만약 한 주제(topic)가 너무 빠른 속도로 발행되고 있을 때, 10 Hz로 속도를 낮추려면 다음의 명령을 사용한다.
> rosrun topic_tools throttle messages &lt;input_topic&gt; 10 &lt;output_topic&gt;

# Launch 파일 속에서 Parameter 값 바꾸기
파라미터의 값을 바꾸려면 Launch 파일 속에서 다음의 예처럼 적는다.
> &lt;param name="enable_pose_jumping" type="bool" value="False" /&gt;
   
만약, 파라미터의 경로가 기본 경로와 다르다면 아래처럼 전체 경로를 지정할 수 있다.
> &lt;param name="/camera/tracking_module/enable_pose_jumping" type="bool" value="False" /&gt;

# Rosbag (메시지 신호 저장 기능) 사용법
1. 화제(topic)(메시지, 신호)들을 저장하고 싶을 때 아래처럼 하나 이상의 화제를 적는다. 기록이 시작되면 저장하는 파일 이름이 나타난다.
> rosbag record /mavros/odometry/in
2. 저장을 중단하고 싶을 때에는 Ctrl+C를 누른다. 저장된 .bag 파일이 home 폴더에 그 파일이 있을 것이다.
3. 저장된 파일을 그래프로 보고 싶으면, roscore가 실행된 상태에서, rqt_bag을 실행한다.
- 열기 단추를 눌러서 파일을 연다.
- 화제의 목록에서 보려는 화제 위에서 오른쪽 단추를 누르고 view / plot을 누르면 오른쪽에 창이 나타난다.
- 이 창을 끌어서 아래 쪽으로 길게 보이게 옮긴다(생략 가능).
- 이 창의 '나무 보기'(tree view)에서 그래프로 보고자 하는 항목들을 체크하면 그래프가 나타난다.
- 주의 할 점은, 이 그래프는 모든 점을 다 찍은 것이 아니라, 자동으로 해상도가 조정되어 적당하게 점들을 띄엄 띄엄 찍은 것이기에 실제 그래프와 다를 수 있으며, 그래프의 시간 범위가 긴 경우에 특히 더 실제 그래프와 다를 수 있다.
- 그래프의 실제 점들을 보고 싶다면, 그 창의 Configure Plot / Show Plot Markers를 체크하며면, 실제 점들이 나타난다.
- 만약, 그래프의 점들을 더 자세히 찍고 싶다면, 그 창의 Resolution: 옆의 Auto를 끄고, 점들 사이의 원하는 시간 간격(초)을 입력한다. 

# ROS를 여러 컴퓨터에서 실행하기
ROS(ROS 2가 아닌 ROS 1 기준)에서는 여러 컴퓨터들 상에서 실행되는 ROS 노드끼리 통신이 가능하다. 이때, 그 중에서의 한 대의 컴퓨터를 master로 지정해야 한다. 참고로, ROS1의 다은 판인 ROS2에서는 master의 지정 없이 컴퓨터들 사이의 통신이 가능하며, 계속 개발 개선 중에 있다.

master가 되는 컴퓨터에서는, 사용자 home 폴더의 `.bashrc` 파일을 열고 다음을 추가한다. 여기서 IP 주소는 master 자신의 주소이다.
> export ROS_HOSTNAME=192.40.1.123  
> export ROS_IP=192.40.1.123  

master가 아닌 컴퓨터에서는, 사용자 home 폴더의 `.bashrc`를 열고 다음을 추가한다. 여기서, IP 주소는 master 컴퓨터의 주소이다.
> export ROS_MASTER_URI=http://192.40.1.123:11311

위와 같이 설정한 뒤에는, 컴퓨터를 재시작하거나, 새로운 터미널에서 노드를 실행해야 한다. 

만약, 화제 목록은 상대 컴퓨터에 나타나는데, 화제의 자료가 나타나지 않을 때에는, 아래의 예처럼 각자의 IP 주소를 가지고 `.bashrc`에 추가한다.
> export ROS_IP=172.80.10.100

# 컴퓨터 사이에 시각 동기화 하기
ROS 사이에 시각 동기화가 잘 되어야 하므로 다음처럼 설정한다.
시각 동기화 SW인 `chrony`를 다음처럼 설치한다.
> sudo apt install chrony

시각 동기화 서버(보통 인터넷이 연결되는 컴퓨터)에서 `/etc/chrony/chrony.conf` 파일을 다음처럼 수정한다.  
여기서, `allow` 뒤에는 두 컴퓨터가 속한 네트워크의 IP 세 자리 앞 주소이고, `allow`문을 여러 개 적을 수 있다.  
```
local stratum 8
manual
allow 192.168.1
smoothtime 400 0.01
```

시각 동기화 클라이언트(서버로부터 시각을 받는)에서 위와 같은 파일을 다음처럼 수정한다.
먼저, `pool`로 시작하는 문장 앞에 #을 붙여서 주석 처리한다.
다음 줄을 수정한다. 여기서, IP 주소는 서버의 것을 적는다.  
```
server 192.168.1.100 iburst
makestep 1 -1
```

# 명령줄에서 메시지 보내기
명령줄(command line)에서 `rostopic` 명령으로 토픽 메시지를 내보낼 수 있다.   
다음 명령은 hello라는 글 메시지를 /my_topic이란 화제로 내보낸다.
```
rostopic pub /my_topic std_msgs/String "hello"
```
   
다음 명령은 /aaa라는 화제(topic)로 geometry_msgs/PoseStamped라는 형식의 메시지를 내보내는 예제이다.   
```
rostopic pub /aaa geometry_msgs/PoseStamped '{header: {seq: 0, stamp: {secs: 0, nsecs: 0}}, pose: {position: {x: 0, y: 1, z: 2}, orientation: {x: 0, y: 0, z: 0, w: 1} } }'
```
