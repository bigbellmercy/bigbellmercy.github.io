---
title: "ROS 유용한 사용법들"
date: 2020-8-25 16:40:00 +09:00
categories: ROS
---

# ROS Topic 이름 바꾸기

## 명령줄(command line)에서 바로 바꾸고 싶다면
이미 출판(publish)되고 있는 ROS 메시지의 주제(topic) 이름을 바꿀 수는 없지만, 다음처럼, 그 주제의 메시지를 다른 이름의 주제에 복사해서 다시 출판할 수 있다.
> rosrun topic_tools relay &lt;input_topic&gt; &lt;output_topic&gt;   
   
그러나, 메시지를 복사해서 새로 만들기 때문에 효율적이지는 못하다. 효율성을 위해서는 아래 방법을 쓴다.

## Launch 파일 내에서 이름 바꾸어 쓰기
한 주제(topic)의 이름을 바꾸는 이유는, 새로운 이름을 갖는 주제를 가지고 다른 소프트웨어(SW)에서 쓰기 위함이다.
따라서, 이름을 바꿀 필요 없이, 그 주제(topic)를 사용하는 ROS SW에서, 다음 문장을 이용해서, 바꾸기 전의 이름 그대로 쓰도록 설정하는 방법이다.
그 ROS SW의 Launch 폴더에 있는 해당 .launch 파일 속에 다음 문장을 적는다:
> &lt;remap from="image" to ="/usb_cam/image_raw" /&gt;
   
이렇게 하면, 이 SW는 /image라는 주제 대신에, /usb_cam/image_raw 주제를 사용한다(구독(subscribe)하거나 출판(publish)한다). 이 방법은 위 방법보다 더 처리가 빠르다.