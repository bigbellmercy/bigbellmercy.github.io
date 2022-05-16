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

`--fakeroot` 옵션은, 컨테이너 속에서 일반 사용자가 root의 권한을 갖게하는 방법이다.

`--writable` 옵션은, 컨테이너가 쓰기 가능하게 되어서, 컨테이너가 종료 뒤에도, 컨테이너 속의 바뀐 내용이 남아 있게 된다.

`--nv` 옵션은, 컨테이너 속에서 Nvidia 사의 GPU를 쓸 수 있게 한다.

`--no-home` 옵션은, 사용자 home 폴더를 마운트하지 않게 한다.


# 컨테이너 이미지 파일 저장하기
현재 실행중인 컨테이너를 이미지 파일로 저장하는 방법은, 아래처럼 sif 폴더를 `tar` 명령으로 단순히 묶어서 파일로 만드는 것이다.
```
tar czf container_image_file.sif.tar.gz container_image_folder.sif
```
만들어진 이미지 파일을 컨테이너로 쓰려면, 아래처럼 묶인 이미지 파일을 sif 폴더를 다시 풀어서 쓰면 된다.
```
tar zxf container_image_file.sif.tar.gz
```
