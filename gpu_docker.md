# Reference WebSites
* https://github.com/studian/Develop-Setting-World/blob/master/gpu_docker.md
* https://m.blog.naver.com/PostView.nhn?blogId=complusblog&logNo=220974632766&proxyReferer=https%3A%2F%2Fwww.google.com%2F
* https://hub.docker.com/r/dash00/tensorflow-python3-jupyter/?source=post_page-----d93fbc99e154----------------------
* https://moordev.tistory.com/173 # docker 에서 gui 사용하기
* https://riptutorial.com/ko/docker/example/21831/linux-컨테이너에서-gui-애플리케이션-실행하기 # docker tutorial
* https://yahwang.github.io/posts/40 # docker에서 PC 그래픽과 연결해 tensorflow-gpu 실행하기
* http://haanjack.github.io/docker/2017/12/01/nvidia-docker-ngc.html # nvidia-docker 2.0 
* https://pbj0812.tistory.com/134 # [Docker] 설치, 다운로드, 실행, jupyter notebook 연동, 삭제, 기타 등등

# Make Docker Env for GPU in ubuntu 

1) install ubuntu

2) install nvidia driver
- reference site: https://hiseon.me/2018/02/17/install_nvidia_driver/

3) install docker-ce 
- reference site(korean): https://hiseon.me/2018/02/19/install-docker/

4) install nvidia-docker
- reference site(korean): https://hiseon.me/2018/02/19/install-docker/

5) install nvidia-docker 2.0 
- reference site(korean): http://haanjack.github.io/docker/2017/12/01/nvidia-docker-ngc.html

5) download docker image 
- reference site: https://hub.docker.com/
```
$ docker pull nvidia/cuda:8.0-cudnn7-runtime-ubuntu16.04 # docker image download instruction
```

# Make Docker 활용

0) Docker 서비스 실행/재실행/
```
$ sudo service docker start
$ sudo service docker restart
$ sudo service docker stop
```

0) docker가 root 계정으로 설치 되었을때 root 계정이 아닌 계정으로 docker를 실행하고자 하면 제목과 같은 에러가 발생할 시 해결 방법
* 에러 메세지: Solving Docker permission denied while trying to connect to the Docker daemon socket
```
$ sudo usermod -a -G docker $USER
$ sudo service docker restart
$ sudo reboot
```

1) Docker build - Dockerfile을 이용해서 이미지 생성하기
* Dockerfile이 있는 폴더 안에서 실행 시
```
$ docker build -t 사용할_docker_이미지_이름 ./
```
```
$ docker build -t img-cuda10.1-cudnn7.6-py3.6 ./
```
* Dockerfile이 있는 폴더의 경로를 알때 실행 시
```
$ docker build -t 사용할_docker_이미지_이름 Dockerfile-PATH
```
```
$ docker build -t img-cuda10.1-cudnn7.6-py3.6 /home/user/cuda10.1-cudnn7.6-devel-ubuntu16.04
```

2) Make contatiner 컨테이너 만들기
```
$ docker run -d -it --name 컨테이너_이름\
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    -env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --runtime=nvidia \
    -v host_환경에서_mount_시킬_폴더_경로:/mnt \
    -e DISPLAY=$DISPLAY \
    -p host_환경에서_사용하는_port_번호:docker_환경에서_사용하는_port_번호 \
    사용할_docker_이미지_이름 \
    /bin/bash
```
```
$ docker run -d -it --name ctn_cuda10.1_cudnn7.6_py3.6\
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    -env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --runtime=nvidia \
    -v /home/msp/HDD:/mnt \
    -e DISPLAY=$DISPLAY \
    -p 8888:8888 \
    -p 6006:6006 \
    img-cuda10.1-cudnn7.6-py3.6 \
    /bin/bash
```

3) 컨테이너 서비스 실행 
```
$ docker start -a 컨테이너_이름
```
```
$ docker start -a ctn_cuda10.1_cudnn7.6_py3.6
```

4) 컨테이너 실행
```
$ docker exec -it 컨테이너_이름 /bin/bash 
```
```
$ docker exec -it ctn_cuda10.1_cudnn7.6_py3.6 /bin/bash
```

5) 컨테이너 stop
```
$ docker stop 컨테이너_이름
```
```
$ docker stop ctn_cuda10.1_cudnn7.6_py3.6
```

6) 컨테이너 restart
```
$ docker restart 컨테이너_이름
```
```
$ docker restart ctn_cuda10.1_cudnn7.6_py3.6
```

7) 동작중인 컨테이너 확인
```
$ docker ps
```

8) 모든 컨테이너 확인
```
$ docker ps -a
```

9) 컨테이너 삭제 (복수개도 가능)
```
$ docker rm 컨테이너id
$ docker rm 컨테이너id, 컨테이너id, 컨테이너id
```

10) 이미지 확인
```
$ docker images
```

11) 이미지 삭제 
```
$ docker rmi 이미지id
```

12) 컨테이너를 삭제하기 전에 이미지를 삭제할 경우 (-f 옵션을 붙이면 컨테이너도 강제삭제)
```
$ docker rmi -f 이미지id
```

13) 만들어져있는 컨테이너 이름 리스트 확인
```
$ docker container ls # 컨테이너 이미지 이름, 컨테이너 이름 확인
```

======================================================================

## auto starting : 굳이 이 세팅 할 필요 없음
```
/etc/systemd/system/cuda_docker.service
```
```
[Unit]
Description=cuda_docker_container
Requires=docker.service

[Service]
ExecStart=/usr/bin/docker start -a cuda_docker
ExecStop=/usr/bin/docker stop cuda_docker

[Install]
WantedBy=multi-user.target
```
```
$sudo systemctl enable cuda_docker
```

# 딥러닝 환경 구축을 위해 docker 컨테이너 실행 후 '기본' 세팅 라이브러리
```
# pip install Pillow numpy graphviz scikit-image scikit-learn scipy tqdm numpy matplotlib
# pip install opencv-python opencv-contrib-python
# apt-get install libsm6 libxrender1 libfontconfig1
# pip install --upgrade pip 
# pip install --no-cache-dir\
```

# 딥러닝 환경 구축을 위해 docker 컨테이너 실행 후 '선택적' 세팅 라이브러리
```
# pip install tensorflow-gpu
# pip install keras
# pip install torch==0.4.1 torchvision
```

# docker 에서 jupyter notebook 실행
```
# jupyter notebook --allow-root --ip 172.17.0.2
```

# docker 환경에서 파일/폴더 생성 시 host 환경에서 열기/수정 권한 문제 해결
* docker 환경에서 명령어 실행
* 하위 폴더까지 적용 시 -Rf 옵션 넣기
```
# chmod -Rf a+rwx '폴더이름 또는 파일이름'
```
```
# chmod -Rf a+rwx Results_*
```




