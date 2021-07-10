# Docker
* [Docker 생활코딩](https://opentutorials.org/course/128/8657)
* [Docker 사용법](http://pyrasis.com/Docker/Docker-HOWTO)
* [Docker image 안을 sftp로 접근방법](https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220650722592&proxyReferer=https:%2F%2Fgeekcoders.tistory.com%2Fentry%2FDocker-Docker-%25EC%2584%25A4%25EC%25B9%2598%25EB%25B6%2580%25ED%2584%25B0-%25EA%25B8%25B0%25EB%25B3%25B8-%25EC%2582%25AC%25EC%259A%25A9)
* [Docker 란?](https://www.44bits.io/ko/post/easy-deploy-with-docker)
* [Docker, Kubernetes](https://medium.com/withj-kr/d-3eba3de2894e)
* [Docker youtube 기초 강의](https://www.youtube.com/watch?v=ePpiEy_C_jk&list=PLnIaYcDMsSczk-byS2iCDmQCfVU_KHWDk)
* [Docker 컨테이너 자동시작](https://help.iwinv.kr/manual/read.html?idx=572)
* [Docker logs 명령어 및 파일 위치](https://hoony-gunputer.tistory.com/entry/docker-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-log-%EB%82%A8%EA%B8%B0%EA%B8%B0)
* [Jenkins 와 Docker 그리고 AWS](https://pks2974.medium.com/jenkins-%EC%99%80-docker-%EA%B7%B8%EB%A6%AC%EA%B3%A0-aws-cli-%EC%82%BD%EC%A7%88%EA%B8%B0-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-e728986960e2)
##### 설치(ubuntu)
```
  $ sudo apt-get update
  $ sudo apt-get install docker.io
  $ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker # 링크
```
##### 공유폴더 설정
* [공유 폴더 설정하기](https://tttsss77.tistory.com/161)
```
docker -v <공유하고자 하는 호스트 시스템 디렉토리 절대 경로>:<호스트 시스템 디렉토리를 마운트할 컨테이너 내부 절대 경로> [IMAGE NAME]
```

##### 기본 명령어
```
  docker ps : 현재 실행중인 컨테이너 확인 (옵션 : -a 전체, -q 아이디만 보기)
  docker images : 저장된 이미지들 보기
  docker run <이미지이름 또는 아이디>: 컨테이너 생성 및 실행(이미지가 없을 경우 다운로드까지 진행)
    옵션 : -i 입력스트림 -t 터미널 기본적으로 -it 로 많이 사용
           -v 볼륨 연결, -d 백그라운드 실행, --name <사용할이름> 이름지정
  docker stop <컨테이너이름 또는 아이디>
  docker commit <옵션> <컨테이너 이름> <새로저장할 이미지 이름>
    옵션 : -a 작성자, -c 생성된 이미지에 도커파일 명령 적용, -m 커밋메세지, -p 커밋중 컨테어니 일시 중지
  docker diff <이미지 이름> : 본래 이미지와 달라진 파일 리스트 출력 (A 추가, D 삭제, C 수정)
  docker exec <이미지 이름> -it /bin/bash : 컨테이너 안으로 진입
  docker inspect : 이미지와 컨테이너 설정 확인
  docker logs : stdout 확인
  docker rm : 컨테이너삭제
  docker rmi : 이미지 삭제
```
##### DockerFile
* [DockerFile 작성법](https://velog.io/@seheon99/Dockerfile-%EC%9E%91%EC%84%B1-%EB%B0%A9%EB%B2%95-12)

```
  # DockerFile 작성 옵션
  FROM : 베이스가 될 도커 이미지 이름 (기반이 되는 이미지, <이미지 이름>:<태그> 형식으로 설정)
  MAINTAINER : 작성자 정보
  RUN : Shell Script 또는 명령을 실행(보통 패키지 설치에 사용 apt-get update > apt-get install -y flask)
  CMD : 컨테이너를 실행할 때 사용할 default를 설정
  LABEL : 라벨 작성 (docker inspect 명령으로 label 확인할 수 있습니다.)
  EXPOSE : 호스트와 연결할 포트 번호를 설정한다.
  ENV : 환경변수 설정
  ADD : 호스트 OS또는 원격 URL에 파일 또는 디렉토리 복사
  COPY : 호스트 OS에 파일 또는 디렉토리 복사
  ENTRYPOINT : 컨테이너가 시작되었을 때 스크립트 실행(docker run 이후 나오는 명령어에 인수만 받고 명령어는 미리 등록된 명령어가 실행)
  VOLUME : 볼륨 마운트(이미지에 지정한 경로의 파일을 호스트에 /var/lib/docker/volume/ 경로에 저장 
                      도커가 지정한 해시값으로 저장되므로 나중에 찾기 힘듬 기본적으로 도커를 실행할때 -v 옵션을 사용)
  USER : 명령 실행할 사용자 권한 지정
  WORKDIR : "RUN", "CMD", "ENTRYPOINT" 명령이 실행될 작업 디렉터리
  ARG : Dockerfile 내부 변수
  ONBUILD : 다른 이미지의 Base Image로 쓰이는 경우 실행될 명령 수행
  SHELL : Default Shell 지정
```
* [RUN, CMD, ENTRYPOINT의 차이](https://nirsa.tistory.com/66)
* [YAML 문법](https://subicura.com/k8s/prepare/yaml.html#%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB%E1%84%86%E1%85%AE%E1%86%AB%E1%84%87%E1%85%A5%E1%86%B8)
* [YAML TO JSON](https://onlineyamltools.com/convert-yaml-to-json)
* [Docker Compose를 활용한 개발환경 구성](https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose)
* [Docker Compose 커맨드](https://www.daleseo.com/docker-compose/)
* [Docker Compose 공식문서](https://docs.docker.com/compose/)
```
  # Docker Compose 옵션
  version : <사용할 docker compose 버전>
  services : # 컨테이너들정보들을 가지고 있는 맵(key, value)
    <컨테이너 이름>:
      image: <Docker Hub에 있는 이미지 명 : <태그>
      restart: <자동 재시작 옵션 always 항상재시작, "no" 기본값 재시작하지 않음, unless-stopped 수동으로 중지한 경우를 제외하고 재시작>
      logging: <로그 옵션>
        driver: "json-file"
        options:
          max-file: "5" <파일 갯수>
          max-size: "100m" <파일 최대 크기>
      volumes: # docker run 에 -v 옵션과 동일한 역할(배열 형태)
        - <호스트에경로>:<컨테이너내부경로>
      environment: # 환경 변수 및 컨피그 옵션 등(배열형태)
        - MYSQL_PASSWORD=password
        - TZ="Asia/Seoul" # 시간대 설정(서울로 시간대 변경 timezone)
      ports: #사용할 포트(배열)
        - <외부포트>:<내부포트>
    <컨테이너 이름>:
      ....
```  
  
```  
  # Docker Compose 명령
  docker-compose up -d : 실행
  docker-compose ls : 조회
  docker-compose stop : 중지
  docker-compose down : 생성된 컨테이너 삭제 <해당 명령을 수행하면 docker log가 다 삭제됨>
      
  
            
```
##### requirements.txt로 모듈 설치시 mysql_config Error 대처법
```
  FROM python:3.8.5-slim ## -slim = apt-get이 설치된 버전의 이미지
  
  RUN apt-get update
  RUN apt-get install default-libmysqlclient-dev gcc  -y
  RUN pip install -r requirements.txt
```
##### 컨테이너 내에 타임존 설정(Dockerfile)
```
  ARG DEBIAN_FRONTEND=noninteractive
  ENV TZ=Asia/Seoul
  RUN apt-get install -y tzdata
```
