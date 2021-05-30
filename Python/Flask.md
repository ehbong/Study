# Flask

* [플라스크 튜토리얼](https://flask-docs-kr.readthedocs.io/ko/latest/)
* [잔재미코딩 flask 사용법](https://www.fun-coding.org/flask_basic-2.html)
* [Jinja2 템플릿 사용법](http://hleecaster.com/flask-jinja2/)

## mysql for flask
* [mac mysql 설치](https://stackoverflow.com/questions/15314791/django-error-vertualenv-environmenterror-mysql-config-not-found)
* [venv 에서 mysql 경로 못찾을때](https://stackoverflow.com/questions/15314791/django-error-vertualenv-environmenterror-mysql-config-not-found)

## order
* [request 받기](https://stackoverrun.com/ko/q/11370200)
* [requests 모듈 외부 주소 호출](https://m.blog.naver.com/wideeyed/221586482884)

## session
* [session 사용](https://riptutorial.com/ko/flask/example/9236/%EB%B3%B4%EA%B8%B0-%EB%82%B4%EC%97%90%EC%84%9C-%EC%84%B8%EC%85%98-%EA%B0%9D%EC%B2%B4-%EC%82%AC%EC%9A%A9)


## socket-io
* [SocketIO 공식문서](https://flask-socketio.readthedocs.io/en/latest/getting_started.html)
```

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
```
  # 로그남기기
  socketio = SocketIO(logger=True, engineio_logger=True)
```
