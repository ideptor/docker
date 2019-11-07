# 가장 빨리 만나는 도커 - 이재홍지음 / 

## CH03 Docker 사용해 보기

### 3.1 Search 명령으로 이미지 검색하기

```
$ docker search ubuntu
NAME                                                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
ubuntu                                                    Ubuntu is a Debian-based Linux operating sys…   10115               [OK]
dorowu/ubuntu-desktop-lxde-vnc                            Docker image to provide HTML5 VNC interface …   358                                     [OK]
rastasheep/ubuntu-sshd                                    Dockerized SSH service, built on top of offi…   232                                     [OK]
...
```

### 3.2 pull 명령으로 이미지 받기
```
$ docker pull ubuntu
```

### 3.3 images 명령으로 이미지 목록 출력하기
```
$ docker images
```

### 3.4 run 명령으로 컨테이너 생성하기
```
docker run -dit --name hello ubuntu /bin/bash
```

### 3.5 ps 명령으로 컨테이너 목록 확인하기
```
$ cker ps -a
```

### 3.6 start 명령으로 컨테이너 시작하기
```
$ sudo docker start hello
```

### 3.7 restart 명령으로 컨테이너 재시작하기
```
$ sudo docker restart hello
```

### 3.8 attach 명령으로 컨테이너 접속하기
```
$ sudo docker attach hello
```

### 3.9 exec명령으로 외부에서 컨테이너 안의 명령 실행하기
```
$ sudo docker exec hello echo "hello world"
```


## CH04 nginx 이미지 만들기

### Dockerfile 만들기
```
FROM ubuntu
MAINTAINER David <ideptor.d@gmail.com>

RUN apt-get update
RUN apt-get install -y nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN chown -R www-data:www-data /var/lib/nginx

VOLUME ["/data", "/etc/nginx/site-enabled", "/var/log/nginx"]

WORKDIR /etc/nginx

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
```

### build 명령으로 이미지 생성하기
```
$ sudo docker build --tag hello:0.1
```

### 실행하기
```
$ sudo docker run --name hello-nginx -d -p 80:80 /root/data:/data hello:0.1
```

웹브라우저를 실행하고 **http://<host IP>:8080** 으로 접속하면 Welcome to ninx! 페이지 표시


## CH05 Docker 살펴보기
