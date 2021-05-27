# Server

* [SSL 인증서 생성,사설 인증서 생성](https://namjackson.tistory.com/24)
* [구글 검색 안되게 하기](https://ragonfly.tistory.com/entry/%EA%B5%AC%EA%B8%80%EC%97%90%EC%84%9C-%EA%B2%80%EC%83%89-%EC%95%88%EB%90%98%EA%B2%8C-%ED%95%98%EB%8A%94%EB%B2%95)
* DNS의 설정을 변경하려면, 도메인 업체가 아닌 네임서버에서 쪽에서 변경해야 변경. 
  * ex) AWS EC2 인스턴스에 Route 53으로 연결하고 도메인을 가비아에서 사서 연결할 경우 Route53에서 설정을 변경해야 반영.
  * ex2) 메일 서버를 연결할 경우 Route53에서 mx 추가, 인증을 txt 로할경우 txt 
  
* [ubuntu 프로세스 관리 supervisor 설치와 사용법](https://devlog.jwgo.kr/2016/11/07/how-to-use-supervisor-in-one-minute/)
* [채팅서버의 부하 분산 사례 slideshare](https://www.slideshare.net/JohnKim0331/ss-52091187?from_m_app=android)
* [PM2 사용법](https://engineering.linecorp.com/ko/blog/pm2-nodejs/)
* [PM2 로그관리 모듈](https://lahuman.jabsiri.co.kr/258)

```
 # pm2 로 파이썬 실행
 pm2 start run.py --interpreter=python
 # 오류발생시
 pm2 start job1.py --name job1 --interpreter python3
```
#### supervisor 명령어
```
   supervisord :  프로세스 관리 및 모니터링을 위한 프로그램 
   supervisorctl : supervisor내에 프로그램 관리, 프로그램 추가, 재가동 등등... 

   supervisord 구동

   supervisord  : start
   kill $pid       : stop

   supervisorctl 사용
   status                # 모든 프로세스 보기
   avail                  # 설정 프로세스 보기
   exit / quit           # shell에서 나가기
   start                  # 등록된 프로세스 시작
   stop                  # 등록된 프로세스 중지
   restart                # 등록된 프로세스 재시작
   reload                # supervisord 재시작
   reread                # 설정 파일 다시 읽기
 
```
* [flask는 프로덕션 서버가 아닙니다.](https://build.vsupalov.com/flask-web-server-in-production/)
* [flask and nginx](http://egloos.zum.com/mcchae/v/11149241)
* [에러 추적(Error Tracking) 및 로그 취합(logging aggregation) 시스템인 Sentry](https://www.lesstif.com/system-admin/error-tracking-logging-aggregation-sentry-30705079.html)
* [ubuntu 패키지 관리하기, 여러개 패키지 중 대표 버전설정](https://www.whatwant.com/entry/update-alternatives-%EC%97%AC%EB%9F%AC-%EB%B2%84%EC%A0%84%EC%9D%98-%ED%8C%A8%ED%82%A4%EC%A7%80-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)

* [Nginx](https://opentutorials.org/module/384/3462)
* [Nginx, Gunicorn(+ WSGI) 개념 이해 및 활용](https://www.opentutorials.org/module/4936/28881)
* [Nginx 설치 및 기본 환경 설정](https://kscory.com/dev/nginx/install)
* [AWS EC2 ubuntu Nginx 기본 설치가이드](https://erulabo.com/post/aws-ec2-how-to-install-nginx-server)
* [Nginx + Gunicorn + flask 연동](https://velog.io/@yvvyoon/flask-nginx-gunicorn-1)
* [AWS CICD pipeline build](https://medium.com/better-programming/how-to-build-a-ci-cd-pipeline-in-aws-in-5-minutes-and-58-seconds-4de156477042)
* [AWS CICD Automation](https://aws-diary.tistory.com/26)
* [AWS를 이용한 간략 지속적 통합 예제, 무중단 배포 자동화 CI & CD, CodeBuild, CodeDeploy, CodePipeline](https://roka88.dev/97)
* [Foward Proxy 와 Reverse Proxy 차이](https://bcp0109.tistory.com/194)
* [Server 운용 방법 5가지](https://blog.msalt.net/77)
## MSA

* [MicroService for AWS](https://www.slideshare.net/awskorea/3-microservice-aws-architecture-pattern-usecase)
* [MicroService and Serverless](https://waspro.tistory.com/495)
* [MSA란](https://blog.neonkid.xyz/200?category=830544)


## cron
* [Cron 사용법](https://www.letmecompile.com/scheduler-cron-tutorial/)
* [Crontab 명령어](https://ojava.tistory.com/154)

## sysstat
* [sysstat사용법](https://brunch.co.kr/@lars/9)

## homebrew
```
 # 설치 및 변경이 안될때 해당 경로 아래의 모든 소유를 바꿈
 sudo chown -R $(whoami) $(brew --prefix)/*
 
 # 브류업데이트로 파이썬 버전이 업데이트 돼서 심볼릭 링크가 깨졌을때(3.8>3.9로 변경되어서 되돌릴때)
 brew install python@3.8
 brew unlink python@3.9
 brew link python@3.8 # 이 명령어가 안되면 brew link --overwrite --dry-run python@3.8
```

