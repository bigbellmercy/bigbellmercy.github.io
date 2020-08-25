---
title: "ROS 유용한 사용법들"
date: 2020-8-25 16:40:00 +09:00
categories: ROS
---

# ROS Topic 이름 바꾸기
이미 출판(publish)되고 있는 ROS 메시지의 주제(topic) 이름을 바꿀 수는 없지만, 다음처럼, 그 주제의 메시지를 다른 이름의 주제에 복사해서 다시 출판할 수 있다.
> rosrun topic_tools relay &lt;input_topic&gt; &lt;output_topic&gt;
