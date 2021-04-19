# Docker
* [Docker 생활코딩](https://opentutorials.org/course/128/8657)
* [Docker 사용법](http://pyrasis.com/Docker/Docker-HOWTO)
* [Docker image 안을 sftp로 접근방법](https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220650722592&proxyReferer=https:%2F%2Fgeekcoders.tistory.com%2Fentry%2FDocker-Docker-%25EC%2584%25A4%25EC%25B9%2598%25EB%25B6%2580%25ED%2584%25B0-%25EA%25B8%25B0%25EB%25B3%25B8-%25EC%2582%25AC%25EC%259A%25A9)
* [Docker 란?](https://www.44bits.io/ko/post/easy-deploy-with-docker)
* [Docker, Kubernetes](https://medium.com/withj-kr/d-3eba3de2894e)
* [Docker youtube 기초 강의](https://www.youtube.com/watch?v=ePpiEy_C_jk&list=PLnIaYcDMsSczk-byS2iCDmQCfVU_KHWDk)

##### 공유폴더 설정
* [공유 폴더 설정하기](https://tttsss77.tistory.com/161)
```
host system directory : 공유하고자 하는 호스트 시스템 디렉토리 절대 경로
container directory : 호스트 시스템 디렉토리를 마운트할 컨테이너 내부 절대 경로
docker -v <host system directory>:<container directory> [IMAGE NAME]
docker -volume="<host system directory>:<container directory>" [IMAGE NAME]
```

##### 기본 명령어
```
  docker ps : 현재 실행중인 컨테이너 확인 (옵션 : -a 전체, -q 아이디만 보기)
  docker images : 저장된 이미지들 보기
  docker run <이미지이름 또는 아이디>: 컨테이너 생성 및 실행(이미지가 없을 경우 다운로드까지 진행)
    옵션 : -i 입력스트림 -t 터미널 기본적으로 -it 로 많이 사용
           -v 볼륨 연결, -d 백그라운드 실행, --name <사용할이름> 이름지정
  docker stop <컨테이너이름 또는 아이디>
  docker rm : 컨테이너삭제
  docker rmi : 이미지 삭제
```
