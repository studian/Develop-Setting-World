# reference: https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Generic-x86-Docker

## Case3. Creating a Custom Autoware Docker Container

### 0. install docker

### 1. Clone the docker repository and move into the generic docker folder.
$ git clone https://gitlab.com/autowarefoundation/autoware.ai/docker.git
$ cd docker/generic

### 2. Before building the container, you can modify the Dockerfile files in the generic folder to change the generated container. Once you have modified them to your liking, build the docker container using the build.sh script:
$ ./build.sh
