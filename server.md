# Server

* [SSL 인증서 생성,사설 인증서 생성](https://namjackson.tistory.com/24)
* [구글 검색 안되게 하기](https://ragonfly.tistory.com/entry/%EA%B5%AC%EA%B8%80%EC%97%90%EC%84%9C-%EA%B2%80%EC%83%89-%EC%95%88%EB%90%98%EA%B2%8C-%ED%95%98%EB%8A%94%EB%B2%95)
* [DNS A레코드, CNAME 차이](https://dev.plusblog.co.kr/30)
* [gRPC 공식문서](https://grpc.io/)
* [Golang gRPC server 구축하기](https://devjin-blog.com/golang-grpc-server-1/)
* [gRPC GIT](https://github.com/grpc)
> SSH 접속시 RSA 공유키 충돌문제 REMOTE HOSt IDENTIFICATION HAS CHANGED
```zsh
  ssh-keygen -R <IP 또는 주소>
```
> DNS의 설정을 변경하려면, 도메인 업체가 아닌 네임서버에서 쪽에서 변경해야 변경. 
> * ex) AWS EC2 인스턴스에 Route 53으로 연결하고 도메인을 가비아에서 사서 연결할 경우 Route53에서 설정을 변경해야 반영.
> * ex2) 메일 서버를 연결할 경우 Route53에서 mx 추가, 인증을 txt 로할경우 txt 
  
* [ubuntu 프로세스 관리 supervisor 설치와 사용법](https://devlog.jwgo.kr/2016/11/07/how-to-use-supervisor-in-one-minute/)
* [채팅서버의 부하 분산 사례 slideshare](https://www.slideshare.net/JohnKim0331/ss-52091187?from_m_app=android)
* [Server 운용 방법 5가지](https://blog.msalt.net/77)
* [Naver 메인페이지 트래픽처리 방법](https://d2.naver.com/helloworld/6070967)
* [Bash:_systemctl:_command_not_found](https://zetawiki.com/wiki/Bash:_systemctl:_command_not_found)
```zsh
## 우분트 시스템에 자동업데이트 서비스로 인해 문제가 생길때
sudo systemctl stop apt-daily.timer
sudo systemctl disable apt-daily.timer
sudo systemctl disable apt-daily.service

sudo systemctl stop apt-daily-upgrade.timer
sudo systemctl disable apt-daily-upgrade.timer
sudo systemctl disable apt-daily-upgrade.service

sudo systemctl daemon-reload
```

#### PM2
* [PM2 사용법](https://engineering.linecorp.com/ko/blog/pm2-nodejs/)
* [PM2 로그관리 모듈](https://lahuman.jabsiri.co.kr/258)

```zsh
 # pm2 로 파이썬 실행
 pm2 start run.py --interpreter=python
 # 오류발생시
 pm2 start job1.py --name job1 --interpreter python3
```
#### supervisor 명령어
```zsh
 supervisord :  프로세스 관리 및 모니터링을 위한 프로그램 
 supervisorctl : supervisor내에 프로그램 관리, 프로그램 추가, 재가동 등등... 

 supervisord 구동

 supervisord  : start
 kill $pid       : stop

 supervisorctl 사용
 supervisorctl status                # 모든 프로세스 보기
 supervisorctl avail                  # 설정 프로세스 보기
 supervisorctl exit / quit           # shell에서 나가기
 supervisorctl start                  # 등록된 프로세스 시작
 supervisorctl stop                  # 등록된 프로세스 중지
 supervisorctl restart                # 등록된 프로세스 재시작
 supervisorctl reload                # supervisord 재시작
 supervisorctl reread                # 설정 파일 다시 읽기
 
```
* [ubuntu 패키지 관리하기, 여러개 패키지 중 대표 버전설정](https://www.whatwant.com/entry/update-alternatives-%EC%97%AC%EB%9F%AC-%EB%B2%84%EC%A0%84%EC%9D%98-%ED%8C%A8%ED%82%A4%EC%A7%80-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)
* [에러 추적(Error Tracking) 및 로그 취합(logging aggregation) 시스템인 Sentry](https://www.lesstif.com/system-admin/error-tracking-logging-aggregation-sentry-30705079.html)

## nginx
* [flask는 프로덕션 서버가 아닙니다.](https://build.vsupalov.com/flask-web-server-in-production/)
* [flask and nginx](http://egloos.zum.com/mcchae/v/11149241)
* [Nginx](https://opentutorials.org/module/384/3462)
* [Nginx, Gunicorn(+ WSGI) 개념 이해 및 활용](https://www.opentutorials.org/module/4936/28881)
* [Nginx 설치 및 기본 환경 설정](https://kscory.com/dev/nginx/install)
* [Nginx 캐시 설정](https://medium.com/@tunacan252/nginx%EC%9D%98-%EC%BA%90%EC%8B%9C-%EC%84%A4%EC%A0%95-2666f6dc7ab9)
* [AWS EC2 ubuntu Nginx 기본 설치가이드](https://erulabo.com/post/aws-ec2-how-to-install-nginx-server)
* [Nginx + Gunicorn + flask 연동](https://velog.io/@yvvyoon/flask-nginx-gunicorn-1)
* [Foward Proxy 와 Reverse Proxy 차이](https://bcp0109.tistory.com/194)
* [nginx 프록시 패스 리다이렉션 무시](https://serverfault.com/questions/363159/nginx-proxy-pass-redirects-ignore-port)
* [nginx 튜닝](https://couplewith.tistory.com/entry/%EA%BF%80%ED%8C%81-%EA%B3%A0%EC%84%B1%EB%8A%A5-Nginx%EB%A5%BC%EC%9C%84%ED%95%9C-%ED%8A%9C%EB%8B%9D-1-%EB%94%94%EC%8A%A4%ED%81%AC%EC%9D%98-IO-%EB%B3%91%EB%AA%A9-%EC%A4%84%EC%9D%B4%EA%B8%B0)
```
  # nginx.conf 포트 고정(프록시 리다이렉트 무시)할때 설정 $host를 $http_host로 변경
  proxy_set_header Host $host; > proxy_set_header Host $http_host; 
```


## CI/CD
* [AWS CICD pipeline build](https://medium.com/better-programming/how-to-build-a-ci-cd-pipeline-in-aws-in-5-minutes-and-58-seconds-4de156477042)
* [AWS CICD Automation](https://aws-diary.tistory.com/26)
* [AWS를 이용한 간략 지속적 통합 예제, 무중단 배포 자동화 CI & CD, CodeBuild, CodeDeploy, CodePipeline](https://roka88.dev/97)
* [jenkins & Docker](https://pks2974.medium.com/jenkins-%EC%99%80-docker-%EA%B7%B8%EB%A6%AC%EA%B3%A0-aws-cli-%EC%82%BD%EC%A7%88%EA%B8%B0-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-e728986960e2)
* [jenkins flask 연동](https://velog.io/@inyong_pang/devops-jenkins-flask-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%97%B0%EB%8F%99)
* [jenkins github 연동](https://goddaehee.tistory.com/258)
* [jenkins github 연결설정](https://bcho.tistory.com/1237)
* [CI/CD 툴 비교](https://medium.com/day34/ci-cd-tool-comparison-f710a4777852)

## MSA
* [MicroService for AWS](https://www.slideshare.net/awskorea/3-microservice-aws-architecture-pattern-usecase)
* [MicroService and Serverless](https://waspro.tistory.com/495)
* [MSA란](https://blog.neonkid.xyz/200?category=830544)
* [MSA 선택의 이유(카카오 이모티콘서비스에 )](https://tech.kakao.com/2021/09/14/msa/)


## cron
* [Cron 사용법](https://www.letmecompile.com/scheduler-cron-tutorial/)
* [Crontab 명령어](https://ojava.tistory.com/154)

## sysstat
* [sysstat사용법](https://brunch.co.kr/@lars/9)

## homebrew
```zsh
 # 설치 및 변경이 안될때 해당 경로 아래의 모든 소유를 바꿈
 sudo chown -R $(whoami) $(brew --prefix)/*
 
 # 브류업데이트로 파이썬 버전이 업데이트 돼서 심볼릭 링크가 깨졌을때(3.8>3.9로 변경되어서 되돌릴때)
 brew install python@3.8
 brew unlink python@3.9
 brew link python@3.8 # 이 명령어가 안되면 brew link --overwrite --dry-run python@3.8
```

## Ansible
* [Ansible 공식 튜토리얼](https://www.redhat.com/ko/topics/automation/learning-ansible-tutorial)

## python
```zsh
  # python 명령어로 python3 실행하기
  ~/.bashrc 또는 ~/.bash_aliases 파일에 아래의 내용을 추가

  alias python=python3
  alias pip=pip3
  그리고 이를 적용하기 위해 source ~/.bashrc 또는 source ~/.bash_aliases를 실행

  $ python --version
  Python 3.6.9
```
## cookiecutter
* [cookiecutter ](https://cookiecutter.readthedocs.io/en/latest/installation.html)

## Traefik
> Traefik( 트래픽으로 발음 )은 마이크로서비스를 쉽게 배포할 수 있게 해주는 최신 HTTP 역방향 프록시 및 로드 밸런서
* [traefik Github](https://github.com/traefik/traefik)
