# 1st-submission

 ## 1) 실행 환경
- OS: 
```bash
$ uname -a
Darwin c3r3s7.codyssey.kr 24.6.0 Darwin Kernel Version 24.6.0: Mon Jan 19 22:00:10 PST 2026; root:xnu-11417.140.69.708.3~1/RELEASE_X86_64 x86_64
```

- Shell:
```bash
$ echo$SHELL
/bin/zsh
```
- Docker: 
```bash
$ docker --version
Docker version 28.5.2, build ecc6942
```
- Git: 
```bash
$ git --version
git version 2.53.0
```

- Terminal:
```bash
$ printenv
 MallocNanoZone=0
USER=dave1392857
COMMAND_MODE=unix2003
__CFBundleIdentifier=com.microsoft.VSCode
```
- 


## 2) 수행 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 변경 실습   
- [x] Docker 설치/점검
- [x] hello-world 실행
- [x] Dockerfile 빌드/실행
- [x] 포트 매핑 접속(2회)
- [x] 바인드 마운트 반영
- [x] 볼륨 영속성
- [x] Git 설정 + VSCode GitHub 연동


## 2) 터미널 조작 로그
 1. 현재 위치 확인 : pwd
 ```bash
 $ pwd
/Users/dave1392857/practice/1st-submission
```

 2. 목록 확인: ls(파일만) ls -l(파일 권한) ls -la(숨김 파일)
```bash
$ ls

1st-submission  README.md
```
```bash
$ ls -l

total 8
drwxr-xr-x  5 dave1392857  dave1392857   160 Apr 10 19:30 1st-submission
-rw-r--r--  1 dave1392857  dave1392857  4013 Apr  9 21:45 README.md
```
```bash
$ls -la

otal 8
drwxr-xr-x   5 dave1392857  dave1392857   160 Apr 10 19:31 .
drwxr--r--   5 dave1392857  dave1392857   160 Apr  9 21:41 ..
drwxr-xr-x  14 dave1392857  dave1392857   448 Apr  9 21:50 .git
drwxr-xr-x   5 dave1392857  dave1392857   160 Apr 10 19:30 1st-submission
-rw-r--r--   1 dave1392857  dave1392857  4013 Apr  9 21:45 README.md
```

 3. 이동: mv 파일명.txt 새경로/파일.txt.    , (상위로 이동) mv 파일명.txt ../파일명.txt
 ```bash
#하위 폴더로 이동
$ 1% ls   
2       a

$ mv a 2/a

$ 1% ls
2
 ```
 ```bash
 #상위 폴더로 이동
$ 2 % ls
3       a

$ 2 % mv a ../a

$ 1 % ls
2       a
```


 4. 이름변경: mv 옛이름.txt 새이름.txt
 ```bash
# a => b
2       a

$ 1 % mv a b

$ 1% ls
2       b
 ```

 5. 폴더 생성: mkdir 폴더명   / (상위-하위) mkdir -p 이름1/이름2 .. 

 ```bash
 $ mkdir -p 1/2/3
dave1392857@c3r3s7 practice % ls
1               1st-submission
```
```bash
$ mkdir a
dave1392857@c3r3s7 1 % ls
2       a
```
 6. 파일 생성: touch 파일명.txt / (내용 담아서) echo 내용 > 파일명.txt
 ```bash
 #빈 파일
$ 1 % touch c
$ 1 % cat c
 ```
 ```bash
$ 1 % echo hi >d
$ 1 % cat d
hi
 ```
 7. 삭제: (파일 삭제) rm 파일명.txt.  /  (폴더 삭제) rm -r 이름 ,   (하위도 같이 삭제) rm -r e
```bash
#파일 삭제
$ 1 % ls
2       b       c

$ 1 % rm c

$ 1 % ls
2       b
```
```bash
#폴더 삭제
$ 1 % ls
2       b

$ 1 % rm -r b

$ 1 % ls
2
```

 8. 복사: cp 파일명.txt 복사파일명.txt
 ```bash
$ 1 % echo hi > a

$ 1 % cp a 2/b
 
$ 2 % ls
3       b

$ 2 % cat b
hi
 ```

## 3) 권한 실습
1. 권한 실습: r(read)/ w(write) / x(excute)
```bash
#권한 표기 확인
$ls -l 
$stat '파일명'

$stat b
16777220 1945074 -rw-r--r-- 1 dave1392857 dave1392857 0 3 "Apr 10 20:29:21 2026" "Apr 10 20:29:20 2026" "Apr 10 20:29:20 2026" "Apr 10 20:29:20 2026" 4096 8 0 b

$stat -f "%Sp %p" b
-rw-r--r-- 100644  
#100= 일반파일 / 040=폴더
```
```bash
#권한 변경
$ chmod 744 b

$ stat -f "%Sp %p" b
-rwxr--r-- 100744
```



## 6) 컨테이너 실행 실습

1. 컨테이너 실행 (hello world)
```bash
$docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
2. ubuntu 컨테이너 실행 (ls, echo)
```bash
$docker run -it --name pass ubuntu bash

$root@5eaff8e5795c:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

$root@5eaff8e5795c:/# echo hi>app
$root@5eaff8e5795c:/# ls  
app  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

