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
* [jwt 토큰 사용법](https://juneyr.dev/2018-01-28/making-token-pyjwt)
##### 상속
* [상속 & 메소드 오버라이딩](https://ordo.tistory.com/30)

##### 문자열치환
``` replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수]) ```
* [정규표현식 활용](https://greeksharifa.github.io/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D(re)/2018/08/04/regex-usage-05-intermediate/)
* [re 모듈 활용](https://velog.io/@ednadev/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC-re%EB%AA%A8%EB%93%88)
##### 앞뒤 공백제거
``` strip() ```
##### 반복문 인덱스 구하기
``` for i in range(len(array)): ```

##### 딕셔너리리스트 검색
``` 
  list = [{'Name': 'Tom', 'Age': 30},{'Name': 'Jack', 'Age': 31},{'Name': 'Sue', 'Age': 32}]
  tom = (item for item in list if item['Name'] == 'Tom')\
  dict = next(tom, False)
  >>> dict {'Name': 'Tom', 'Age': 30} 
  >>> dict['Age']
  
  ret = next(item for item in list if item['Name'] == 'Tom'), None)
  print(ret)
  ## 키가 없을때 item['Name'] 은 오류발생 item.get('Name') 을 사용
```
* [pandas 예제](https://dandyrilla.github.io/2017-08-12/pandas-10min/)

##### 변수 스코프
```
  def a: 
    a = 0
    if a == 0:
      b = 0
    print(a)
    print(b)
  # 둘다 동작
  # 자바스크립트의 var와 비슷하게 def 함수 안에서 전역으로 동작한다.
```
##### 특정 시간마다 실행
*[특정시간마다 실행](https://tre2man.tistory.com/188)

##### 예외 전이
```
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
```
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
