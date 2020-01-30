## Docker Container Application 구축

### Containerize 
-> docker-compose로 구현 권고

#### 1. MySql & Wordpress
* docker link 사용
```
$ docker run -d --name wordpressdb -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress mysql:5.7
$ docker run -d -e WORDPRESS_DB_PASSWORD=password --name wordpress --link wordpressdb:mysql -p 80 wordpress
```
* docker network 사용
```
$ docker run -d --name wp-db --network wp-network -e MYSQL_ROOT_PASSWORD=password1 -e MYSQL_DATABASE=wp -v `pwd`/wp_db:/var/lib/mysql mysql:5.7
$ docker run -d --name wp --network wp-network -e WORDPRESS_DB_NAME=wp -e WORDPRESS_DB_PASSWORD=password1 -e WORDPRESS_DB_HOST=wp-db -p 80 wordpress
```
* docker network 사용 + docker volume
```
$ docker volume create wp-db-volume
$ docker run -d --name wp-db --network wp-network -e MYSQL_ROOT_PASSWORD=password1 -e MYSQL_DATABASE=wp -v wp-db-volume:/var/lib/mysql mysql:5.7
$ docker run -d --name wp --network wp-network -e WORDPRESS_DB_NAME=wp -e WORDPRESS_DB_PASSWORD=password1 -e WORDPRESS_DB_HOST=wp-db -p 80 wordpress
```
#### 2. Host - Container - Container volume 연결
```
$ docker run -it --name data_share -v /data_share ubuntu /bin/bash
$ docker run -it --name data_share_c1 --volumes-from data_share ubuntu /bin/bash
$ docker run -it --name data_share_c2 --volumes-from data_share ubuntu /bin/bash
```
#### 3. 

#### 4. MariaDB - Sharding(분산DB Partition)
