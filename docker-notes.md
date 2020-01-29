Docker Container가 동일 network로 묶였을때 ping에 hostname이나 ip가 아니고 container 이름으로도 가능하다~!


h2. memory 제한시 발생하는 warning 제거

WARNING: Your kernel does not support swap limit capabilities or the cgroup is not mounted. Memory limited without swap.
$ sudo vi /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="cgroup_enable=memory swapaccount=1"
#GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

$ sudo update-grup
$ sudo reboot

docker memory swap 제한 시 -1 일 경우 무제한, 0이면 disable(사용안함)

h3. 리눅스 리소스 측정 방법
htop : 각 cpu core 별로 정확한 값을 보여줌
free -mt : 메모리 사용량 측정
df -h : storage 사용량
alicek106/stress : stress 주는 docker image 
ex) docker run -d --name cpu_1024 --cpu-shares 1024 --cpuset-cpus 0 alicek106/stress stress --cpu 1
ps -auxf | grep stress : time 측정

docker update를 통해서 실행중인 container의 설정을 변경할 수 있다.
