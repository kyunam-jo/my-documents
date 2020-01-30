### Storage 속도 측정
```
$ dd if=/dev/zero of=test.out bs=1M count=10 oflag=direct
```

### 새로운 disk 설치시
```
/dev/sdb
fdisk 로 파티션생성 /dev/sdb1
mkfs.ext4 filesystem 생성
mount
```
### OS level에서 용량을 제한한 Image 생성 후 연결할 directory에 mount
```
# dd if=/dev/zero of=harddrive.img count=512 bs=1M
# mkfs.ext4 harddrive.img
# fdisk -l harddrive.img
# mkdir /home/jeff/myvolume
# mount -o loop harddrive.img /home/jeff/volume
# chown -R jeff:jeff /home/jeff/myvolume
```    
## Docker Network
* overlay network : 다중 host 다중 container를 묶을때 사용하는 네트워크 (swarm cluster에서 사용)

### docker running 중인 container network 추가
```
$ docker network create --drivier=bridge 네트워크이름
$ docker network connect 네트워크이름 컨테이너이름
```
## Docker Container 조작
* attach : docker attach 하면 연결된 모든 terminal에서 동일한 동작이 수행된다 (심지어 exit까지)
    ```
    $ docker attach 이름
    ```
* exec : 임의의 command 실행
    ```
    $ docker exec 이름 bash
    ```
* top : 실행 프로세스 출력
    ```
    $ docker top 이름
    ```
* port : 외부에 노출된 port 정보 출력
    ```
    $ docker port 이름
    ```
* rename : container의 이름 변경
    ```
    $ docker rename old이름 new이름
    ```
* cp : host에서 container 내부로 파일 복사
    ```
    $ docker cp lotto.py test_copy:/lotto.py
    ```
* diff : Host에서 container의 변경사항을 조회
    ```
    $ docker diff 이름
    ```
* commit : container를 image로 만듬
    ```
    $ docker commit -a [author] container이름 image이름:tag이름
    ```
* export : container를 tar 파일로 저장
    ```
    $ docker export container이름 > 파일이름.tar
    ```
* import : tar파일에서 이미지로 밀어넣기
    ```
    $ docker image import tar파일이름 이미지이름:태그이름
    or
    $ cat tar파일이름 | docker import - 이미지이름:태그이름
    ```
* save : 이미지를 tar 파일로 저장 ( export 는 필요한 프로세스파일만, save는 이미지의 모든 레이어 )
    ```
    $ docker image save 이미지이름:태그이름 > 파일이름.tar
    ```
* load : tar파일을 이미지로 저장
    ```
    $ docker image load -i tar파일이름
    ```
* prune : 사용하지 않는 이미지 or Container 삭제
