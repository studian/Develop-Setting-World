# ===================================================================================
# ubuntu 에서 도커 사용환경 만들기
1. install ubuntu
2. install nvidia driver # https://hiseon.me/2018/02/17/install_nvidia_driver/
3. install docker-ce 
4. install nvidia-docker
5. download docker image # https://hub.docker.com/
   # docker image download instruction $ docker pull nvidia/cuda:8.0-cudnn7-runtime-ubuntu16.04
6. 컨테이너 만들기
```
$ docker run -d \
-it --name cuda_docker \
-v /home/hdd1:/mnt \
--network=host \
--runtime=nvidia \
nsml/ml:cuda9.0-cudnn7-tf-1.11torch1.0keras2.2 /bin/bash
```
7. 컨테이너 서비스 실행 
```
$ docker start -a cuda_docker
```
8. 컨테이너 실행
```
$ docker exec -it cuda_docker /bin/bash 
```

3./4. reference web site
- https://hiseon.me/2018/02/19/install-docker/


======================================================================

# create container (컨테이너 환경 만드는거)
```
docker run -d \
-it --name cuda_docker \
-v /home/hdd1:/mnt \
--network=host \
--runtime=nvidia \
nsml/ml:cuda9.0-cudnn7-tf-1.11torch1.0keras2.2 /bin/bash
```

# auto starting
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

# execute container
```
docker exec -it cuda_docker /bin/bash
```

# check current container list (만들어져있는 컨테이너 환경 보는거)
```
$ docker container ls # 컨테이너 이미지 이름, 컨테이너 이름 확인
```

# if no container 
```
$ sudo systemctl enable cuda_docker # 서비스 시작 (cuda_docker: 컨테이너 이름)
$ docker start -a cuda_docker # 컨테이너 status : up 으로 변경하는거 (업해서 실행해야함)
$ docker exec -it cuda_docker /bin/bash # (컨테이너 실행: /bin/bash를 cuda_docker로 돌린다)
"root@mspserver:/# " 뜨는지 확인
```
