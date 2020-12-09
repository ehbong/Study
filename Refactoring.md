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

* 메서드 추출
  + 너무 긴 메소드(함수)를 기능단위 또는 중복을 제거해서 나눈다.
```
  // 기존소스
  function printText(text){
    var barLength = 10;
    var str = "";
    // 구분선 추가
    for(var i = 0; i < barLength; i++){
      str += "-";
    }
    
    // 내용 출력
    for(var i = 0; i < barLength; i++){
      str += text+"\n";
    }
    
    // 구분선 추가
    for(var i = 0; i < barLength; i++){
      str += "-";
    }  
  }
  
  // 바뀐소스
  function printText(text){
    
    var str = "";
    // 구분선 추가
    str = setBorder(str);
    
    // 내용 출력
    str = setContent(str, text);
    
    // 구분선 추가
    str = setBorder(str);
    
    console.log(str);
    
  }
  
  function setBorder(text){
    var barLength = 10;
    for(var i = 0; i < barLength; i++){
      text += "-";
    }
    return text;
  }
  
  function setContent(sumtext, text){
    
    for(var i = 0; i < barLength; i++){
      sumtext += text+"\n";
    }
    return sumtext;
  }
  
```

* 조건 분기 간결화
  + if문의 조건이 너무 복잡할 경우 함수로 분리함
```
  // 변경 전
  if(sx <= px && px < ex && sy <= py && ey){
  }
  
  // 변경 후
  if(isInside()){
  }
  
```
