# Javascript

* [prototype 이해](https://poiemaweb.com/js-prototype)
* [prototype 이해2](https://velog.io/@adam2/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Prototype-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)
* [prototype, \_\_proto__ 생활코딩](https://www.youtube.com/watch?v=wT1Bl5uV27Y)
* [prototype 유튜브 설명](https://www.youtube.com/watch?v=wUgmzvExL_E&t=16s)
* [ES6 문법정리](https://velog.io/@decody/ES6-Sheetsheet)

* [변수 변경 탐지하기](https://www.zerocho.com/category/JavaScript/post/5a6578a3c994bd001ba0f9d9)
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
* [내부 명렁 처리 순서 stack, queue, 등](https://www.youtube.com/watch?v=v67LloZ1ieI)
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
