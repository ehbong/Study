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
