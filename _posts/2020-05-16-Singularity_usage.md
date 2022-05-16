---
title: "Singularity 사용법"
date: 2022-5-16 16:25:00 +09:00
categories: Container
---

# 목적
컴퓨터 가상화용 컨테이너(container) 소프트웨어인 Singularity[싱귤래러티]의 사용법을 정리하였습니다.

# Singularity의 특징
- Docker가 대중적인데 비해, Singularity는 대규모 고성능의 과학 프로젝트에서의 사용을 목표로 만들었다고 함.

# 실행 명령 사례
다음 명령을 터미널에서 실행하면, 'container_image_file.sif'라는 컨테이너 이미지로 인스탄스를 만든다.
```
singularity shell --fakeroot --writable --nv --no-home --bind /container_outside_folder/:/container_inside_folder /container_image_file.sif"
```
여기서, 'shell'은 컨테이너 속에서 처음으로 셸(shell)(리눅스 명령줄(command line)이 실행되는 소프트웨어)을 실행하는 명령이고, 이로써, 컨테이너 인스턴스(instance)(사례)가 만들어 진 뒤에 셸 창이 나타난다.

`--bind` 옵션을 썼으므로, 컨테이너 밖의 호스트 컴퓨터의 '/container_outside_folder' 폴더가, 컨테이너 속의 '/container_inside_folder'에 연결되어, 파일 공유가 가능해진다.
