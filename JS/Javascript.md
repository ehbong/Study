# Javascript


* [ES6 문법정리](https://velog.io/@decody/ES6-Sheetsheet)

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
