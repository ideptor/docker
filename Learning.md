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

### 4.1 Dockerfile 만들기
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

### 4.2 build 명령으로 이미지 생성하기
```
$ sudo docker build --tag hello:0.1
```

### 4.3 실행하기
```
$ sudo docker run --name hello-nginx -d -p 80:80 /root/data:/data hello:0.1
```

웹브라우저를 실행하고 **http://<host IP>:8080** 으로 접속하면 Welcome to ninx! 페이지 표시


## CH05 Docker 살펴보기

### 5.1 history 명령으로 이미지 history 살펴보기
```
$ docker history hello:0.1
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
eac1a5065fac        9 minutes ago       /bin/sh -c #(nop)  EXPOSE 443                   0B
111bc3f5439c        9 minutes ago       /bin/sh -c #(nop)  EXPOSE 80                    0B
505bbf6b92a6        9 minutes ago       /bin/sh -c #(nop)  CMD ["nginx"]                0B
29633862fb69        9 minutes ago       /bin/sh -c #(nop) WORKDIR /etc/nginx            0B
d46848bb703b        9 minutes ago       /bin/sh -c #(nop)  VOLUME [/data /etc/nginx/…   0B
3e36b00967ba        9 minutes ago       /bin/sh -c chown -R www-data:www-data /var/l…   0B
f62abbb0e42b        9 minutes ago       /bin/sh -c echo "\ndaemon off;" >> /etc/ngin…   1.5kB
83a80dd6d8c2        9 minutes ago       /bin/sh -c apt-get install -y nginx             60.2MB
c3af8e2d006b        10 minutes ago      /bin/sh -c apt-get update                       27.4MB
7df0b851cbf1        10 minutes ago      /bin/sh -c #(nop)  MAINTAINER David <ideptor…   0B
775349758637        6 days ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           6 days ago          /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B
<missing>           6 days ago          /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B
<missing>           6 days ago          /bin/sh -c [ -z "$(apt-get indextargets)" ]     987kB
<missing>           6 days ago          /bin/sh -c #(nop) ADD file:a48a5dc1b9dbfc632…   63.2MB
```

### 5.2 cp 명령으로 파일 꺼내기
```
$ docker cp hello-nginx:/etc/nginx/nginx.conf ./
```

### 5.3 commit 명령으로 컨테이너의 변경사항을 이미지로 생성하기
```
$ docker commit -a "David <ideptor.d@gmail.com>" -m "add hello.txt" hello-nginx hello:0.2
sha256:10ed250836e598f8e28d80810dce6f5707817dd16b043bd4ff2878a5c2c984b1

$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello               0.2                 10ed250836e5        6 seconds ago       152MB
hello               0.1                 eac1a5065fac        32 minutes ago      152MB
```

### 5.4 diff 명령으로 컨테이너에서 변경된 파일 확인하기
```
$ docker diff hello-nginx
C /var
C /var/lib
C /var/lib/nginx
A /var/lib/nginx/body
...
```

### 5.5 inspect 명령으로 세부정보 확인하기
```
$ docker inspect hello-nginx
[
    {
        "Id": "ae97753f3964d8999fd1e4c31fc927e5e6e2f4cac5b1a92768c1582cd1c1f1eb",
        "Created": "2019-11-07T00:12:20.692915853Z",
        "Path": "nginx",
...
```
