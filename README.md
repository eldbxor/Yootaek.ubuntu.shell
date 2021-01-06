# Server Management

## 용량 확인
### 용량을 많이 차지하는 경로 확인
```bash
du -x -h / | sort -h | tail -40 | sort -h -r
```

### 현재 경로의 용량 확인
```bash
$ du -hs *
```

## Docker
### 자주 쓰는 명령어
```bash
$ docker images // docker 이미지 목록 조회

$ docker run <옵션> <이미지 이름> <실행할 파일> // 컨테이너 생성과 시작

$ docker ps // 현재 실행중인 컨테이너 목록

$ docker ps -a // 생성한 전체 컨테이너 목록

$ docker inspect [NAME|ID] | grep IP // IP 관련 정보 보기
```

### 이미지 생성 / 컨테이너 생성
```bash
$ docker build --tag node_server:0.0.1 [Dockerfile이 위치하는 경로]

$ docker create --name [서버명] -p [외부 포트:컨테이너 내부포트] [이미지명:버전태그]
```


### 안쓰는 이미지와 컨테이너 삭제
```bash
$ docker system prune -a -f

$ docker rmi <Image ID>
```

### 모든 컨테이너 죽이기/삭제
```bash
$ docker kill $(docker ps -q)

$ docker rm $(docker ps -a -q)
```

### 볼륨 만들기
```bash
$ docker volume create --name myvolume  # --name : myvolume 이름의 볼륨 생성

$ docker volume ls # 생성된 볼륨을 확인
```

### 컨테이너 로그 보기
```bash
$ docker logs <Container ID>
```

### Docker Log 설정
```bash
$ vi /etc/docker/daemon.json  
 {
 "log-driver": "json-file",
 "log-opts": {
     "max-size": "100m",    
     "max-file": "3"    
     }
 } 
```

### Docker Log 옵션
```bash
$ docker logs -f <Container> // 로그를 계속 모니터링

$ docker logs --tail <log 개수> <Container> // 원하는 개수만큼 마지막부터 로그 출력

$ docker logs -t <Container> // Timestamp를 같이 출력
```

### Docker Container 접속
```bash
$ docker exec -it <Container ID> /bin/bash // -it: STDIN 표준 입출력을 열고 가상 tty를 통해 접속하겠다는 의미

$ docker attach <Container name> // 쉘 없이 접속, 서버 로그를 볼 수 있음(접속 종료: Ctrl + p + q)

```

### Container 시작/재시작/정지
```bash
$ docker start <container name>

$ docker restart <container name>

$ docker stop <container name>
```

### Docker Compose
```bash
$ docker-compose build

$ docker-compose up [-d]

$ docker-compose down
```

### Docker Low-level 정보를 가져오기
옵션

--format, -f // Format the output using the given Go template

--size, -s // Display total file sizes if the type is container

--type // Return JSON for specified type

```bash
# docker inspect [OPTIONS] NAME|ID [NAME|ID]
```

### Docker 명령어 Root 권한 없이 사용하기
```bash
$ sudo groupadd docker // 이미 docker 그룹이 있다면 생략

$ sudo usermod -aG docker $USER
```

## Nginx
```bash
$ nginx // 실행

$ nginx -s stop // 강제 종료

$ nginx -s quit // request처리 종료하고 난뒤 nginx 정지

$ nginx -s reload // 설정파일 다시 읽어들임

$ nginx -s reopen // nginx 재실행 중에 로그파일을 다시 오픈
```

## 사용자 설정

### Sudo 명령어 비밀번호 없이 사용하기
```bash
$ (사용자명) ALL=(ALL:ALL) NOPASSWD:ALL // 맨 아래에 추가
```

### 사용자 계정 속성 변경
```bash
# usermod [옵션] [계정명]
-u: 사용자 계정의 UID 생성
-g: 사용자 계정의 1차 그룹의 GID 지정
-G: 사용자 계정의 2차 그룹의 GID 지정
-c: Comment
-d: 사용자의 홈디렉토리를 지정
-e: 사용자의 계정 만기일 지정
-f: 사용자의 계정 유효일 지정
-s: 로그인 시 사용할 기본 쉘 지정
```
