# Javascript
* [setInterval, setTimeout의 차이](https://www.jiwon.me/setinterval-vs-settimeout/?fbclid=IwAR3Y_Ul-RzI6wh3aGiLNLu9vEBNu-hbII_TWzcCRHsIW7Xec5kgKwG_rPCM)
* [prototype 이해](https://poiemaweb.com/js-prototype)
* [prototype 이해2](https://velog.io/@adam2/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Prototype-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)
* [prototype, \_\_proto__ 생활코딩](https://www.youtube.com/watch?v=wT1Bl5uV27Y)
* [prototype 유튜브 설명](https://www.youtube.com/watch?v=wUgmzvExL_E&t=16s)
* [valueOf 메소드](https://dev.to/composite/valueof-mesodeu-mweohareo-issnya-1n97?fbclid=IwAR3NbHOY1Y-H7jxBdIdUTw1gzL0cf3Mdx_hpcP76m24qr08CQK-whDqUe5Q)
* [ES6 문법정리](https://velog.io/@decody/ES6-Sheetsheet)
* [class 접근자 프로퍼티](https://velog.io/@bigbrothershin/JavaScript-%EC%A0%91%EA%B7%BC%EC%9E%90-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0-getter-setter)
* [변수 변경 탐지하기](https://www.zerocho.com/category/JavaScript/post/5a6578a3c994bd001ba0f9d9)
* [javascript set(중복불가능한 순서가 없는 배열)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set)
* [Object.defineProperty()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
```javascript
var someObj = {};
Object.defineProperty(someObj, 'valA', {
 get: function() {
   return this._a || 0;
 },
 set: function(num) {
   this._a = num;
   console.log(this._a); // 변경될때 일괄 동작 처리
 },
});

var a = { get b() {
  return this._b || 0;
 },
 set b(num) {
   this._b = num;
   console.log(this._b); // 변경될때 일괄 동작 처리
}};


someObj.valA++;
a.b++;
```


* [ES2015 proxy](https://www.zerocho.com/category/EcmaScript/post/57ca5f053316f61500c4f902)
##### web component
* [web component](https://developer.mozilla.org/ko/docs/Web/Web_Components)
* [web component의 구성요소 및 역할](https://d2.naver.com/helloworld/188655)
* [customerElement 생성](https://developer.mozilla.org/ko/docs/Web/Web_Components/Using_custom_elements)
```javascript
customerElements.defind('<새로만들 컴포넌트 명>', <html 정보를 가진 클래스 오브젝트>) 

class CustomInput extends HTMLElement {
 // connectedCallback 은 커스텀 엘리먼트가 document의 DOM에 연결될 때마다 호출
 // attributeChangedCallback은 커스텀 엘리먼트의 애트리뷰트가 추가, 제거 또는 변경될때 호출
 connectedCallback(){
  let label = document.createElement('label');
  label.innerHTML = '인풋A';
  this.appendChild(label);
  let input = document.createElement('input');
  this.appendChild(input);
 }
 // 변경점 감시 함수
 static get observerdAttributes(){
  return ['<변경점을 감시할 속성>']
 }
 // 변경점이 감시될때 실행될 함수
 attributeChangeCallback(){
  
 }
}

```
* [shadow DOM](https://developer.mozilla.org/ko/docs/Web/Web_Components/Using_shadow_DOM)


##### 비동기 처리

* [Promise](https://ko.javascript.info/promise-basics)

* async/await
  * [async/await 를 사용하기 전에 promise를 이해하기](https://medium.com/@kiwanjung/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4)
  * [async/await](https://joshua1988.github.io/web-development/javascript/js-async-await/)
  * [async/await 병목현상 해결](https://akasai.space/node-js/solving_promise_bottleneck/)

* [유니코드 정규화 방식 nomalize](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/normalize)
```javascript 
// 결합된 한글 문자열

// U+D55C: 한(HANGUL SYLLABLE HAN)
// U+AE00: 글(HANGUL SYLLABLE GEUL)
var first = '\uD55C\uAE00';


// 정규형 정준 분해 (NFD)
// 정준 분해 결과 초성, 중성, 종성의 자소분리가 일어납니다.
// 일부 브라우저에서는 결과값 '한글'이 자소분리된 상태로 보여질 수 있습니다.

// U+1112: ᄒ(HANGUL CHOSEONG HIEUH)
// U+1161: ᅡ(HANGUL JUNGSEONG A)
// U+11AB: ᆫ(HANGUL JONGSEONG NIEUN)
// U+1100: ᄀ(HANGUL CHOSEONG KIYEOK)
// U+1173: ᅳ(HANGUL JUNGSEONG EU)
// U+11AF: ᆯ(HANGUL JONGSEONG RIEUL)
var second = first.normalize('NFD'); // '\u1112\u1161\u11AB\u1100\u1173\u11AF'


// 정규형 정준 결합 (NFC)
// 정준 결합 결과 자소분리 되었던 한글이 결합됩니다.

// U+D55C: 한(HANGUL SYLLABLE HAN)
// U+AE00: 글(HANGUL SYLLABLE GEUL)
var third = second.normalize('NFC'); // '\uD55C\uAE00'

```
```javascript
 // base64
 btoa()  //  base64로 인코딩
 atob()  //  base64로 디코딩
 // base64 인코딩 오류시
 btoa(unescape(encodeURIComponent(str)))
```
* [** javascript 내부 명렁 처리 순서 stack, queue, 등](https://www.youtube.com/watch?v=v67LloZ1ieI)
```
1. 실행 컨텍스트(Execution Context):
코드가 실행될 때 생성되는 객체로(주로 함수가 실행될 때 만들어 짐)
실행 컨텍스트는 변수, 함수 선언, 매개변수 등의 정보를 담고 있으며,
함수가 실행되는 동안 이 정보를 사용하여 코드를 실행하고,
실행이 끝나면 파기

2. 호출 스택(Call Stack):
호출 스택은 실행 컨텍스트가 쌓이는 스택 자료구조.
자바스크립트 엔진은 코드의 실행 순서를 관리하기 위해 호출 스택을 사용.
함수가 호출될 시 추가되고, 종료되면 제거.

3. WebAPIs(비동기 함수와 이벤트 리스너):
비동기 처리 및 이벤트 리스너가 실행되면, WebAPIs를 통해 등록 및 처리되고, 완료 및 이벤트 발생 시
이벤트 큐로 콜백을 전달 하는 역할을 수행

4. 이벤트 큐(Event Queue):
이벤트 큐는 비동기 함수의 콜백 함수 또는 이벤트 리스너의 발생한 이벤트들이
대기하는 큐 자료 구조의 공간

5. 이벤트 루프(Event Loop):
이벤트 루프는 호출 스택과 이벤트 큐를 모니터링하고,
호출 스택이 비어있을 때 이벤트 큐에 있는 함수들을 호출 스택으로 옮기는 역할
이벤트 루프는 호출 스택이 비어있는지 반복적으로 확인하며,
비어있으면 이벤트 큐에서 함수를 하나씩 꺼내어 호출 스택으로 옮김
```
* [Script 인클루드 할때 옵션 async defer](https://www.youtube.com/watch?v=tJieVCgGzhs)

```javascript
// import, export 종류 및 차이

////////////// named export 각각 export, import 해서 사용
//cal.js
export const plus = (a, b) => a + b;
export const minus = (a, b) => a - b;

// main.js
import { plus } from './cal'; // 이름이 export 이름과 동일

////////////// default export 각 파일당 1개만 가능
//cal.js
const plus = (a, b) => a + b;
const minus = (a, b) => a - b;
export default { plus, minus }

// main.js
import cal from './cal'; // 이름 마음대로 지정가능
cal.plus(1,2);


////////////// default export, named export 가 섞여있는 경우
//cal.js
const plus = (a, b) => a + b;
export const minus = (a, b) => a - b;
export default plus

// main.js
import plus, { minus } from './cal'; // default 는 기본형식으로, named 는 {} 괄호를 이용해 import 


////////////// dynamic import 필용한 상황에 불러오기
//cal.js
export const plus = (a, b) => a + b;
export const minus = (a, b) => a - b;

// main.js
function callAnything(){
 // then 방식
 import('./cal').then(cal => cal.plus(2, 2));
 // async/await 방식
 const cal = await import('./cal');
 cal.plus(2, 2);
}

// 해당 내용 출처
// https://www.youtube.com/watch?v=WUirHxOBXL4

```


### 성능개선
* [javascript 성능을 높이는 코드 스타일](https://12bme.tistory.com/134)
* [기본적인 웹사이트 최적화 방법](https://12bme.tistory.com/128?category=682905)
```javascript
// Code #1 - String 객체를 이용한 문자열 생성 
var str = new String("abcdefghijklmnopqrstuvwxyz"); 
// Code #2 - 리터럴을 이용한 문자열 생성 (속도가 더 빠름)
var str = "abcdefghijklmnopqrstuvwxyz";

```

### npm
* [npm 명령어 정리](https://velog.io/@archivvonjang/npm-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC)

```bash
# 디펜던시를 가져오는 명령어
> npm ls --depth=0 
```
