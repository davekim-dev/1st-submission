# 1st-submission

 ## 1) 실행 환경
- OS: UDarwin c3r3s7.codyssey.kr 24.6.0 Darwin Kernel Version 24.6.0: Mon Jan 19 22:00:10 PST 2026; root:xnu-11417.140.69.708.3~1/RELEASE_X86_64 x86_64

- Shell:/bin/zsh
- Docker: 28.5.2
- Git: 2.53.0
- Terminal: MallocNanoZone=0
USER=dave1392857
COMMAND_MODE=unix2003
__CFBundleIdentifier=com.microsoft.VSCode

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

 ## 3) 수행 로그(발췌)
 - 현재 위치 확인 : pwd
 - 목록 확인: ls(파일만) ls -l(파일 권한) ls -la(숨김 파일)
 - 이동: mv 파일명.txt 새경로/파일.txt.    , (상위로 이동) mv 파일명.txt ../파일명.txt
 - 이름변경: mv 옛이름.txt 새이름.txt
 - 폴더 생성: mkdir 폴더명   / (상위-하위) mkdir -p 이름1/이름2 .. 
 - 파일 생성: touch 파일명.txt / (내용 담아서) echo 내용 > 파일명.txt
 - 삭제: (파일 삭제) rm 파일명.txt.  /  (폴더 삭제) rm -r 이름 ,   (하위도 같이 삭제) rm -r e
 - 복사: cp 파일명.txt 복사파일명.txt

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