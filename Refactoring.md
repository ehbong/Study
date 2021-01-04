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

* 반복문을 파이프라인으로 바꾸기
  파이프라인형으로 이해하기 쉬운 코드로 변경
```
  // 변경전
  const names = [];
  for (const i of input){
    if(i.job === "programmer") name.push(i.name)
  }
  
  // 변경 후
  const names = input
    .filter(i => i.job === "programmer")
    .map(i => i.name);
```

* 변수 쪼개기
  변수에 여러번 대입이 들어가는 경우역할에 따라 변수를 쪼개서 사용한다
```
  // 변경 전
  let temp = 2 * (height + width);
  console.log(temp);
  temp = height * width;
  console.log(temp);
  // 변경 후
  const perimeter = 2 * (height + width);
  console.log(perimeter);
  const area = height * width;
  console.log(area);
```

* 조건문 분해하기
  복잡한 조건문을 함수로 추출해서 코드의 이해를 돕는다.
```
  // 변경 전
  if (fromDate > new Date() && toDate < new Date())
    action = a * b;
  else
    action = a + b;
  
  // 변경 후
  if (checkInDate())
    action = multiply();
  else
    action = plus();
    
  // 한줄로 표현가능
  action = checkInDate() ? multiply() : plus();
      
  function checkInDate(){
    return fromDate > new Date() && toDate < new Date();
  }
  
  function multiply(){
    return a * b;
  }
  function plus(){
    return a + b;
  }
```

* 중첩 조건문을 보호 구문으로 바꾸기
```
  // 변경 전
  function getPayAmount(){
    let reuslt;
    if (isDead)
      result = deadAmount();
    else {
      if (isSeparated)
        result = separatedAmount();
      else {
        if (isRetired)
          result = retiredAmount();
        else
          result = normalPayAmount();
      }
    }
    return result;
  }
  // 변경 후
  function getPayAmount(){
    if (isDead) return deadAmount();
    if (isSeparated) return separatedAmount();
    if (isRetired) return retiredAmount();
    return normalPayAmount();
  }
```

* 질의 함수와 변경 함수 분리하기
```
// 변경 전
 function getTotalOutstandingAndSendBill(){
  const result = customer.invoices.reduce((total, each)=> each.amount + total, 0);
  sendBill();
  return result;
 }

// 변경 후
function totalOutstanding(){
  return customer.invoices.reduce((total, each)=> each.amount + total, 0);
}
function sandBill(){
  emailGateway.send(formatBill(customer));
}
```
