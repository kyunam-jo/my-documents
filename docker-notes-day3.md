### Storage 속도 측정
dd if=/dev/zero of=test.out bs=1M count=10 oflag=direct

### 새로운 disk 설치시 
/dev/sdb
fdisk 로 파티션생성 /dev/sdb1
mkfs.ext4 filesystem 생성
mount

### OS level에서 용량을 제한한 Image 생성 후 연결할 directory에 mount
    # dd if=/dev/zero of=harddrive.img count=512 bs=1M
    # mkfs.ext4 harddrive.img
    # fdisk -l harddrive.img
    # mkdir /home/jeff/myvolume
    # mount -o loop harddrive.img /home/jeff/volume
    # chown -R jeff:jeff /home/jeff/myvolume
    
### 
