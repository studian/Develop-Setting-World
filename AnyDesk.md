### 1. install Anydesk in Ubuntu
Run the following commands as root user:
```
user$ sudo su
```
- add repository key to Trusted software providers list
```
root# wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | apt-key add -
```
- add the repository:
```
root# echo "deb http://deb.anydesk.com/ all main" > /etc/apt/sources.list.d/anydesk-stable.list
```
- update apt cache:
```
root# apt update
```
- install anydesk:
```
root# apt install anydesk
```

### 2. Security setting
```
root# anydesk-global-settings
```
