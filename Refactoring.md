# Refactoring

* 매직 넘버를 기호 상수로 치환
  + 특정 의미를 가진 구분 값을 그대로 사용하지 말고 상수에 저장해서 명확하게 표현하고,
  반복사용에도 수정을 용이하게 한다.
```
  // 기존 소스
  if(a == 100){...}
  
  // 변경소스
  const optionA = 100;
  if(a == optionA){...}
  
```

* 제어 플래그 삭제
  + 흐름을 제어하기 위한 변수를 break, continue, return 으로 변환한다.
```
  // 기존 소스
  flag = true;
  while(flag){
    ...
    if(A){
      flag = flase;
    }else{
      ...
    }
  }
  // 변경 소스
  while (true){
    ...
    if(A){
      break;
    } else {
      ...
    }
  }
```

* 가정 설정문 도입(assertion)
  + 값이 특정 형태나 값이여야 할때 미리 오류를 검증하는 방법
```
  ## python 
  
  ## a == 2 가 아닐때 에러를 발생시켜 해당 조건문을 검증한다.
  >>> a = 3
  >>> assert a == 2 

  #결과
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  AssertionError
```
