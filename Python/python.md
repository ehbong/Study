# Python

* [Python 공식문서](https://docs.python.org/ko/3/)
* [python 문법](https://wikidocs.net/145)
* [ *, ** 의 의미](https://sshkim.tistory.com/182)
* [ _, 언더스코어의 의미](https://doorbw.tistory.com/153)
* [클래스 json 변환](http://jsonpickle.github.io/)
* [split](https://mainia.tistory.com/5624)
* [문자열로 된 숫자 확인하는 방법](https://soooprmx.com/archives/10159)
* [filter](https://wikidocs.net/22803)
* [AES-GCM 암복호화](https://blog.naver.com/chandong83/221886840586)
* [AES CBC 암복호화](https://mkjjo.github.io/python/2019/08/04/crypto.html)
* [AES CBC 암복호화2](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=chandong83&logNo=221021909030)
* [jwt 토큰 사용법](https://juneyr.dev/2018-01-28/making-token-pyjwt)
* [enumerate 반복문 적용시 인덱스와 객체 둘다 필요할때](https://wikidocs.net/16045)
* [lambda 함수(js에 화살표 함수랑 비슷)](https://wikidocs.net/64)
* [효율적인 메모리 관리 예제](https://deepwelloper.tistory.com/130)
* [staticMethod class 차이](https://sshkim.tistory.com/184)
* 서버간 세션을 유지하기 위해서는 리스폰스에서 쿠키 값을 꺼내서 그 쿠키 값을 헤더에 넣어서 보내주면 유지가능(브라우저에서는 자동으로 이루어지는 부분)
* formData 를 만들때는 바디는 string 형식으로 a=1&b=2&c=3 식으로 데이터를 보내고 헤더에 폼형식을 넣어서 보냄.
```
 # 3항 연산자 자바나 자바스크립트와는 다름
 <참 결과> if <조건> else <거짓결과>
```
##### socketio
* [Using Websockets with Python](https://medium.com/koko-networks/using-websockets-with-python-4396e54d36e6)
```
 # Using Websockets with Python 링크에서 참조 
 # WebSocket은 n 개의 클라이언트에 연결할 수 있으므로 플라스크는 Eventlet 또는 Gevent와 같은 일부 비동기 라이브러리를 사용해야합니다. 따라서 우리의 경우 Eventlet을 설치하고 있습니다.
 # Eventlet 스레드 라이브러리로 프로젝트를 실행하려면 Gunicorn 웹 서버를 설치하거나 UWsgi 서버를 사용하겠습니다.
 # socket_io.run() 을 사용하려면 Gunicorn 또는 UWsgi 서버를 사용해야함.
 
 # 소켓사용 nginx 설정 시 
 # location 항목에 아래 옵션 추가
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection "upgrade";
```
* [flask-socketio 모듈 공식문서 Deployment 항목에 gunicorn 서버 연결 부분 참조](https://flask-socketio.readthedocs.io/en/latest/deployment.html)







##### 상속
* 설치한 특정 모듈의 메소드를 수정해서 사용하고 싶을때 사용가능하다.
* [상속 & 메소드 오버라이딩](https://ordo.tistory.com/30)
#### 문자열
##### 문자열치환
```python 
replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수]) 
```
* [정규표현식 활용](https://greeksharifa.github.io/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D(re)/2018/08/04/regex-usage-05-intermediate/)
* [re 모듈 활용](https://velog.io/@ednadev/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC-re%EB%AA%A8%EB%93%88)

##### 앞뒤 공백제거
``` strip() ```
##### 문자열 검색
````python
 'abc'.index('a) # >>> 0 #인덱스를 반환 없을 예
 'abc'.find('a) # >>> 0 #인덱스를 반환 없을 경우 -1
````

##### 반복문 인덱스 구하기
``` for i in range(len(array)): ```

##### 배열
* [배열 검색 filter and list comprehension](https://m.blog.naver.com/wideeyed/221839555992)
```python
  # 필터 형식 검색
  result = list(filter(lambda x: x.value == 1 , arrayData))
  
  # list comprehension 형식 검색
  result = [x for x in arrayData if x.value == 1]
```
```python
  # 인덱스 없을 경우 오류발생(인덱스 번호로 반환)
  temp.index(<검색할 값>)
  # in 으로 배열내 값이 있는지 확인(오류발생은 없으나 반환값을 True, False로 반환)
  <검색할 값> in temp
  
  # 두 배열의 차집합 구하는 방법
  temp3 = list(set(temp1) - set(temp2)) #순서 보존이 안됨

  #또는
  s = set(temp2)
  temp3 = [x for x in temp1 if x not in s] #순서 보존됨
```
##### 시간 다루기
* [날짜 포메팅](https://krksap.tistory.com/1635)
```python
  # 타임 스탬프를 데이트 타입으로 변경
  datetime.datetime.fromtimestamp(<타입스탬프> / 1000, <타임존 예 datetime.timezone.utc>)
  # 데이트 타입을 문자열로(데이트 > 바꿀 데이트 형태 문자열)
  datetype_data.strftime(<포멧형식 예) %Y-%m-%d %H:%M:%S >)
  # 시간형태 문자열을 포멧변경(데이트 형태 문자열+ 데이트형식 > 데이트)
  datetime.strptime(<시간형태 문자열>, '%Y-%m-%d %H:%M:%S.%f')
```

##### 딕셔너리리스트 검색
```python
  list = [{'Name': 'Tom', 'Age': 30},{'Name': 'Jack', 'Age': 31},{'Name': 'Sue', 'Age': 32}]
  tom = (item for item in list if item['Name'] == 'Tom')\
  dict = next(tom, False)
  # >>> dict {'Name': 'Tom', 'Age': 30} 
  # >>> dict['Age']
  
  ret = next(item for item in list if item['Name'] == 'Tom'), None)
  print(ret)
  ## 키가 없을때 item['Name'] 은 오류발생 item.get('Name') 을 사용
```
* [pandas 예제](https://dandyrilla.github.io/2017-08-12/pandas-10min/)

##### 변수 스코프
```python
  def a: 
    a = 0
    if a == 0:
      b = 0
    print(a)
    print(b)
  # 둘다 동작
  # 자바스크립트의 var와 비슷하게 def 함수 안에서 전역으로 동작한다.
```
##### 특정 시간마다 실행(스케줄러)
* [특정시간마다 실행](https://tre2man.tistory.com/188)
* [apscheduler 기본 사용법](https://hello-bryan.tistory.com/216)

##### 예외
* [에러와 예외](https://docs.python.org/ko/3/tutorial/errors.html)
##### 예외 전이
```python
  # 따로 throw 없이 예외가 전이돼서 예외처리됨
  def a():
    try:
      return b():
    except Exception as e:
      print('예외발생 :'+str(e)):
    
  def b():
    #오류 발생

```

##### 데코레이터
* [파이썬 코딩 도장 데코레이터](https://dojang.io/mod/page/view.php?id=2427)
* [데코레이터 기본 사용법](https://www.daleseo.com/python-decorators/)
```python
  # 매개변수가 있는 데코레이터 출처 https://dojang.io/mod/page/view.php?id=2429
  def is_multiple(x):              # 데코레이터가 사용할 매개변수를 지정
    def real_decorator(func):    # 호출할 함수를 매개변수로 받음
        def wrapper(a, b):       # 호출할 함수의 매개변수와 똑같이 지정
            r = func(a, b)       # func를 호출하고 반환값을 변수에 저장
            if r % x == 0:       # func의 반환값이 x의 배수인지 확인
                print('{0}의 반환값은 {1}의 배수입니다.'.format(func.__name__, x))
            else:
                print('{0}의 반환값은 {1}의 배수가 아닙니다.'.format(func.__name__, x))
            return r             # func의 반환값을 반환
        return wrapper           # wrapper 함수 반환
    return real_decorator        # real_decorator 함수 반환

  @is_multiple(3)     # @데코레이터(인수)
  def add(a, b):
      return a + b

  print(add(10, 20))
  print(add(2, 5))
```

##### 멀티쓰레드 & 멀티 프로세스
* [멀티쓰레드 & 멀티 프로세스](https://monkey3199.github.io/develop/python/2018/12/04/python-pararrel.html)
* [멀티프로세싱 예제](https://doorbw.tistory.com/205)
* [병렬처리할때 공용으로 사용할 변수를 정의할때 multiprocessing.Manager()](https://docs.python.org/ko/3/library/multiprocessing.html)
```python
 # 멀티 프로세스(함수에 매개변수 넣는 형태의 목록을 프로세스를 여러개 생성에서 병렬로처리) 
 # sqlAlcemy를 사용해서 db.session.commit() 을 바깥에서 할 경우 실제로는 커밋되지 않음(세션을 공유하지않음)
 pool = multiprocessing.Pool(processes=4)
 pool.map(<함수명>, <매개변수 리스트>)
 pool.close()
 pool.join()
```

##### 비동기 처리
* [비동기 처리 asyncio](https://www.daleseo.com/python-asyncio/)
* [비동기 request처리](https://item4.blog/2017-11-26/Asynchronous-HTTP-Request-with-aiohttp/)
* [async/await 기초 코루틴과 테스크](https://kdw9502.tistory.com/6)
```
  ## 시간 딜레이 추가
  await asyncio.sleep(<초>) 
```
##### logger
* [logging 기본설명](https://docs.python.org/ko/3/howto/logging.html)
* [날짜별 로깅파일 생성](https://yurimkoo.github.io/python/2019/08/11/logging.html)
* [flask 에 적용 방법](https://ourcstory.tistory.com/230)
* [formatter 설정](https://docs.python.org/ko/3/library/logging.html#logging.Formatter)
* [formatter 예제](https://stackoverflow.com/questions/533048/how-to-log-source-file-name-and-line-number-in-python/44401529)

##### QR code
* [qrcode 모듈 공식 문서](https://pypi.org/project/qrcode/)
* [qrcode > pdf 생성 reportlab-qrcode 모듈 공식문서](https://pypi.org/project/reportlab-qrcode/)
* [pdf as response + sampleSytleSheet font](https://stackoverflow.com/questions/63992269/reportlab-pdf-python-3-problems-with-fonts)

##### eval(), exec()
```
  eval 함수는 
  수식을 받아서 컴파일 코드로 변환(문자열 형태만 받음)
  exec 함수는 
  소스코드를 받아서 컴파일 코드로 변환
```
