# Server

* [SSL 인증서 생성,사설 인증서 생성](https://namjackson.tistory.com/24)
* [구글 검색 안되게 하기](https://ragonfly.tistory.com/entry/%EA%B5%AC%EA%B8%80%EC%97%90%EC%84%9C-%EA%B2%80%EC%83%89-%EC%95%88%EB%90%98%EA%B2%8C-%ED%95%98%EB%8A%94%EB%B2%95)
* [인증 인가 시스템(쿠키, 세션, 토큰)](https://dev.gmarket.com/45)
* [DNS A레코드, CNAME 차이](https://dev.plusblog.co.kr/30)
* [세션 동작 원리](https://thecodinglog.github.io/web/2020/08/11/what-is-session.html)
* [프로세스, 서비스(데몬) 차이](https://inpa.tistory.com/entry/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8D%B0%EB%AA%AC-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%A0%95%EB%A6%AC)
* [시스템 설계에 대해](https://velog.io/@lshn1007/System-Archi-1-%EC%82%AC%EC%9A%A9%EC%9E%90-%EC%88%98%EC%97%90-%EB%94%B0%EB%A5%B8-%EA%B7%9C%EB%AA%A8%EC%9D%98-%ED%99%95%EC%9E%A5%EC%84%B1)

> 상태 코드
* [http 상태 코드 정리](https://www.whatap.io/ko/blog/40/)
```
 200(성공) 요청 처리 성공
 201(등록성공) 요청을 등록하는 데 성공 주로 POST, PUT 사용 시 리턴
 202(수신성공 비처리) 요청을 수신했지만 처리할 수 없음
 300(다증응답) 요청에 대해 여러 응답이 가능
 301(이동) 요청한 URI변경
 302(일시적이동) 요청한 URI가 일시적으로 변경
 400(잘못된요청) 잘못된 문법요청으로 서버가 이해할 수 없음
 401(미인증) 인증에 대한 정보가 없음
 403(미권한) 보유한 인증정보로 접근권한이 없음
 404(없음) 찾을 수 없는 응답
 413(크기초과) payload 크기 초과
 500(내부서버오류) 서버오류 발생
 501(구현되지 않음) 메소드인식 불가
 502(게이트웨이 오류) 게이트웨이에서 발생한 오류
 504(게이트웨이 타임아웃) 제 시간에 요청을 받지 못했을 경우
```
* [REST API 규칙](https://velog.io/@gga4638/REST-API-URI-%EB%94%94%EC%9E%90%EC%9D%B8-%EA%B7%9C%EC%B9%99)
* [REST API, Soap 차이](https://velog.io/@zioo/JSON-API-SOAP)
* [websocket 클러스터](https://medium.com/@mohsenes/websocket-cluster-with-nestjs-and-redis-a18882d418ed)
* [websocket 서버 이슈 및 대처, 우하한 기술 블로그](https://techblog.woowahan.com/2547/)

> Cookie 보안  
> * HttpOnly: 자바스크립트 접근을 제한

```javascript
// 서버에서 쿠키 생성 (Node.js와 Express 예제)
res.cookie('sessionID', 'abcdef', { httpOnly: true });
```
> * Secure: https 환경에서만 전송

```javascript
// 서버에서 쿠키 생성 (Node.js와 Express 예제)
res.cookie('sessionID', 'abcdef', { secure: true });
```

> * SmaeSite: CSRF 공격 방지를 위해 외부 도메인 요청 차단

```javascript
// 서버에서 쿠키 생성 (Node.js와 Express 예제)
res.cookie('sessionID', 'abcdef', { sameSite: 'strict' });
```

> * Expiration (Max-Age): 유효기간 설정

```javascript
// 서버에서 쿠키 생성 (Node.js와 Express 예제)
res.cookie('sessionID', 'abcdef', { maxAge: 3600000 }); // 1시간 유효
```

> * Domain 및 Path 설정: 특정 주소에서만 쿠키 접근

```javascript
// 서버에서 쿠키 생성 (Node.js와 Express 예제)
res.cookie('sessionID', 'abcdef', { domain: '.example.com', path: '/app' });
```
----

###### [브라우저 캐시](https://www.rfc-editor.org/rfc/rfc2068#section-14.9)
>* ETag: 수정을 확인할 수 있는 버전 등을 저장해서 수정 여부에 따라 캐시를 사용하는 헤더
>	1. 요청을 받으면 서버가 수정을 구분할 수 있는 값을 헤더에 ETag 키로 담아 반환 
>	2. 브라우저가 서버에서 ETag를 받고, 저장
>	3. 같은 요청 발생 시 헤더에 if-none-match 키로 ETag 값을 실어서 서버에 요청
>	4. 서버는 if-none-match 값을 확인해서 수정 여부를 알 수 있는 값과 비교해서 같으면 304 코드를 반환, 아니면 새로운 값을 200으로 반환
>* Last-Modified: 마지막 수정 날짜를 기록해서 비교하여 캐시
>	1. 요청을 받으면 서버는 마지막 수정 시간을 헤더에 Last-Modified 키로 담아 반환
>	2. 브라우저가 서버에서 Last-Modified를 받고 저장
>	3. 같은 요청 발생 시 헤더에 if-modified-since 키로 Last-Modified 값을 실어서 서버에 요청
>	4. 서버는 if-modified-since 값과 수정시간을 비교해서 같으면 304코드를 반환, 아니면 새로운 값과 200을 반환
>* Cache-Control: 캐시를 어떻게 처리할 것인 가를 지정
>	 * no-cache: 캐시 사용 전 서버에 유효성 검사 필요(위의 Etag, Last-Modified 등을 이용해 검증)
>	 * no-store: 응답을 캐싱하지않음
>	 * max-age: 초 단위로 응답을 캐싱할 시간을 지정(변경하지 않을 파일도 최대 1년을 권장)
>	   이 경우 파일 변경 시, 파일이름 변경 등을 통해 캐싱을 회피
>	 * immutable: 리소스가 변경되지 않음


```

> SSH 접속시 RSA 공유키 충돌문제 REMOTE HOSt IDENTIFICATION HAS CHANGED
```zsh
  ssh-keygen -R <IP 또는 주소>
```
> DNS의 설정을 변경하려면, 도메인 업체가 아닌 네임서버에서 쪽에서 변경해야 변경. 
> * ex) AWS EC2 인스턴스에 Route 53으로 연결하고 도메인을 가비아에서 사서 연결할 경우 Route53에서 설정을 변경해야 반영.
> * ex2) 메일 서버를 연결할 경우 Route53에서 mx 추가, 인증을 txt 로할경우 txt 
  
* [ubuntu 프로세스 관리 supervisor 설치와 사용법](https://devlog.jwgo.kr/2016/11/07/how-to-use-supervisor-in-one-minute/)

### APM 모니터링
* [모니터링 Prometheus and Grafana](https://essem-dev.medium.com/%ED%94%84%EB%A1%9C%EB%A9%94%ED%85%8C%EC%9A%B0%EC%8A%A4%EC%99%80-%EA%B7%B8%EB%9D%BC%ED%8C%8C%EB%82%98%EB%A1%9C-%EA%B0%9C%EB%B0%9C-%EC%84%9C%EB%B2%84-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81%ED%95%98%EA%B8%B0-8942aea724b3)
* [도커 컴포즈 활용 Prometheus and Grafana 설치](https://danawalab.github.io/common/2020/03/16/Common-Prometheus.html)
* [nginx-prometheus-exporter](https://gurumee92.tistory.com/231)
* [grafana dashboard labs](https://grafana.com/grafana/dashboards/)
* [grafana alert 설정](https://ksr930.tistory.com/177)
* [프로메테우스와 그라파나](https://velog.io/@moey920/%EC%95%88%EC%A0%95%EC%A0%81%EC%9D%B8-%EC%9A%B4%EC%98%81%EC%9D%84-%EC%99%84%EC%84%B1%ED%95%98%EB%8A%94-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81.-%ED%94%84%EB%A1%9C%EB%A9%94%ED%85%8C%EC%9A%B0%EC%8A%A4%EC%99%80-%EA%B7%B8%EB%9D%BC%ED%8C%8C%EB%82%98)
* [에러 추적(Error Tracking) 및 로그 취합(logging aggregation) 시스템인 Sentry](https://www.lesstif.com/system-admin/error-tracking-logging-aggregation-sentry-30705079.html)
* [Sentry 도입기 from Line](https://engineering.linecorp.com/ko/blog/log-collection-system-sentry-on-premise)
* [프론트 모니터링 bugsnag 공식](https://www.bugsnag.com/)
* [프론트 모니터링 bugsnag git](https://github.com/bugsnag)
* [자바 기반 어플리케이션 대상 모니터링 도구 scouter](https://developercc.tistory.com/30)


### 분산처리
* [채팅서버의 부하 분산 사례 slideshare](https://www.slideshare.net/JohnKim0331/ss-52091187?from_m_app=android)
* [Server 운용 방법 5가지](https://blog.msalt.net/77)
* [Naver 메인페이지 트래픽처리 방법](https://d2.naver.com/helloworld/6070967)

* [Bash:_systemctl:_command_not_found 오류](https://zetawiki.com/wiki/Bash:_systemctl:_command_not_found)
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


## nginx
> Nginx 특징
> * 웹서버: 정적 파일 서빙 및 WAS 연동 처리
> * 역방향프록시: 서버 앞에 프록시 서버를 두어서 클라이언트 요청을 중계(정방향프록시는 클라이언트 앞에서 요청을 중계)
>   * 로드밸런싱: 트래픽을 분배
>   * 보안: 클라이언트가 서버의 IP를 직접적으로 알 수 없음, IP기반 인증 및 엑세스 제어 등 기능
>   * SSL/TLS 종단점: WAS서버가 부담하는 SSL/TLS 암호화 트래픽을 처리해서 부담 감소
>   * 캐싱: 정적파일 및 동적 파일 캐싱
>   * 가상 호스팅: 같은 IP주소로 들어오는 여러개의 도메인에 대해 구분하여 중계
> * HTTP/2 지원: 로딩 단축 및 성능향상
> * 로그 및 모니터링: 웹서버 동작에 대해 로그 기능 

* [flask and nginx](http://egloos.zum.com/mcchae/v/11149241)
* [Nginx](https://opentutorials.org/module/384/3462)
* [Nginx, Gunicorn(+ WSGI) 개념 이해 및 활용](https://www.opentutorials.org/module/4936/28881)
* [Nginx 설치 및 기본 환경 설정](https://kscory.com/dev/nginx/install)
* [websocket 프록시 설정](https://shinwusub.tistory.com/111)
* [Nginx 캐시 설정](https://medium.com/@tunacan252/nginx%EC%9D%98-%EC%BA%90%EC%8B%9C-%EC%84%A4%EC%A0%95-2666f6dc7ab9)
* [Nginx 마이크로 캐시](https://couplewith.tistory.com/entry/%EA%BF%80%ED%8C%81%EA%B3%A0%EC%84%B1%EB%8A%A5-Nginx%EB%A5%BC%EC%9C%84%ED%95%9C-%ED%8A%9C%EB%8B%9D5-%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%BA%90%EC%8B%B1)
```
  proxy_cache_key 를 설정할때는 주의 해서 설정, 같은 호출이라고 판단하면 다른 호출에 대해 같은 결과 값을 반환
  $scheme
  $request_method
  $host
  $uri
  $is_args
  $args
  $request_body
  $content_length
  $remote_addr
  $query_string
```
* [$ 변수 목록](http://nginx.org/en/docs/varindex.html)
* [AWS EC2 ubuntu Nginx 기본 설치가이드](https://erulabo.com/post/aws-ec2-how-to-install-nginx-server)
* [Nginx + Gunicorn + flask 연동](https://velog.io/@yvvyoon/flask-nginx-gunicorn-1)
* [Foward Proxy 와 Reverse Proxy 차이](https://bcp0109.tistory.com/194)
* [nginx 프록시 패스 리다이렉션 무시](https://serverfault.com/questions/363159/nginx-proxy-pass-redirects-ignore-port)
* [Nginx Keepalive 웹서버와 was 간의 통신 튜닝](https://jojoldu.tistory.com/322?category=777282)
* [nginx health check module](https://github.com/yaoweibin/nginx_upstream_check_module)
* [Nginx 로드밸런싱](https://kscory.com/dev/nginx/loadbalancer)
* [Nginx 보안설정](https://couplewith.tistory.com/entry/%EA%BF%80%ED%8C%81%EA%B3%A0%EC%84%B1%EB%8A%A5-Nginx%EB%A5%BC%EC%9C%84%ED%95%9C-%EB%B3%B4%EC%95%887-DoS-DDoS-%EA%B3%B5%EA%B2%A9-%EB%B0%A9%EC%96%B4-%EC%84%A4%EC%A0%95)
* [nginx 로드밸런싱 파마레터 설명](https://kamang-it.tistory.com/entry/WebServernginxnginx%EB%A1%9C-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1-%ED%95%98%EA%B8%B0)
```
Load balancing methods(부하 부산 규칙)

round-robin(디폴트) - 그냥 돌아가면서 분배한다.
hash - 해시한 값으로 분배한다 쓰려면 hash <키> 형태로 쓴다. ex)hash $remote_addr <- 이는 ip_hash와 같다.
ip_hash - 아이피로 해싱해서 분배한다.(한번 접속한 IP는 같은 서버로 분배)
random - 그냥 랜덤으로 분배한다.
least_conn - 연결수가 가장 적은 서버를 선택해서 분배, 근데 가중치를 고려함
least_time - 연결수가 가자 적으면서 평균 응답시간이 가장 적은 쪽을 선택해서분배
```
* [nginx 튜닝](https://couplewith.tistory.com/entry/%EA%BF%80%ED%8C%81-%EA%B3%A0%EC%84%B1%EB%8A%A5-Nginx%EB%A5%BC%EC%9C%84%ED%95%9C-%ED%8A%9C%EB%8B%9D-1-%EB%94%94%EC%8A%A4%ED%81%AC%EC%9D%98-IO-%EB%B3%91%EB%AA%A9-%EC%A4%84%EC%9D%B4%EA%B8%B0)
```
  # nginx.conf 포트 고정(프록시 리다이렉트 무시)할때 설정 $host를 $http_host로 변경
  proxy_set_header Host $host; > proxy_set_header Host $http_host; 
```
* [nginx 자주쓰는 5가지 대표기능 설정](https://wonit.tistory.com/336)


## CI/CD
* [AWS CICD pipeline build](https://medium.com/better-programming/how-to-build-a-ci-cd-pipeline-in-aws-in-5-minutes-and-58-seconds-4de156477042)
* [AWS CICD Automation](https://aws-diary.tistory.com/26)
* [AWS를 이용한 간략 지속적 통합 예제, 무중단 배포 자동화 CI & CD, CodeBuild, CodeDeploy, CodePipeline](https://roka88.dev/97)
* [AWS CI/CD 구축 git, Codebuild, CodeDeploy, CodePipeline](https://mingoogle.tistory.com/22)
* [jenkins & Docker](https://pks2974.medium.com/jenkins-%EC%99%80-docker-%EA%B7%B8%EB%A6%AC%EA%B3%A0-aws-cli-%EC%82%BD%EC%A7%88%EA%B8%B0-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-e728986960e2)
* [Jenkins와 GitHub 연결을 통한 CICD Docker 환경 구성](https://txegg.tistory.com/173)
* [jenkins 호출을 위한 Github Webhook](https://crispyblog.kr/development/common/11)
* [젠킨스(Jenkins) Github Webhooks 연동](https://junhyunny.github.io/information/jenkins/github/jenkins-github-webhook/)
* [jenkins flask 연동](https://velog.io/@inyong_pang/devops-jenkins-flask-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%97%B0%EB%8F%99)
* [jenkins github 연동](https://goddaehee.tistory.com/258)
* [jenkins github 연결설정](https://bcho.tistory.com/1237)
* [CI/CD 툴 비교](https://medium.com/day34/ci-cd-tool-comparison-f710a4777852)
* [github action cicd](https://wookim789.tistory.com/39)
* [버전관리 규칙 Semantic versioning](https://kiwinam.com/posts/33/version-naming/)
* [Argo CD GitOps 설치](https://nayoungs.tistory.com/entry/ArgoCD%EB%9E%80-ArgoCD-%EA%B0%9C%EC%9A%94-%EB%B0%8F-%EC%84%A4%EC%B9%98)

## MSA
* [MicroService for AWS](https://www.slideshare.net/awskorea/3-microservice-aws-architecture-pattern-usecase)
* [MicroService and Serverless](https://waspro.tistory.com/495)
* [MSA란](https://blog.neonkid.xyz/200?category=830544)
* [MSA 선택의 이유(카카오 이모티콘서비스 예)](https://tech.kakao.com/2021/09/14/msa/)
* [숨고 MSA를 위한 내부프레임워크](https://blog.soomgo.com/blog/soomgo-msa-architecture-soomgo-py/)


## cron
* [Cron 사용법](https://www.letmecompile.com/scheduler-cron-tutorial/)
* [Crontab 명령어](https://ojava.tistory.com/154)

## sysstat
* [sysstat사용법](https://brunch.co.kr/@lars/9)
* [ubuntu port확인방법](https://jungfo.tistory.com/93)

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


## cookiecutter
* [cookiecutter ](https://cookiecutter.readthedocs.io/en/latest/installation.html)

## Traefik
> Traefik( 트래픽으로 발음 )은 마이크로서비스를 쉽게 배포할 수 있게 해주는 최신 HTTP 역방향 프록시 및 로드 밸런서
* [traefik Github](https://github.com/traefik/traefik)
* [traefik vs nginx](https://gist.github.com/rabelais88/a458c1f45eea7d28240c64621853bb64)
* [traefik docker 환경설정](https://danawalab.github.io/common/2021/07/14/traefik-reverse-froxy.html)
* [Docker Swarm 을 이용한 Container Orchestration 환경](https://tech.osci.kr/2019/02/13/docker-swarm-%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-container-orchestration-%ED%99%98%EA%B2%BD-%EB%A7%8C%EB%93%A4%EA%B8%B0/)


## 쿠버네티스
* [쿠버네티스 문서](https://kubernetes.io/ko/docs/home/)
* [쿠버네티스 AWS 구축](https://litiblue.com/post/2018-03-14-kubernetesonaws/)
* [쿠버네티스 docker 지원 중단에 따른 대안](https://velog.io/@borab/%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-docker-%EC%A7%80%EC%9B%90-%EC%A4%91%EB%8B%A8%EC%97%90-%EB%94%B0%EB%A5%B8-%EB%8C%80%EC%95%88)
* [쿠버네티스 관련 기술정보](https://github.com/sysnet4admin/_Book_k8sInfra/tree/main/docs/k8s-stnd-arch/2022?fbclid=IwAR0cqaD042vdJj1eMJmN74dxHlvzIWWVh2wryDwsseKyUAWFenpkAtVKg8o)
* [쿠버네티스 패키지 메니저 헬름 공식](https://helm.sh/ko/)


## 메세지 브로커
* [RabbitMQ 란?](https://azderica.github.io/00-rabbitmq/)



## 부하테스트
* [wrk 설치 및 간단 설명](https://www.lesstif.com/software-architect/wrk-modern-http-bench-marking-tool-106856711.html)

## 패킷 분석
* [와이어샤크(WireShark) 사용법](https://jeong-pro.tistory.com/155)



## 웹푸시
* [webpush 라이브러리](https://github.com/web-push-libs/web-push)
* [webpush vapid키 얻는 법](https://stackoverflow.com/questions/62861030/how-to-get-vapid-public-key-and-vapid-private-key-for-django-webpush-implementat)
* [SSE(Server-Sent Events) 푸시(웹푸시와는 다름)를 별도 추가 기술 없이 동작하는 방법](https://hamait.tistory.com/792)
* [web socket과 sse의 차이점](https://surviveasdev.tistory.com/entry/%EC%9B%B9%EC%86%8C%EC%BC%93-%EA%B3%BC-SSEServer-Sent-Event-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0)
```python
from fastapi import FastAPI, Response
from starlette.responses import StreamingResponse
from time import sleep

app = FastAPI()

@app.get("/events")
async def events():
    async def event_generator():
        # 이벤트 메시지 생성
        # "data:" 이 부분이 필수 값
        # 개행은 \n 마지막행은 \n\n 두번 포함
        yield "data: Event 1\n\n"
        sleep(1)
        yield "data: Event 2\n\n"
        sleep(1)
        yield "data: Event 3\n\n"
    
    return StreamingResponse(event_generator(), media_type="text/event-stream")
```
```javascript
if (!!window.EventSource) {
  var source = new EventSource('events');
} else {
  // Result to xhr polling :(
}
source.addEventListener('message', function(e) {
  console.log(e.data);
}, false);

source.addEventListener('open', function(e) {
  // Connection was opened.
}, false);

source.addEventListener('error', function(e) {
  if (e.readyState == EventSource.CLOSED) {
    // Connection was closed.
  }
}, false);
```

