# Python

* [Python 공식문서](https://docs.python.org/ko/3/)
* [python 문법](https://wikidocs.net/145)
* [python 버전별 새로운 기능](https://docs.python.org/3.11/whatsnew/index.html)
* [ *, ** 의 의미](https://sshkim.tistory.com/182)
* [ _, 언더스코어의 의미](https://doorbw.tistory.com/153)
* [클래스 json 변환](http://jsonpickle.github.io/)
* [split](https://mainia.tistory.com/5624)
* [문자열로 된 숫자 확인하는 방법](https://soooprmx.com/archives/10159)
* [filter](https://wikidocs.net/22803)
* [enumerate 반복문 적용시 인덱스와 객체 둘다 필요할때](https://wikidocs.net/16045)
* [lambda 함수(js에 화살표 함수랑 비슷)](https://wikidocs.net/64)
* [with 문 사용법](https://velog.io/@zkffhtm6523/Python-With%EB%AC%B8-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
* [\_\_init\_\_.py 사용 이유](https://mmjourney.tistory.com/14)
* [is None 과 == None의 차이](https://blog.metafor.kr/162)
* [dataclass 사용법](https://sunow.tistory.com/entry/Python-dataclass-%EB%AA%A8%EB%93%88-%EC%82%AC%EC%9A%A9%EB%B2%95)
* [12가지 python 런타임](https://www.itworld.co.kr/news/132322)
* [좌표간 거리 계산](https://stricky.tistory.com/283)
* [python 3.11 속도차이](https://docs.python.org/3.11/whatsnew/3.11.html)
* [python 3.11 정식릴리즈](https://www.python.org/downloads/release/python-3110/)
* [경우의 수](https://armontad-1202.tistory.com/entry/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%AA%A8%EB%93%A0-%EA%B2%BD%EC%9A%B0%EC%9D%98-%EC%88%98-%EC%B6%94%EC%B6%9C-%EA%B0%80%EB%8A%A5%ED%95%9C-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC)
#### python 설치 및 연결
```zsh
  # python 명령어로 python3 실행하기
  ~/.bashrc 또는 ~/.bash_aliases 파일에 아래의 내용을 추가

  alias python=python3
  alias pip=pip3
  그리고 이를 적용하기 위해 source ~/.bashrc 또는 source ~/.bash_aliases를 실행

  $ python --version
  Python 3.6.9
```
*** 
> AES 암복호화
* [AES-GCM 암복호화](https://blog.naver.com/chandong83/221886840586)
* [AES CBC 암복호화](https://mkjjo.github.io/python/2019/08/04/crypto.html)
* [AES CBC 암복호화2](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=chandong83&logNo=221021909030)
* [AES Pycrytptodemo 암복호화](https://deok2kim.tistory.com/302)
***
> jwt 토큰
* [jwt 토큰 사용법](https://juneyr.dev/2018-01-28/making-token-pyjwt)
* [refresh token, access token](https://tansfil.tistory.com/59)
***
> 정적메소드
* [정적메소드 2가지 차이 staticMethod classMethod 차이](https://sshkim.tistory.com/184)
* [정적메소드 사용법 및 2가지 종류 차이](https://wikidocs.net/16074)
***
* [효율적인 메모리 관리 예제](https://deepwelloper.tistory.com/130)


* [m1 macOS11 python 버전관리](https://laict.medium.com/install-python-on-macos-11-m1-apple-silicon-using-pyenv-12e0729427a9)
* [설정값 관리 방법](https://mingrammer.com/ways-to-manage-the-configuration-in-python/)



* [defaultdict](https://dongdongfather.tistory.com/69)
> defaultdict(<자료형>) 형식으로 dict 키의 값이 없을 때 default 값을 지정 가능



* [3.6이후 지원 변수주석](https://conansjh20.tistory.com/55)
```python
   # 변수명: 주석 = 대입 값 형태로 사용
   test_no:int = 123
   def test_func(param:int=0):
   	print(param)

   # 단순한 주석 역할 이기때문에 오류를 발생시키지는 않음
   test_func('aaa')
```
* [bcrypt로 암호화](https://24hours-beginner.tistory.com/120)
* [.env 사용](https://blog.gilbok.com/how-to-use-dot-env-in-python/)
```python
   ## dotenv 모듈설치
   pip install python-dotenv
   
   ## 사용
   from dotenv import load_dotenv
   import os 

   # load_dotenv 실행해서 env 읽기 가능 하도록 설정, 사용 가능한 파라메터
   ## dotenv_path: .env 파일의 절대경로 및 상대경로
   ## stream: .env 파일 내용에 대한 StringIO 객체
   ## verbose: .env 파일 누락 등의 경고 메시지를 출력할 것인지에 대한 옵션
   ## override: 시스템 환경변수를 .env 파일에 정의한 환경변수가 덮어쓸지에 대한 옵션
   load_dotenv()
   
   

   data = os.getenv('<env key>')

```
### webFramework
* [framework 비교](https://dingrr.com/blog/post/python-%EC%9B%B9%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC-%EB%81%9D%ED%8C%90%EC%99%95-%EA%B0%80%EB%A6%AC%EA%B8%B0-django-flask-fastapi-sanic)
* [fastAPI 장단점](https://velog.io/@maintain0404/Django%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%9D%98-FastAPI-%EC%82%AC%EC%9A%A9-%ED%9B%84%EA%B8%B0)
* [Context Manager 사용법](https://sjquant.tistory.com/12)
* [Context Manager 설명 및 간단 생성](https://velog.io/@fregataa/Python3-Context-manager)
* [비동기 분산처리 Celer](https://velog.io/@swhan9404/Celery%EB%9E%80)
> 서버간 세션을 유지하기 위해서는 리스폰스에서 쿠키 값을 꺼내서 그 쿠키 값을 헤더에 넣어서 보내주면 유지가능(브라우저에서는 자동으로 이루어지는 부분)
> formData 를 만들때는 바디는 string 형식으로 a=1&b=2&c=3 식으로 데이터를 보내고 헤더에 폼형식을 넣어서 보냄.
```
 # 3항 연산자 자바나 자바스크립트와는 다름
 <참 결과> if <조건> else <거짓결과>
 'True' if a == 1 else 'False'
```

##### base64 인코딩(encoding), 디코딩(decoding)
```python
import base64

str = '문자열'
# encode
str_base64 = base64.b64encode(str.encode('utf-8'))
# b' ' 지우기
str_base64.decode('utf-8')

# decode
str = base64.b64decode(str_base64).decode('utf-8')

```

##### yield
> 함수 안에서 yield를 사용하면 함수는 제너레이터가 되며 yield에는 값(변수)을 지정
* [yield 이해하기](https://tech.ssut.me/what-does-the-yield-keyword-do-in-python/)
* [제너레이터와 yield](https://dojang.io/mod/page/view.php?id=2412)

##### 웹소켓 socketio
* [Using Websockets with Python](https://medium.com/koko-networks/using-websockets-with-python-4396e54d36e6)
```
 # Using Websockets with Python 링크에서 참조 
 # WebSocket은 n 개의 클라이언트에 연결할 수 있으므로 플라스크는 Eventlet 또는 Gevent와 같은 일부 비동기 라이브러리가 필요
 # Eventlet 스레드 라이브러리로 프로젝트를 실행하려면 Gunicorn 웹 서버를 설치하거나 UWsgi 서버를 사용
 # socket_io.run() 을 사용하려면 Gunicorn 또는 UWsgi 서버를 사용해야함.
 
 # 소켓사용 nginx 설정 시 
 # location 항목에 아래 옵션 추가
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection "upgrade";
```
* [flask-socketio 모듈 공식문서 Deployment 항목에 gunicorn 서버 연결 부분 참조](https://flask-socketio.readthedocs.io/en/latest/deployment.html)
* [socketio channel, room 의 개념 설명](https://itseminar.tistory.com/31)
```python
 # channel은 어떤 이름을 가진 room들이 모여있는 개념이고
 # room은 참여자들이 모여있는 하나의 공간 개념
```
* [python-socketio 도큐먼트](https://python-socketio.readthedocs.io/en/latest/server.html)
---
## 속도 개선 방법 
* [속도 개선 코딩 방법](https://camel-it.tistory.com/140)
* [다양한 속도 개선 방법 예제](https://jinwoo1990.github.io/dev-wiki/python-concept-4/)
##### JIT(Just In Time)컴파일 런타임
* [pypy](https://www.pypy.org/)
* [python pypy 차이](https://ralp0217.tistory.com/entry/Python3-%EC%99%80-PyPy3-%EC%B0%A8%EC%9D%B4)
```
 numpy, pandas 모듈 사용시 특정 버전이 필요한게 아니라면 
 requirements.txt 에 버전 없이 표기해서 설치p
```
* [Numba](http://numba.pydata.org/)
* [Numba 설명](https://gurujung.github.io/_posts/2019-02-17-numba_user_5minguide/)
* [Numba 기본 사용법](https://gurujung.github.io/_posts/2019-04-10-numba_user_jit/)
```
 numba 사용 시 특정 상황에서 오류 발생
 겪은 상황
 1. 빈 배열을 주고 받을 때
```
##### 확장모듈 생성
* [cython](https://cython.org/)
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
* [asyncio 사용하기](https://dojang.io/mod/page/view.php?id=2469)
* [비동기 request처리](https://item4.blog/2017-11-26/Asynchronous-HTTP-Request-with-aiohttp/)
* [async/await 기초 코루틴과 테스크](https://kdw9502.tistory.com/6)
* [flask 에서 백그라운드처리](https://blog.kshgroup.kr/background-jobs-with-flask/)
* [비동기 동작이 실행중 비동기 요청이 들어올 경우 오류 발생 대처방법](https://stackoverflow.com/questions/55409641/asyncio-run-cannot-be-called-from-a-running-event-loop)
* [FastAPI / uvicorn 호스팅 환경에서 asyncio 사용하는 방법](https://www.sysnet.pe.kr/2/0/13087?pageno=0)
```python
  ## 시간 딜레이 추가
  await asyncio.sleep(<초>) 
```
* [unsync](https://github.com/alex-sherman/unsync)
```python
from unsync import unsync
  
@unsync
async def unsync_async():
	    await asyncio.sleep(1)
	    return 'I like decorators'

unfuture1 = unsync_async()
unfuture2 = unsync_async()
print(unfuture1.result() + unfuture2.result())
```
###### . 연산 사용을 줄임
```python
# 모듈을 import 해서 내부 함수를 사용하는 것보다
from mudule
module.function()
# 직접 내부 함수를 import해서 사용하면 __getattribute()__하거나 __getattr()__ 등 사전연산을 줄일 수 있음.
from module import function
```

###### List Comprehension 사용
```python
result = []
# for 문을 사용하는 것보다
for element in some_list:
	if some_filter(element):
		result.append(element) 

# List Comprehension 으로 변환하면 속도가 개선됨
result = [x for x in large_list if some_filter(x)]
```
* [List comprehension 2중 for문](https://velog.io/@yejin20/TILList-comprehension-%EC%A4%91%EC%B2%A9)
###### 외부 라이러리를 변수에 담아 사용
```python
import random #wrong
While something
>> print(random.randint(0,10))

import random #right
rand = random.randint
While something:
>>print(rand(0,10))
```
######  cProfile 속도 측정 모듈
* [공식문서 한글 번역](https://docs.python.org/ko/3/library/profile.html)
---

##### 상속
> 설치한 특정 모듈의 메소드를 수정해서 사용하고 싶을때 사용가능하다.
* [상속 & 메소드 오버라이딩](https://ordo.tistory.com/30)
#### 문자열
##### 문자열치환
```python 
replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수]) 
```
* [정규표현식 활용](https://greeksharifa.github.io/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D(re)/2018/08/04/regex-usage-05-intermediate/)
* [re 모듈 활용](https://velog.io/@ednadev/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC-re%EB%AA%A8%EB%93%88)

##### 앞뒤 공백제거
```python 
strip() 
```
##### 문자열 검색
````python
 'abc'.index('a) # >>> 0 #인덱스를 반환 없을 예
 'abc'.find('a) # >>> 0 #인덱스를 반환 없을 경우 -1
````

##### 반복문 인덱스 구하기
```python
for i in range(len(array)): 
```

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
  
  # list -> set 으로 형변환할 때 내부 자원이 class일경우 오류발생할 수 있음 
  
  # 두 배열의 차집합 구하는 방법(배열안에 dict 또는 클래스일 경우 안됨)
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
  ## strptime 실행시 포멧 형식이 안맞으면 오류발생
```
* [timezone 변경방법](https://codechacha.com/ko/python-apply-timezone-to-datetime/)

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
* [apscheduler missed job : 에러](https://jjeongil.tistory.com/944)
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

#### 파일다루기

####### 링크만들기(동일한 파일을 여러 이름으로 사용할때 등)
> 하드링크와 소프트 링크 차이
> * 하드링크
> 	* 원본을 복사해서 사본을 만들고 원본과 연결시켜서 변경 사항이 동시에 반영, 원본 삭제시에도 유지
> * 소프트링크
> 	* 원본을 바로가기 개념으로 참조만 하고 원본이 삭제될경우 사용할 수 없음.
```python
import os


# 하드 link 파일 혹은 폴더를 만들 때 사용
os. link(<참조할 경로>, <링크 생성 경로>)

# 소프트 link 파일 혹은 폴더를 만들 때 사용
os.symlink(<참조할 경로>, <링크 생성 경로>)


# 소프트 link 파일 혹은 폴더와 연결된 실제 경로 조회
os.readlink(<링크 생성 경로>)

# 연결된 파일 혹은 폴더를 끊을 때 사용
os.unlink(<링크 생성 경로>)

# 하드 혹은 소프트 link 파일 혹은 폴더인지 확인할 때 사용
os.path.islink(<링크 생성 경로>)

# 링크가 있는지 확인해서 있으면 삭제 후 생성
if os.path.islink('/abc/link.file'):
  os.symlink('/abc/orifile.file')
os.symlink('/abc/orifile.file', '/abc/link.file')

# 파일이나 경로가 존재하는지 확인 True or False
# 심볼릭 링크가 깨진 경우, 접근 권한이 없어도 False
os.path.exists(path)

# path가 파일인 경우 True를 리턴하고 디렉토리이거나 파일이 존재하지 않으면 False
os.path.isfile(path)

# path가 디렉토리인 경우 True를 리턴하고 파일이거나 디렉토리가 존재하지 않으면 Fals
os.path.isdir(path)

```


##### 다른 언어 파일 다루기
* [java 다루기 jPype](https://jpype.readthedocs.io/en/latest/quickguide.html)


##### command 라인 다루기
* [shell 명령어](https://codechacha.com/ko/python-run-shell-script/)
* [subprocess](https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=sagala_soske&logNo=221280201722&parentCategoryNo=&categoryNo=118&viewDate=&isShowPopularPosts=true&from=search)

```python
import os

# 콘솔에 프린트
os.system('echo "hello"')

# 데이터로 리턴
stream = os.popen('echo "hello"')
output = stream.read()
print(output)

```

##### 보안
* [XSS(Cross-Site Scripting) 개념 및 방어 방법](https://roadofdevelopment.tistory.com/38)


##### pydantic 데이터 유효성검사
* [pydantic 공식홈페이지](https://pydantic-docs.helpmanual.io/)
* [orm 개체에 매핑하기 위해 모델에 하는 설정](https://pydantic-docs.helpmanual.io/usage/models/)
* [pycharm pydantic 플러그인](https://plugins.jetbrains.com/plugin/12861-pydantic)


### 데이터 처리
##### Pandas
* [판다스(Pandas) and 넘파이(Numpy) and 맷플롭립(Matplotlib)](https://wikidocs.net/32829)


##### 크롤링
* [Selenium을 활용한 크롤러](https://beomi.github.io/2017/02/27/HowToMakeWebCrawler-With-Selenium/)
* [Selenium 지연방법](https://codechacha.com/ko/selenium-explicit-implicit-wait/)
* [기본적인 크롤링](https://wikidocs.net/6660)

##### pyscript, python으로 웹프론트개발
* [pyscript란](https://velog.io/@taekkim/PyScript-%EB%9E%80)


#### web push
* [pywebpush](https://github.com/web-push-libs/pywebpush)
* [web push 샘플 코드](https://github.com/raturitechmedia/python_flask_webpush_notification)


##### GUI(윈도우 프로그램 그래픽 인터페이스)
* [GUI라이브러리](https://showering.tistory.com/150)
* [PyQt5 Tutorial](https://wikidocs.net/book/2165)
> py 파일을 exe 파일로 생성
```bash
> pip install pyinstaller
# 하나의 파일로 생성
> pyinstaller -w -F 파일명.py
```

* [외부 프로그램 호출](https://www.delftstack.com/ko/howto/python/call-external-programs-python/)
