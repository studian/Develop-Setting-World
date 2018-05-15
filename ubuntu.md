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
# 마운트
```bash
mount -a
```
