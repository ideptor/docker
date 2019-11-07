# CH04 nginx 이미지 만들기

## Dockerfile 만들기
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

## build 명령으로 이미지 생성하기
```
$ sudo docker build --tag hello:0.1
```

## 실행하기
```
$ sudo docker run --name hello-nginx -d -p 80:80 /root/data:/data hello:0.1
```

웹브라우저를 실행하고 **http://<host IP>:8080** 으로 접속하면 Welcome to ninx! 페이지 표시

