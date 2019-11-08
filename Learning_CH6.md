# 가장 빨리 만나는 도커 - 이재홍지음 / 

## 들어가기 전에 (Docker-Toolbox @ Windows10 에서 파일 공유)
참고: https://stackoverflow.com/questions/33126271/how-to-use-volume-option-with-docker-toolbox-on-windows

### 1. VirtualBox의 default 머신 설정 변경
**VirtualBox**를 실행하여 `default` machine 의 **설정** > **공유폴더** 화면으로 이동 후 
폴더 경로에 `C:\` 추가 후 **자동 마운트(A)** **항상 사용하기(M)** 체크

### 2. Docker Machine restart 
docer-machine restart
```
$ docker-machine restart
Restarting "default"...
(default) Check network to re-create if needed.
...
```

`c` 디렉토리 접근 가능한지 확인
```
$ docker-machine ssh
   ( '>')
  /) TC (\   Core is distributed with ABSOLUTELY NO WARRANTY.
 (/-_--_-\)           www.tinycorelinux.net

docker@default:~$ cd /c/
docker@default:/c$ ls -al
total 4
drwxr-xr-x    3 root     root            60 Nov  8 01:24 .
drwxr-xr-x   18 root     root           460 Nov  8 01:24 ..
dr-xr-xr-x    1 docker   staff         4096 Nov  4 01:44 Users

```

## CH06 Docker 좀 더 활용하기

### 6.1 Docker 개인 저장소 구축하기 (Docker Registory)

#### 6.1.1 로컬에 이미지 데이터 저장
Docker Registory 이미지 받기
```
$ docker pull registry:latest
```

컨테이너 실행
```
$ docker run -d -p 5000:5000 --name hello-registry -v /c/Users/idept/Documents/docker/registry:/tmp/registry registry
```



