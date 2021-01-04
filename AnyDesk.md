### 1. install Anydesk in Ubuntu
Run the following commands as root user:
```
$ sudo su
```
- add repository key to Trusted software providers list
```
# wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | apt-key add -
```
- add the repository:
```
echo "deb http://deb.anydesk.com/ all main" > /etc/apt/sources.list.d/anydesk-stable.list
```
- update apt cache:
```
apt update
```
- install anydesk:
```
apt install anydesk
```

### 2. Security setting
```
$ anydesk-global-settings
```
