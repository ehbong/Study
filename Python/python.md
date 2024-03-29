# Python

### Python 공식 문서 및 문법
* [Python 공식문서](https://docs.python.org/ko/3/)
* [python 문법](https://wikidocs.net/145)
* [pep8 python 코딩 스타일 가이드](https://ultrakain.gitbooks.io/python/content/chapter1/coding-style-pep8.html)
* [ *, ** 의 의미](https://sshkim.tistory.com/182)
* [바다코끼리 연산자 := 에 대한 설명](https://bio-info.tistory.com/120)
* [비트 쉬프트 연산 <<, >> ](https://heestory217.tistory.com/81)
* [python 의 함수 인자 전달방식 call by assignment](https://velog.io/@yun9yu/%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%80-Call-by-reference-Call-by-value)
* [is None 과 == None의 차이](https://blog.metafor.kr/162)
```python
  # is 는 id() 값을 비교(할당된 메모리 주소를 비교), == 는 값 자체를 비교
```
* [dataclass 사용법](https://sunow.tistory.com/entry/Python-dataclass-%EB%AA%A8%EB%93%88-%EC%82%AC%EC%9A%A9%EB%B2%95)
* [가정 설정문 assert](https://wikidocs.net/21050)
* [기본 매개변수 초기화 특징](http://suhanlee.github.io/2016/python-parameter.html)
```python
# 변수 초기화를 할때 아래와 같이 작성하면 변수가 선언될 때 배열이 초기화 되어서, 실행할 때 마다 배열안에 값이 변한다.
def test(arg, param_list=[]):
  result.append(arg)
  print(result)
# 의도한 방향이 변수 값이 없을 때 빈 배열이라면 아래와 같이 수정이 필요하다.
def test_fix(arg, param_list=None):
  if param_list is None:
    param_list = []
  result.append(arg)
  print(result)

```
##### type
> * type 은 모든 클래스의 부모인 object의 metaclass, 즉 모든 클래스의 메타클래스가 type  
>   type의 역할
> * type(object): object의 타입을 반환
> * type(name, bases, dict): 새로운 클래스 생성
>   * name: 클래스이름
>   * bases: 상속받는 클래스들의 튜플
>   * dict: 속성과 메소드를 담은 dict
```python
# 클래스 생성 예제
# type('클래스명', (상속받는 클래스들의 튜플), {필드와 메소드를 담은 dict})
MyClass = type('MyClass', (object,), {'x': 1, 'y': 2})
my_class = MyClass() # 인스턴스 생성
```
> * type.__call__() 이 클래스를 생성하는 메서드이자, 모든 클래스는 type의 인스턴스  
>   클래스 내에서 \_\_call\_\_메서드를 따로 정의하지 않으면 type.\_\_call\_\_메서드가 동작  
>   type.\_\_call\_\_이 클래스를 선언하는 메소드지만 type을 상속받을 경우 자식의 환경에 영향을 받아
>   super().\_\_call\_\_은 type이 클래스(타입의 인스턴스)를 반환하듯이 인스턴스를 반환
```python
# 실행 순서 __new__ > __init__ > __call__(인스턴스가 호출 될 때 사용)
# MyClassA 를 클래스 선언 할 때, 메타클래스의 __new__, __init__ 이 실행되면서
# 메타클래스의 인스턴스로 MyClassA 클래스 선언 객체를 생성한다.
# MyClassA() 를 실행했을 때, MyClassA는 메타클래스의 인스턴스이므로,
# 메타클래스의 __call__ 를 실행해서 MyClassA 클래스의 객체를 생성한다.
# 그 이후 MyClass 내에 __new__, __init__ 이 호출 된다.
class MyMetaClassA(type):
    def __new__(cls, name, bases, attrs):
        print('metaclass __new__')
        return super().__new__(cls, name, bases, attrs)
        
	def __init__(cls, *args, **kwargs): 
		print('metaclass __init__')
		super().__init__(*args, **kwargs)

    def __call__(cls, *args, **kwargs):
        print('metaclass __call__')
        instance = super().__call__(*args, **kwargs)
        return instance
class MyClassA(metaclass=MyMetaClassA):
    pass
my_instance_a = MyClassA()

```
> 메타클래스(metaclass)
> * python 의 모든 것은 객체이고, 클래스 선언도 객체
> * 메타클래스의 인스턴스가 클래스 선언, 즉 클래스를 만드는 클래스가 메타클래스
> 메타클래스 활용 예제
```python
class Singleton(type):    # type을 상속받음
    __instances = {}      # 클래스의 인스턴스를 저장할 속성
    def __call__(cls, *args, **kwargs):    # 클래스로 인스턴스를 만들 때 호출되는 메서드
        if cls not in cls.__instances:     # 클래스로 인스턴스를 생성하지 않았는지 확인
            cls.__instances[cls] = super().__call__(*args, **kwargs)
                                           # 생성하지 않았으면 인스턴스를 생성하여 속성에 저장
        return cls.__instances[cls]        # 클래스로 인스턴스를 생성했으면 인스턴스 반환
 
class Hello(metaclass=Singleton):    # 메타클래스로 Singleton을 지정
    pass
 
a = Hello()     # 클래스 Hello로 인스턴스 a 생성
b = Hello()     # 클래스 Hello로 인스턴스 b 생성
print(a is b)   # True: 인스턴스 a와 b는 같음
```
> type.__mro__ 에 대해
```python
# __mro__(Method Resolution Order) 메서드 결정 순서
# 아래 소스에서 d.foo()는 과연 어떤 클래스의 foo메서드를 실행하게 될지 순서를 반환
# 1. 자식 클래스는 부모 클래스 보다 앞에 위치
# 2. 부모 클래스의 순서는 상속 시에 지정한 순서와 일치(클래스 D 선언 시 B, C 순서로 정의 했기 때문에 B가 먼저 위치)
# 3. 모든 부모 클래스는 한 번씩만 배치
# 4. object 클래스는 가장 마지막에 위치
class A:
    def foo(self):
        print("A")

class B(A):
    def foo(self):
        print("B")

class C(A):
    def foo(self):
        print("C")

class D(B, C):
    pass

d = D()
d.foo()
# D.mro() or type.mro(D)
# [<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```
> type 과 object의 관계에 대해
```python
# 모든 클래스의 부모는 object, 모든 객체의 타입도 object
# 모든 클래스의 메타클래스는 type, 그 이유는 object의 메타클래스가 type이고, object가 모든 클래스의 부모
# type은 object의 상속을 받고 object는 type의 객체
isinstance (type, object) # type은 object의 인스턴스인가? True
isinstance (object, type) # object는 type의 인스턴스인가? True
issubclass (type, object) # type은 object의 서브클래스인가? True
issubclass (object, type) # object는 type의 서브클래스인가? False
```
> type과 object가 서로가 서로를 필요로 하는 관계라면 생성될 수 없을 텐데 어떻게 생성될까?  
> ex) object가 없으면 type이 상속받을 수 없고, type이 없으면 object는 메타클래스로 type을 지정할 수 없다.  
> object와 type은 python에 가장 기본이 되는 내장 객체이며, 이는 python 인터프리터가 실행되기전에 C언어에서 구현된다.  
> 1. PyObject가 정의되며 PyObject는 모든 객체를 나타내며 타입과 참조 카운트 등의 정보를 가지고 모든 객체의 최상위 구조체
> 2. PyTypeObject가 정의되며 PyTypeObject는 PyObject를 상속받고, 클래스의 이름, 속성, 메소드, 부모 클래스 등의 정보를 가지고 type이 PyTypeObject의 python 구현체
> 3. PyBaseObject_Type가 정의되면 PyTypeObject의 상속을 받고, object클래스에 특화된 정보를 가지며, object가 PyBaseObject_Type의 python 구현체
> 즉 python의 object class는 PyBaseObject_Type의 구현체이며, type class는 PyTypeObject의 구현체, 그리고 모든 객체는 PyObject의 구현체입니다.

### GIL(Global Interpreter Lock)
> * CPython에서 사용되는 메모리 관리 방식, GIL은 한번에 하나의 스레드만 파이썬 바이트코드를 실행할 수 있도록 제한
> * 동일한 파이썬 객체에 대해 동시 수정을 막아 동시성을 제한하여 파이썬 인터프리터의 안정성을 보장하는 것이 목적
>   이와 관련해서 객체를 생성하면 참조 횟수(reference count)가 증가하는데, 동시에 다수의 스레드가 작업을 실행하면,
>   참조횟수가 제대로 처리되지 않아 0이 되면 동작하는 가비지컬렉션이 동작하지 않아서 메모리 누수, 성능저하 등의 문제가 발생이를 해결하기 위해 GIL을 사용
>   CPU 바운드 작업에서 멀티스레드를 사용해도 성능 향상을 기대하기 힘듬
> * 멀티 프로세싱 또는 비동기 프로그래밍으로 GIL로 인한 성능저하 방지가능
> * GIL로 인해 멀티스레드로 인한 성능 향상을 기대하기 힘듬에도 멀티스레드로 성능향상이 가능한 경우는  
>   I/O 바운드의 사용이 많을 때, 하나의 스레드에서 I/O 바운드가 진행되는 동안 다른 스레드가 CPU 바운드 작업이 진행될 수 있음
* [GIL에 대한 설명](https://it-eldorado.tistory.com/160)

### 문자열과 데이터 처리
* [split 문자열 나누기](https://mainia.tistory.com/5624)
* [문자열로 된 숫자 확인하는 방법](https://soooprmx.com/archives/10159)
* [문자열이 숫자로만 이루어져있는지 확인 isdigit()](https://blockdmask.tistory.com/556)
```python
# 문자열치환
replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수]) 
```
* [정규표현식 활용](https://greeksharifa.github.io/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D(re)/2018/08/04/regex-usage-05-intermediate/)
* [re 모듈 활용](https://velog.io/@ednadev/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC-re%EB%AA%A8%EB%93%88)
```python
# 앞뒤 공백제거
strip() 
```
````python
# 문자열 검색
 'abc'.index('a') # >>> 0 #인덱스를 반환 없을 예
 'abc'.find('a') # >>> 0 #인덱스를 반환 없을 경우 -1
````
### 변수와 스코프
* [변수 스코프 지정자 global, nonlocal](https://www.daleseo.com/python-global-nonlocal/)
* [ _, 언더스코어의 의미](https://doorbw.tistory.com/153)
> 클래스 변수와 인스턴스 변수가 동일 이름일 때 발생할 수 있는 현상  
```python
class TestClass():

    class_v = 0 # 클래스 변수 (자바의 static 변수와 비슷한 역할)

    def __init__(self) -> None:

        self.class_v += 1 # 인스턴스 변수 + 1
        # 위 코드는 실제로는 아래와 같이 계산 됨
        # self.class_v += 1 > self.class_v = self.class_v + 1
        # python에서 대입하는 변수를 찾는 순서
        # 1. 같은 이름의 인스턴스 변수를 찾음
        # 2. 1에 없으면 같은 이름의 클래스 변수에 찾음(현재 상황)
        # 3. 부모 클래스에서 같은 이름의 클래스 변수를 찾음
        # 4. 찾을 수 없을 때 같은 이름의 변수를 임의 생성
        TestClass.class_v += 1 # 클래스 변수 + 1

print(TestClass.class_v) # 클래스 변수 값 0

class_a = TestClass()
class_b = TestClass()
  
# 실제 동작은 인스턴스 변수 + 1 이 된게 아닌 클래스 변수 + 1이 된 상황
# 따라 첫번째 호출 떄는 0 + 1, 두번째 호출 때는 1 + 1의 값을 출력
print(f'class_a.class_v = {class_a.class_v}') # 인스턴스 변수 값 1
print(f'class_b.class_v = {class_b.class_v}') # 인스턴스 변수 값 2?

print(TestClass.class_v) # 클래스 변수 값 2

def a: 
	a = 0
	if a == 0:
	  b = 0
	print(a)
	print(b)
# 둘다 동작
# 자바스크립트의 var와 비슷하게 def 함수 안에서 전역으로 동작한다.
```

### 함수와 람다 표현식
##### 프레임 (frame)
> 프레임은 다음과 같은 정보를 가짐
> * 함수의 실행 정보를 가진 객체
> * 호출 스택(Call Stack): 함수가 호출되면 스택에 프레임이 추가되고, 종료되면 제거
> * 값 스택(Value Stack): 임시 변수 저장 스택
> * 지역 변수: 함수 내 정의된 변수 저장공간
> * 마지막 바이트 코드 명령어

* [filter 함수](https://wikidocs.net/22803)
* [lambda 함수(js에 화살표 함수랑 비슷)](https://wikidocs.net/64)
* [divmod(), 두 숫자를 나누어 몫과 나머지를 tuple 로 반환](https://technote.kr/259)
* [any, all 함수](https://blockdmask.tistory.com/430)
* [특수 매개변수 위치전용 매개변수](https://velog.io/@easttwave/python-%EB%8C%80%EC%9E%85-%ED%91%9C%ED%98%84%EC%8B%9D-%EC%9C%84%EC%B9%98-%EC%A0%84%EC%9A%A9-%EB%A7%A4%EA%B0%9C-%EB%B3%80%EC%88%98)
* [두개의 배열로 index 기준 dict로 만들 때 활용하는 ZIP함수](https://www.daleseo.com/python-zip/)
* [Counter 함수 객체의 구성원들의 수를 dict로 반환](https://www.daleseo.com/python-collections-counter/)
* [sum 함수 활용](https://stackoverflow.com/questions/33541947/what-does-the-built-in-function-sum-do-with-sumlist)
```python
  # sum의 기본 활용
  sum([1, 2, 3]) # 1 + 2 + 3 = 6
  sum([1, 2, 3], 1) # 1 + 1 + 2+ 3 = 7
  # sum의 추가 활용
  sum([[1, 2], [3, 4], [5, 6]], []) # [] + [1, 2] + [3, 4] + [5, 6] = [1, 2, 3, 4, 5, 6]
  # 뒤에 [] 추가 인자가 없으면 int가 아니라고 오류 발생 뒤에 추가 인자로 배열을 넣음으로 배열의 합으로 변환
```
```python
  # 무한대 표현 방법
  float('inf') # 양의 무한대
  float('-inf') # 음의 무한대
  
  # math 활용 
  import math
  math.inf # 양의 무한대
  -math.inf # 음의 무한대
```
* [map 함수 사용법 및 예제](https://hbase.tistory.com/404)
```python
  # dict 함수 활용 2차원 배열을 dict()로 감싸면 key, value 형태로 반환 가능
  [['a', 1]['b', 2]]  
```
* [양방향 큐 deque](https://chaewonkong.github.io/posts/python-deque.html)
* [heapq 사용법](https://juun42.tistory.com/20)
* [list 음수 슬라이싱](https://pybasall.tistory.com/217)
* [우선순위 큐와 힙큐(PriorityQueue & heapq) 비교](https://slowsure.tistory.com/130)
* [python 함수형프로그래밍 할 때 예제 및 장단점](https://velog.io/@keywookim/%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9C%BC%EB%A1%9C-%ED%95%A8%EC%88%98%ED%98%95%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%A7%9C%EA%B8%B0)
* [defaultdict](https://dongdongfather.tistory.com/69)
> defaultdict(<자료형>) 형식으로 dict 키의 값이 없을 때 default 값을 지정 가능
```python
 int_dict = defaultdict(int) # 기본 값이 0인 dict
 int_1_dict = defaultdict(lambda: 1)  # 기본 값이 1인 dict
 list_dict = defaultdict(list) # 기본값이 리스트 인 dict 
```

> Counter 객체를 카우팅 하는 컬렉션 dict
```python
from collections import Counter

num = [1, 2, 3, 4, 5, 1, 2, 3, 1, 2, 3, 4]
num_counts = Counter(num)
print(num_counts)
# Counter({5: 1, 1: 3, 2: 3, 3: 3, 4: 2})
```

### 제어 흐름
* [Case 문 형태인 match](https://docs.python.org/ko/3/tutorial/controlflow.html#match-statements)

### 반복문과 이터레이션
* [enumerate 반복문 적용시 인덱스와 객체 둘다 필요할때](https://wikidocs.net/16045)
* [itertools 의 각 함수 설명](https://velog.io/@davkim1030/Python-%EC%88%9C%EC%97%B4-%EC%A1%B0%ED%95%A9-product-itertools)
```python
   # 이터레이터 객체를 자를 때 사용하는 함수
   itertools.islice(iterable, 시작index, 종료index(바로 앞 index에서 절삭), 간격(필수 값 X))
```
##### Generator
* [Generator 개념 및 활용](https://velog.io/@jewon119/TIL30.-Python-%EC%A0%9C%EB%84%88%EB%A0%88%EC%9D%B4%ED%84%B0Generator-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)
> 제너레이터가 일반 이터레이터와 다른 점
> * yield 키워드를 사용해 다른 이터레이터에서 사용하는 next 함수 동작을 커스터마이징 가능
> * 피보나치 수열 같은 무한한 시퀀스 생성 가능
* [iterator, Generator 쉬운 설명](https://velog.io/@sawol/Python#iterable-%EA%B3%BC-iterator)
##### yield
> 함수 안에서 yield를 사용하면 함수는 제너레이터가 되며 yield에는 값(변수)을 지정
* [yield 이해하기](https://tech.ssut.me/what-does-the-yield-keyword-do-in-python/)
* [제너레이터와 yield](https://dojang.io/mod/page/view.php?id=2412)
```
# 제너레이터 중첩
# 제너레이터 함수를 yield from 을 통해 중첩
# 중첩 할경우
# 1. sub_generator 를 다 소화할 때까지 3회 반복
# 2. 4 출력
# 3. sub_generator2 를 다 소화할 때까지 3회 반복
# 4. 5 출력 과 같은 방식으로 진행

def sub_generator():
    yield 1
    yield 2
    yield 3


def sub_generator2():
    yield 'A'
    yield 'B'
    yield 'C'


def main_generator():
    yield from sub_generator()
    yield 4
    yield from sub_generator2()
    yield 5
```



### 클래스와 객체
* [클래스 json 변환](http://jsonpickle.github.io/)
* [\_\_init\_\_.py 사용 이유](https://mmjourney.tistory.com/14)
* [추상클래스](https://wikidocs.net/16075)
> 클래스 변수와 인스턴스 변수
> * 인스턴스 생성 없이 값을 요청 가능
> * 클래스 변수는 클래스의 인스턴스 끼리 값을 공유
```python
class ClassA:
  class_v = 0  # 클래스 변수
  def __init__(self, instance_v):
	self.instance_v = instance_v # 인스턴스 변수
        ClassA.class_v += 1 # 클래스 변수 값 증가
print(ClassA.class_v) # 0 # 인스턴스 생성 없이 값 확인

obj1 = ClassA(2)
obj2 = ClassA(3)

print(obj1.instance_v) # 2 인스턴스 변수는 독립적
print(obj2.instance_v) # 3
print(obj1.class_v) # 2 # 클래스 변수는 공유
print(obj2.class_v) # 2
```
> 클래스 메서드와 인스턴스 메서드
> * 클래스 메서드는 객체 생성 없이 실행가능
> * @classmethod 데코레이터를 메서드 위에 붙여서 선언
> * 첫번째 매개변수로 cls를 받고 cls를 통해 클래스 변수, 메서드에 접근
> * 클래스 변수와 메서드는 클래스가 선언되거나 import 될 때 메모리에 로드
```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1, arg2):
        # 클래스 메서드 내용

```
* [싱글톤 예제](https://codechacha.com/ko/python-singleton/)
> 변수와 객체의 생명 주기
```python
# 변수 선언 및 값 변경 예제
list1 = [1, 2, 3]
# 1. int class instance 1, 2, 3이 생성 되고 참조카운트 0으로 초기화
# 2. List class instance 가 생성되고 참조 카운트 0으로 초기화
# 3. List class instance와 int class instance 1,2,3 을 연결하고 1,2,3 의 참조카운트를 1로 변경
# 4. list1 식별자 생성하고 List class instance 와 연결하면서 참조카운트를 1로 변경
list2 = list1
# 5. list2 식별자 생성하고 list1 이 가르키고 있는 List class instance와 연결하면서 참조카운트를 2로 변경 
list1[0] = 100
# 6. int class instance 100이 생성 되고 참조카운트 0으로 초기화
# 7. List class instance의 0번째 인덱스에 100과 연결되고 참조카운트 1로 변경
# 8. int class instance 1의 참조카운트가 0으로 변경되면서 GC 대상이 됨
# 9. 스코프를 벗어나서 list1, 2 식별자가 더이상 사용되지 않으면 List의 참조카운트가 0으로 변경
# 10. List가 사라지면서 int class instance 도 참조카운트가 0으로 변경 되고 GC 대상이 됨
```
> 객체를 메서드처럼 사용
> * 객체를 () 로 호출 시 내부에 \_\_call\_\_() 함수가 동작
```python
# 객체 호출 사용 예제
# 1. 객체에 상태에 따라 동작하는 함수로 사용
class Adder:
	def __init__(self, n):
		self.n = n
	
	def __call__(self, x):
		return self.n + x

plus_3 = Adder(3) # 초기화 때 인스턴스에 특정 값을 저장해서 인스턴스

print(plus_3(4)) # Outputs: 7

# 2. 데코레이터로 사용
# 데코레이터로 사용 시, 해당 함수가 호출할 때 __call__ 이 호출
# init 은 데코레이터가 붙은 메서드가 선언될 때 실행
class Logger:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print(f"Calling function {self.func.__name__}")
        return self.func(*args, **kwargs)

@Logger
def add(a, b):
    return a + b

result = add(2, 3)  # add 함수를 래핑하여 호출될 때 로깅을 추가
```
#### NameSpace
> 변수나 함수, 클래스의 이름과 참조하는 객체 또는 메모리주소를 저장하는 테이블(매핑구조)
> * 식별자의 충돌을 방지
> * 네임스페이스의 식별자와 매칭되지 않은 객체는 참조 카운트가 0이 되므로 GC의 대상
```python
x = 1 # x식별자에 1이라는 int class 인스턴스 객체 주소가 연결
y = 2 # y식별자에 2라는 int class 인스턴스 객체 주소가 연결
x = y # x식별자에 2라는 int class 인스턴스 객체 주소가 연결
# 1의 값을 가진 int class 인스턴스 객체는 연결된 식별자가 없으므로 gc 대상

```


### 컨텍스트 관리
* [with 문 사용법](https://velog.io/@zkffhtm6523/Python-With%EB%AC%B8-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
* [async with 문 사용법](https://soooprmx.com/async-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-%EB%A7%A4%EB%8B%88%EC%A0%80/)
```python
# with 은 리소스 관리를 위해 사용
# 다음은 비동기적으로 네트워크 요청을 보내는 제너레이터 함수
async def fetch_url_async(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            yield await response.text()
# 실행 순서 및 생명주기
# 1. async with aiohttp.ClientSession() as session 를 실행하여 Http 클라이언트 세션 생성(__aenter__() 생성A)
# 2. async with session.get(url) as response 생성된 클라이언트 세션을 이용해서 Http요청을 보내고 (__aenter__() 생성B)
# 3. await response.text() 응답 데이터를 받아오고 yield 를 통해 데이터 반환
# 4. async with session.get(url) as response 에서 생성한 비동기 컨텍스트 매니저를 리소스 정리 (__aexit__() 로 클로즈B)
# 5. async with aiohttp.ClientSession() as session 에서 생성한 비동기 컨텍스트 매니저를 리소스 정리 (__aexit__() 클로즈A)
```



### 기타
* [python 버전별 새로운 기능](https://docs.python.org/3.11/whatsnew/index.html)
* [python DB인터페이스 DB-API 공식문서](https://peps.python.org/pep-0249/)
* [키 배열로 딕셔너리 생성 dict.fromkeys()](https://velog.io/@jaylnne/python-%ED%8C%8C%EC%9D%B4%EC%8D%AC-dict.fromkeys-%EB%94%95%EC%85%94%EB%84%88%EB%A6%AC-%EC%83%9D%EC%84%B1-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%A0%95%EB%A6%AC)
```python
  # join 메소드의 경우 배열 뿐만 아니라 dict 자료형에 사용할 경우 키들을 합쳐서 반환
```

```python
  # 두 개 이상의 값을 서로 바꿀 때, python에 동시에 변수 선언하는 것을 이용해서 바꿀 수 있음
  a[0], a[1] = a[1], a[0]
  a, b = b, a
```
* [12가지 python 런타임](https://www.itworld.co.kr/news/132322)
* [좌표간 거리 계산](https://stricky.tistory.com/283)
* [python 자잘한 팁 모음](https://towardsdatascience.com/100-helpful-python-tips-you-can-learn-before-finishing-your-morning-coffee-eb9c39e68958)
* [효율적인 메모리 관리 예제](https://deepwelloper.tistory.com/130)
* [순환 참조 문제 해결 방법 예제](https://www.pythonpool.com/python-circular-import/)
* [python 가비지 컬렉터 2가지 유형](https://devbull.xyz/python-garbace-collection/)

```python
  # 클래스 변수는 여러 인스턴스 간에 값을 공유
  class Account:
        num_accounts = 0	# 클래스 변수
        def __init__(self, name):	# 생성자
                self.name = name	# 인스턴스 변수
                Account.num_accounts += 1
		
  kim = Account("kim")	# 인스턴스 생성
  print(kim.num_accounts) # 1
  
  lee = Account("lee")

  print(lee.num_accounts) # 2
```


> 서버간 세션을 유지하기 위해서는 리스폰스에서 쿠키 값을 꺼내서 그 쿠키 값을 헤더에 넣어서 보내주면 유지가능(브라우저에서는 자동으로 이루어지는 부분)
> formData 를 만들때는 바디는 string 형식으로 a=1&b=2&c=3 식으로 데이터를 보내고 헤더에 폼형식을 넣어서 보냄.

```
 # 3항 연산자(삼항연산자), 자바나 자바스크립트와는 다름 참의 결과가 if 앞에 나옴
 <참 결과> if <조건> else <거짓결과>
 'True' if a == 1 else 'False'
 # 중첩할 경우 
 'True1' if a == 1 else 'True2' if a == 2 else 'False'
```

```python
# 나누기 할 때 주의 필요
 10 / 5 = 5.0
 10 // 5 = 5
 # // 사용으로 소숫점 아래를 삭제할 때, 작은 수로 변환됨
 # 아래 값은 -3.33333333... 이지만 소숫점 버림이 아닌 -3과 -4 중에 작은 수로 변환 됨
 10 // -3 = -4 
 
# 제곱근 표현
 10 ** 0.5
 math.sqrt(10)
```
```python
# 깊은 복사
# 리스트
a_list = [1, 2, 3]
b_list = a[:]
 
# 셋
a_set = {"1", "2", "3"}
b_set = a_set.copy()

# 딕셔너리
a_dict = {"a": 1, "b": 2}
b_dict = a_dict.copy()
```
```python
 # 10 진수의 부동소수점을 2진수로 똑같이 표현할 수 없어서
 # 실수 간의 비교는 항상 주의가 필요
 0.1 + 0.1 == 0.2 # False
 
 # 위 표현식을 비교하려면
 import math, sys
 x = 0.1 + 0.1
 math.fabs(x - 0.2) <= sys.float_info.epsilon # True
 
 # math.fabs 로 수식을 절대값으로 변환해서 비교
 # sys.float_info.epsilon에 저장된 값을 머신 엡실론(machine epsilon)이라고 부르는데, 
 # 어떤 실수를 가장 가까운 부동소수점 실수로 반올림했을 때 상대 오차는 항상 머신 엡실론 이하

 # 파이썬 3.5이상부터는 두 실수가 같은지 판단할 때 math.isclose 함수 사용
 math.isclose(0.1 + 0.1, 0.2)  # True
```
* [실수간의 비교 방법](https://dojang.io/mod/page/view.php?id=2466)
* [경우의 수 itertools](https://armontad-1202.tistory.com/entry/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%AA%A8%EB%93%A0-%EA%B2%BD%EC%9A%B0%EC%9D%98-%EC%88%98-%EC%B6%94%EC%B6%9C-%EA%B0%80%EB%8A%A5%ED%95%9C-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC)
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
* [bcrypt로 암호화](https://24hours-beginner.tistory.com/120)
***
> jwt 토큰
* [jwt 토큰 사용법](https://juneyr.dev/2018-01-28/making-token-pyjwt)
* [refresh token, access token](https://tansfil.tistory.com/59)
***
> 정적메소드
* [정적메소드 2가지 차이 staticMethod classMethod 차이](https://sshkim.tistory.com/184)
* [정적메소드 사용법 및 2가지 종류 차이](https://wikidocs.net/16074)
***



* [설정값 관리 방법](https://mingrammer.com/ways-to-manage-the-configuration-in-python/)
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
### 멀티쓰레드 & 멀티 프로세스
* [멀티쓰레드 & 멀티 프로세스](https://monkey3199.github.io/develop/python/2018/12/04/python-pararrel.html)
* [쓰레드 동기화(처리순서가 명확하게 필요할 때)](https://niceman.tistory.com/139)
* [멀티프로세싱 예제](https://doorbw.tistory.com/205)
* [병렬처리할때 공용으로 사용할 변수를 정의할때 multiprocessing.Manager()](https://docs.python.org/ko/3/library/multiprocessing.html)
* [Process, pool](https://m.blog.naver.com/qbxlvnf11/221558779545)
```python
 # 멀티 프로세스(함수에 매개변수 넣는 형태의 목록을 프로세스를 여러개 생성에서 병렬로처리) 
 # sqlAlcemy를 사용해서 db.session.commit() 을 바깥에서 할 경우 실제로는 커밋되지 않음(세션을 공유하지않음)
 pool = multiprocessing.Pool(processes=4)
 pool.map(<함수명>, <매개변수 리스트>)
 pool.close()
 pool.join()
```
> 멀티프로세싱을 사용할 때 운영체제 마다 리눅스는 fork, 윈도우는 spawn 매커니즘을 통해 프로세스를 복제함
* [쓰레딩 컨디션 객체 예제](https://snowdeer.github.io/python/2017/11/13/python-producer-consumer-example/)
* [Multithreading, Daemon thread, ThreadPoolExecutor 사용 방법](https://libertegrace.tistory.com/entry/Python-%EB%8F%99%EC%8B%9C%EC%84%B1%EA%B3%BC-%EB%B3%91%EB%A0%AC%EC%84%B1-%EB%AC%B8%EB%B2%95-Multithreading)

### 비동기
* [비동기 처리 asyncio](https://www.daleseo.com/python-asyncio/)
* [asyncio의 이해와 graceful shutdown](https://tech.buzzvil.com/blog/asyncio-no-1-coroutine-and-eventloop/)
* [asyncio 사용하기](https://dojang.io/mod/page/view.php?id=2469)
* [비동기 프로그래밍 동작 원리 (asyncio)](https://it-eldorado.tistory.com/159?category=749661)
* [비동기 프로그래밍 정리](https://velog.io/@heyoni/python-asyncio-1)
* [비동기 request처리](https://item4.blog/2017-11-26/Asynchronous-HTTP-Request-with-aiohttp/)
* [async/await 기초 코루틴과 테스크](https://kdw9502.tistory.com/6)
* [비동기 동작이 실행중 비동기 요청이 들어올 경우 오류 발생 대처방법](https://stackoverflow.com/questions/55409641/asyncio-run-cannot-be-called-from-a-running-event-loop)
* [FastAPI / uvicorn 호스팅 환경에서 asyncio 사용하는 방법](https://www.sysnet.pe.kr/2/0/13087?pageno=0)

#### Asyncio
###### 코루틴(Coroutines):  
> * async def 키워드를 사용해서 정의한 함수를 호출하여 생성하는 객체  
> * 특정 시점에 자신의 실행과 관련된 상태를 자체 저장하고 관리하며, 실행을 중단, 복원 할 수 있는 함수
> * 제너레이터 기반(yield from)
> * 스레드 상태와 같이 프레임 객체를 포함
> * 프레임이 기억하는 실행 인덱스로, 중단 및 재개에 활용 
> * 프레임이 저장하는 지역 변수로 상태를 유지 
###### 태스크(Tasks)
> * 코루틴 객체를 이벤트 루프에 등록하는 단위, 코루틴의 실행을 추적하고, 완료 시 결과를 저장
###### 이벤트루프(Event Loop)
> * 스레드 마다 1개씩 가지고 있으며, 이벤트를 처리하는 루프  
>   태스크를 스케줄링하고, I/O 작업이나 타이머와 같은 블로킹 연산을 만나면  
>   다른 태스크로 제어를 넘겨서 동시성을 구현
```python
  ## 시간 딜레이 추가
  await asyncio.sleep(<초>) 
```
###### 스트림(Stream)
> 소켓 통신을 구현한 고수준 API(비동기, 논블로킹)
###### 록(lock)[링크](https://docs.python.org/ko/3/library/asyncio-sync.html#lock)
> * 이벤트 루프에 존재하는 코루틴 사이에 동기화를 제공 
> * 스레드에 안전하지 않음
###### 이벤트(Event)[링크](https://docs.python.org/ko/3/library/asyncio-sync.html#event)
> * 이벤트 발생 시 태스크에 이벤트를 알림
> * set, clear 함수로 내부 플로그를 관리
> * wait 함수로 플래그가 set 함수의 호출을 대기
###### Condition
> * Event와 Lcok을 결합한 객체

> 이벤트 루프가 사용중이여서 오류 발생할 때
> * asyncio.run 함수는 이벤트루프를 생성하고, 실행하기 때문에  
>    이미 이벤트 루프가 생성 되어 있는 경우 충돌이 발생  [공식문서 링크](https://docs.python.org/3/library/asyncio-runner.html#id1)
```python
from fastapi import FastAPI  
import asyncio  
app = FastAPI()  
  
    
@app.get('/aio_func_test')  
async def aio_func_test():

# 이렇게 사용 시 충돌 발생
asyncio.run(my_func)

# 이미 실행 중인 루프에 테스크를 추가하는 방법
task1 = asyncio.create_task(my_func())  
await task1

return "test"  
  
  
async def my_func():  
await asyncio.sleep(1)  
print('my_func print')  
return "my_value"
```

> * 모듈을 이용해서 이벤트 루프 충돌을 피하는 방법
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
```python
a = [i for i in range(5)] # 리스트 생성
b = (i for i in range(5)) # generator 생성, 다만 일반적인 generator와 다르게 지연평가 하지 않고 모든 데이터를 메모리에 저장
```
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


### Typing
* [공식문서 상 Typing](https://python.flowdas.com/library/typing.html)
* [Typing 기초](https://sjquant.tistory.com/68)
* [Typing 심화](https://sjquant.tistory.com/69)
```python
# typing.Union 하나의 함수의 인자에 여러 타입이 사용될 수 있을 때
from typing import Union

def print_param(p: Union[str, bytes, None]) -> str:
  print(p)
  return p

# typing.Optional 특정 타입 또는 None 일때 사용
from typing import Optional
def print_param(p: Optional[str]) -> str:
  print(p)
  return p
# 3.10 버전부터 | 형태 지원 
def print_param(p: str | None) -> str:
  ...

# typing.TypedDict 딕셔너리의 경우 다양한 타입의 value가 있을 때 TypedDict를 상속받아서 클래스로 만들어서 사용
class Person(TypedDict):
  name: str
  age: int
  gender: str
def check_person(person: Person)->  int:
  ...

# 3.7 버전부터 dataclass 를 사용 가능
from dataclasses import dataclass

@dataclass
class Person:
  name: str
  age: int
  gender: str
```


##### 반복문 인덱스 구하기
```python
for i in range(len(array)): 
```
* [range 함수 활용](https://devpouch.tistory.com/70)

##### 배열
```python
  # 배열에서 인덱스를 정하는 부분에 조건식을 넣어서 0(거짓), 1(참)을 넣은 것과 동일하게 처리 가능
  result = ['a', 'b'][ 1 == 1] # 조건이 참이므로 1 이여서 인덱스 1인 'b'
  
  # 배열에서 쉽게 역정렬 하는 방법 [시작 index 음수로 할 경우 뒤에서부터 몇개 포함: 종료 index(미포함) 음수로 할경우 뒤에서 몇개 제외 : 몇개씩 + 또는 - 순서로]
  # [-1 : -1] > 교집합으로 뒤에서 1개 원소와 뒤에서 1개 원소를 교집함으로 나옴으로 빈 배열 출력
  result = ['a', 'b'][::-1]
```
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
  
  # set으로 교집합
  s1 & s2
  
  # set으로 합집합
  s1 | s2
  
  # set으로 차집합
  s1 - s2
```
```python
  # 배열 안에 데이터를 넣고 해당 값을 복사 생성할 때 주의할 점
  # 배열 안에 넣는 데이터가 자료형이 변경가능한 데이터(list, dict, 등)라면 * 로 하면 call by reference 여서 주의 필요
  a_list = [['a']] * 5   # a_list 는 ['a']를 복사하므로 배열에 대한 참조로 같은 배열이 복사됨(주소참조) 값을 바꿀경우 모든 값 변경
  b_list = [['a'] for i in range(5)]  # b_list 서로 다른 배열로 생성
```

##### 시간 다루기
* [날짜 차이 계산](https://jsikim1.tistory.com/144)
```python

# 현재 날짜
now  = datetime.now()

# 비교 대상이 되는 날짜
date_to_compare = datetime.strptime("20221225", "%Y%m%d")

date_diff = now - date_to_compare

# 시간 전체를 초로 변환
date_diff.total_seconds()
```
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


##### 특정 시간마다 실행(스케줄러)
* [특정시간마다 실행](https://tre2man.tistory.com/188)
* [apscheduler 기본 사용법](https://hello-bryan.tistory.com/216)
* [apscheduler missed job : 에러](https://jjeongil.tistory.com/944)
##### 예외
* [에러와 예외](https://docs.python.org/ko/3/tutorial/errors.html)
* [파이썬 에러와 예외 차이, 대표적인 에러 및 예외](https://www.entity.co.kr/entry/66-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%98%88%EC%99%B8-%EC%B2%98%EB%A6%AC-try-catch-finally-raise)
* [try, except, else finally 기본 사용법](https://devpouch.tistory.com/85)
* [예외 처리 raise, assert 등 활용](https://sikaleo.tistory.com/119)
* [try finally 동작순서](https://stackoverflow.com/questions/19805654/python-try-finally-block-returns)
```python
# except 뒤에 어떤 예외를 처리할지 생략하면
# 최상위 클래스인 BaseException 으로 처리
# BaseException 내부 클래스(Exception 제외)
# SystemExit: sys.exit() 함수로 발생
# KeyboardInterrupt: Ctrl+c 로 발생
# GeneratorExit: 제너레이터나 코루틴을 종료 시킬 시 발생
# StopIteration, StopAsyncIteration: 동기 또는 비동기 이터레이터를 중지 시킬 때 발생
# BaseException 에는 사용자가 의도한 종료 시그널 등이 있기 떄문에
# 의도를 명확하게 하고 사용해야함
try:
	# 내용
except:  # BaseException
	# 예외처리

# 아래와 같이 명확하게 지정필요
try:
	# 내용
except Exception as e:
	# 예외처리
```
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
* [데코레이터 이해를 위핸 규칙](https://engineer-mole.tistory.com/181)
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
* [pathlib 로 경로 다루기](https://engineer-mole.tistory.com/191)
###### 링크만들기(동일한 파일을 여러 이름으로 사용할때 등)
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
> aioredis 모듈이 redis 모듈로 통합

##### Pandas
* [판다스(Pandas) and 넘파이(Numpy) and 맷플롭립(Matplotlib)](https://wikidocs.net/32829)


##### 크롤링
* [Selenium을 활용한 크롤러](https://beomi.github.io/2017/02/27/HowToMakeWebCrawler-With-Selenium/)
* [Selenium 지연방법](https://codechacha.com/ko/selenium-explicit-implicit-wait/)
* [beautifulsoup](https://wikidocs.net/85739)

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

* [python으로 웹앱을 한번에 만들기 gradio](https://gradio.app/)

* [외부 프로그램 호출](https://www.delftstack.com/ko/howto/python/call-external-programs-python/)



## 버전
* [m1 macOS11 python 버전관리](https://laict.medium.com/install-python-on-macos-11-m1-apple-silicon-using-pyenv-12e0729427a9)
* [3.6이후 지원 변수주석](https://conansjh20.tistory.com/55)
```python
   # 변수명: 주석 = 대입 값 형태로 사용
   test_no:int = 123
   def test_func(param:int=0):
   	print(param)

   # 단순한 주석 역할 이기때문에 오류를 발생시키지는 않음
   test_func('aaa')
```
* [python 3.11 속도차이](https://docs.python.org/3.11/whatsnew/3.11.html)
* [python 3.11 정식릴리즈](https://www.python.org/downloads/release/python-3110/)
