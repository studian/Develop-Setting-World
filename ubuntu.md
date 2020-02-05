# GPU monitoring
```bash
nvidia-smi -l 1
```
# 하드디스크 인식확인
```bash
fdisk -l
```
# 파티션 추가
```bash
fdisk /dev/sdb
```
# 포맷
```bash
mkfs.타입 /dev/sdb1
```

# UUID 확인
```bash
blkid
```

# fstab 수정
```bash
vi /etc/fstab
UUID=7514F3C548DC857A   /mnt/data1      ntfs    defaults,locale=ko_KR.UTF-8     0       0
```

```
#/dev/disk/by-uuid/6ce0f131-e804-4ad8-a3eb-5b8ec9ec23e9 /home/user/rs_postdoc auto nosuid,nodev,nofail,x-gvfs-show 0 0
#/dev/disk/by-uuid/424a215a-82a9-46fd-a8ff-f7f331b2d02e /home/user/rs_phd auto nosuid,nodev,nofail,x-gvfs-show 0 0
```
# 마운트
```bash
mount -a
```
# ubuntu 런처 위치 변경
* 런처를 왼쪽에 위치함
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Left 
```
* 런처를 아래쪽에 위치함
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```

# E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing? 에러 
* 참고: https://twpower.github.io/99-change-apt-get-source-server
* 참고: https://chonnom.com/bbs/board.php?bo_table=B19&wr_id=472
* 참고: https://chonnom.com/bbs/board.php?bo_table=B19&wr_id=469
```
sudo sed -i 's/kr.archive.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
```


