# Server

* [SSL 인증서 생성,사설 인증서 생성](https://namjackson.tistory.com/24)
* [구글 검색 안되게 하기](https://ragonfly.tistory.com/entry/%EA%B5%AC%EA%B8%80%EC%97%90%EC%84%9C-%EA%B2%80%EC%83%89-%EC%95%88%EB%90%98%EA%B2%8C-%ED%95%98%EB%8A%94%EB%B2%95)
* DNS의 설정을 변경하려면, 도메인 업체가 아닌 네임서버에서 쪽에서 변경해야 변경. 
  * ex) AWS EC2 인스턴스에 Route 53으로 연결하고 도메인을 가비아에서 사서 연결할 경우 Route53에서 설정을 변경해야 반영.
  
* [ubuntu 프로세스 관리 supervisor 설치와 사용법](https://devlog.jwgo.kr/2016/11/07/how-to-use-supervisor-in-one-minute/)
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
* [flask and nginx](http://egloos.zum.com/mcchae/v/11149241)
* [에러 추적(Error Tracking) 및 로그 취합(logging aggregation) 시스템인 Sentry](https://www.lesstif.com/system-admin/error-tracking-logging-aggregation-sentry-30705079.html)
* [ubuntu 패키지 관리하기, 여러개 패키지 중 대표 버전설정](https://www.whatwant.com/entry/update-alternatives-%EC%97%AC%EB%9F%AC-%EB%B2%84%EC%A0%84%EC%9D%98-%ED%8C%A8%ED%82%A4%EC%A7%80-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)

* [Nginx](https://opentutorials.org/module/384/3462)
* [Nginx, Gunicorn(+ WSGI) 개념 이해 및 활용](https://www.opentutorials.org/module/4936/28881)
