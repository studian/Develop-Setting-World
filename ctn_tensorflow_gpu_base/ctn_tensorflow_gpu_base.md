* cuda: 10.1
* cudnn: 7.5-devel
* python: 3.5
* tensorflow-gpu: 1.13.1
* Keras: 2.3.1
* opencv-python: 4.1.1.26
```
$ docker run -d -it --name ctn_tensorflow_gpu_base\
    --env="DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    -env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --runtime=nvidia \
    -v /home/user/rs_postdoc:/mnt \
    -e DISPLAY=$DISPLAY \
    -p 8888:8888 \
    -p 6006:6006 \
    studian/tensorflow_gpu:1.13.1 \
    /bin/bash
```
