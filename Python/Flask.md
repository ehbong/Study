# Flask

* [플라스크 튜토리얼](https://flask-docs-kr.readthedocs.io/ko/latest/)
* [잔재미코딩 flask 사용법](https://www.fun-coding.org/flask_basic-2.html)
* [Jinja2 템플릿 사용법](http://hleecaster.com/flask-jinja2/)
```python
  # 기본 포트 5000, 아래처럼 실행하면 로컬에서만 접속 가능
  app.run()
  # 기본 호스트를 지정, 포트는 바꿀경우 아래와 같이 추가
  app.run(host='0.0.0.0', port='5000')
```
* [flask 에서 백그라운드처리](https://blog.kshgroup.kr/background-jobs-with-flask/)
## mysql for flask
* [mac mysql 설치](https://stackoverflow.com/questions/15314791/django-error-vertualenv-environmenterror-mysql-config-not-found)
* [venv 에서 mysql 경로 못찾을때](https://stackoverflow.com/questions/15314791/django-error-vertualenv-environmenterror-mysql-config-not-found)

#### zappa
> 파이썬 서버리스 환경(AWS Lambda + API Gateway) 설정 및 배포 라이브러리
* [](https://github.com/zappa/Zappa)
* [zappa 로 serverless 구현](https://tech.junhabaek.net/zappa%EC%99%80-github-action%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%84%9C%EB%B2%84%EB%A6%AC%EC%8A%A4-django-application-aws-%EB%B0%B0%ED%8F%AC-%ED%8A%B8%EB%9F%AC%EB%B8%94-%EC%8A%88%ED%8C%85-15604ed6bbcc)


## 
* [request 받기](https://stackoverrun.com/ko/q/11370200)
* [requests 모듈 외부 주소 호출](https://m.blog.naver.com/wideeyed/221586482884)
* [요청에 대한 이벤트 핸들러](https://blusky10.tistory.com/243)
```python
  @app.before_first_request
  def before_first_request():
  print("앱이 기동되고 나서 첫 번째 HTTP 요청에만 응답")

  @app.before_request
  def before_request():
  print("매 HTTP 요청이 처리되기 전에 실행")

  @app.after_request
  def after_request(response):
  print("매 HTTP 요청이 처리되고 나서 실행")
  return response

  @app.teardown_request
  def teardown_request(exception):
  print("매 HTTP요청의 결과가 브라우저에 응답하고 나서 호출")

  @app.teardown_appcontext
  def teardown_appcontext(exception):
  print("HTTP요청의 어플리케이션 컨텍스트가 종료될때 실행")
  # db.session.close(), db.session.remove() 등 연결 관련 설정을 종료시킬때도 활용
```

## session
* [session 사용](https://riptutorial.com/ko/flask/example/9236/%EB%B3%B4%EA%B8%B0-%EB%82%B4%EC%97%90%EC%84%9C-%EC%84%B8%EC%85%98-%EA%B0%9D%EC%B2%B4-%EC%82%AC%EC%9A%A9)

## file
* [file upload](https://velog.io/@kho5420/Flask-%ED%8C%8C%EC%9D%BC-%EC%97%85%EB%A1%9C%EB%93%9C-File-Upload%ED%95%98%EA%B8%B0)
```python
  # 파일 삭제
  import os
  file = './upload/test.txt'

  if os.path.isfile(file):
    os.remove(file)
  # 폴더 삭제
  os.rmdir('/abc/')
```


## socket-io
* [SocketIO 공식문서](https://flask-socketio.readthedocs.io/en/latest/getting_started.html)
```python

  -- javascript
  let socket = io.connect(
    "http://" + document.domain + ":" + location.port + "/test"
  );
  
  -- flask
  # namespace 는 connect 시 주소에 붙는 namespace 
  # 호출로 모두에게 보내기
  @socketio.on('my event')
  def handle_my_custom_event(data):
    emit('response', data, broadcast=True, namespace='/test')
  # 서버에서 모두에게 보내기 emit가 아니라 socketio.emit
  def some_function():
    socketio.emit('some event', {'data': 'test'}, namespace='/test')
```
```python
  # 로그남기기
  socketio = SocketIO(logger=True, engineio_logger=True)
```