$root@5eaff8e5795c:/# cat app
hi
```
3. attach & exec
백그라운드 컨테이너 실행 후 stat 확인
```bash
#1. attach 백그라운드 컨테이너 실행 후 stat 확인
$docker run -dit --name attach ubuntu

$docker attach attach

$root@6d07906df23e:/# exit
exit

$docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                      PORTS     NAMES
6d07906df23e   ubuntu        "/bin/bash"   30 seconds ago   Exited (0) 3 seconds ago              attach
```
```bash
#2. exec 백그라운드 컨테이너 실행 후 stat 확인
$docker run -dit --name exec ubuntu

$dave1392857@c3r3s7 practice % docker exec -it exec bash

$root@7091eb03dbae:/#exit
exit

$docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                      PORTS     NAMES
7091eb03dbae   ubuntu        "/bin/bash"   2 minutes ago    Up 2 minutes                          exec
```
- ==> attach 는 container PID 1(메인 프로세스)에 직접 연결

"exit = PID 1 종료" 

- ==> exec 는 container PID 2(bash)로 따로 연결 --- PID 1(메인 프로세스) 실행 중

"exit = bash 종료 / PID 1 실행"


- PID 1 접속 후 up 유지하기
```bash
#attach 접속 exit 하면서  up 상태 유지하기 
#1.단축키 (ctrl p + q)
$docker run -dit --name attach2 ubuntu
4df71753e9cd1502b8119f5c244b04d8812432c25ba144f72ad3d9c5ba89ef91

$docker attach --detach-keys="ctrl-d" attach2
#attach 후 변경 단축키(ctrl+d)

$ root@4df71753e9cd:/# read escape sequence

$docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                            PORTS     NAMES
4df71753e9cd   ubuntu        "/bin/bash"   23 seconds ago   Up 22 seconds                               attach2
```


  ## 4) dockerfile 커스텀
  - python, flsk 패키지 사용 
  1. requirements.txt 설치
  2. app.py 설치
  3. dockerfile 설치
   
 dave1392857@c3r3s7 practice % cat dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000


4. docker 커스텀 이미지

```bash
$ docker images d
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
dockerfile   1.0       a5bd26bb382c   55 seconds ago   142MB
```

 ## 5) docker 포트 매핑 실행 로그

 1. container 설치
```bash
$ docker ps -a 
CONTAINER ID   IMAGE            COMMAND           CREATED         STATUS         PORTS                                         NAMES
57baae126614   dockerfile:1.0   "python app.py"   6 seconds ago   Up 5 seconds   0.0.0.0:8000->5000/tcp, [::]:8000->5000/tcp   container
```


dave1392857@c3r3s7 practice % curl http://localhost:8000
Hello,  World!%                                                                                                                                    
CONTAINER ID   IMAGE            COMMAND           CREATED         STATUS         PORTS                                         NAMES
b46ecc3f1e61   dockerfile:1.0   "python app.py"   9 seconds ago   Up 8 seconds   0.0.0.0:3000->5000/tcp, [::]:3000->5000/tcp   container2
57baae126614   dockerfile:1.0   "python app.py"   6 minutes ago   Up 6 minutes   0.0.0.0:8000->5000/tcp, [::]:8000->5000/tcp   container

dave1392857@c3r3s7 practice % curl http://localhost:3000
Hello, World!%   



 ## 6) 볼륨 영속성 예시


 1. volume 생성

 dave1392857@c3r3s7 practice % docker volume create mydata
mydata

dave1392857@c3r3s7 practice % docker volume ls
DRIVER    VOLUME NAME
local     mydata


2. volume 연결 확인

dave1392857@c3r3s7 practice % docker run -dit --name container -v mydata:/app ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
689b91d88a0f: Pull complete 
Digest: sha256:84e77dee7d1bc93fb029a45e3c6cb9d8aa4831ccfcc7103d36e876938d28895b
Status: Downloaded newer image for ubuntu:latest
99e41a8245d69e2b41ec05692c3c4a9a3bceb4f805cae3beb6fda4823f0629af

root@99e41a8245d6:/# cd /app
root@99e41a8245d6:/app# echo hi>a.txt
root@99e41a8245d6:/app# ls
a.txt
root@99e41a8245d6:/app# cat a.txt
hi


3. volume 영속성 확인

dave1392857@c3r3s7 practice % docker run -dit --name container2 -v mydata:/app ubuntu bash
2d166de71daf06106094f98824c4191dc18abf72e0ef86f6b459d9466c782f29

dave1392857@c3r3s7 practice % docker exec -it container2 bash
root@2d166de71daf:/# cd /app
root@2d166de71daf:/app# ls
a.txt
root@2d166de71daf:/app# cat a.txt
hi


![github 연동](./docs/github.png)




## ) 트러블 슈팅
1. 컨테이너에 attach로 접속 후 stat up상태를 유지하며 나가려고 했는데 단축키(ctrl P + Q)가 안 먹혔다.
```bash
#단축키 전환 (ctrl +d)
$docker attach --detach-keys="ctrl-d" attach2

$root@4df71753e9cd:/# read escape sequence

$docker ps -a
CONTAINER ID   IMAGE         COMMAND       CREATED          STATUS                            PORTS     NAMES
4df71753e9cd   ubuntu        "/bin/bash"   23 seconds ago   Up 22 seconds                               attach2
```