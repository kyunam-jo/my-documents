## Storage 속도 측정
dd if=/dev/zero of=test.out bs=1M count=10 oflag=direct

## 새로운 disk 설치시 
/dev/sdb
fdisk 로 파티션생성 /dev/sdb1
mkfs.ext4 filesystem 생성
mount

