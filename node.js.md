### 설치: How To Install Node.js on Ubuntu 16.04
* 참고싸이트: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04
* 12.16.1로 설치

1. 기본 설치 및 버전 확인
```
$ sudo apt-get update
$ sudo apt-get install nodejs
$ sudo apt-get install npm
$ nodejs -v
```
2. 업그레이드 후 12.x 버전 확인
```
$ cd ~
$ curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
$ sudo bash nodesource_setup.sh
$ sudo apt-get install nodejs
$ nodejs -v
```
3. nvm 업그레이드 환경 설치
```
$ npm -v
$ sudo apt-get install build-essential
$ sudo apt-get update
$ sudo apt-get install build-essential libssl-dev
$ curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh -o install_nvm.sh
$ bash install_nvm.sh
$ source ~/.profile
```
4. nvm 최신 버전 확인
```
$ nvm ls-remote
```
5. 앞에서 설치한 node 버전과 동일한 LTS 버전 확인하여 설치(2020.03.17 기준 12.16.1 버전임)
```
$ nvm install 12.16.1
$ nvm use 12.16.1
$ node -v
$ nvm alias default 12.16.1
$ npm install express
```

### Error

1. /usr/bin/env: ‘node’: No such file or directory
* solution: 
```
$ ln -s /usr/bin/nodejs /usr/bin/node
```

### 삭제
```
$ sudo apt-get remove nodejs
$ sudo apt-get remove npm
$ sudo apt-get update
```
* Check for any .npm or .node folder in your home folder and delete those.
```
$ which node
$ which nodejs
$ which npm
```
* This is better to remove NodeJS and its modules manually because installation leaves a lot of files, links and modules behind and later it create problems while we reconfigure another version of NodeJS and its modules. Run the following commands.
```
$ sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* /usr/local/lib/dtrace/node.d ~/.npm ~/.node-gyp /opt/local/bin/node /opt/local/include/node /opt/local/lib/node_modules 
$ sudo rm -rf /usr/local/lib/node*
$ sudo rm -rf /usr/local/include/node*
$ sudo rm -rf /usr/local/bin/node*
```
