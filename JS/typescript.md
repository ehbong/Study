# Typescript

* [공식 페이지](https://www.typescriptlang.org/)
* [Typescript 기본설명](https://www.samsungsds.com/kr/insights/TypeScript.html)
* [TypeScript 가이드북](https://yamoo9.gitbook.io/typescript/)
* [TyepScript 환경설정 및 시작하기](https://mine-it-record.tistory.com/578)
* [Never 타입](https://ui.toast.com/posts/ko_20220323)
* [ts-node 타입스크립트 파일을 별도의 컴파일 없이 자동 컴파일하여 실행 시켜주는 라이브러리](https://github.com/TypeStrong/ts-node)
* [Declare, Ambient-Module](https://bum-developer.tistory.com/entry/TypeScript-Declare-Ambient-Module)

```typescript
// declare 명령어는 자바스크립트 작성된 라이브러리를 타입스크립트에 사용할 때
// TypeScript에서 컴파일 될 때 타입이슈로 문제가 생기는 걸 방지하기 위해 사용.
// 사용 예
// 외부 라이브러리의 타입 참조
declare module 'library-name' {
  export function someFunction(): void;
  export const someValue: number;
  // ...
}

// 현재 스코프에 존재하지 않는 변수, 함수, 클래스 등의 타입 선언
declare const globalVariable: string;
declare function customFunction(arg: number): string;
declare class MyClass {
  // ...
}

// 사용 예시
globalVariable = 'Hello'; // 외부 변수 사용
const result = customFunction(42); // 외부 함수 호출
const instance = new MyClass(); // 외부 클래스 인스턴스 생성

```

### 이슈
```javascript
// typesciprt 에서 console.log 오류 발생 시
// tsconfig.json 안에
"lib": [
            "es6",
            "dom"    <------- Add this "dom" here
        ],
```

```typescript
# 함수를 통해 객체를 생성할 경우
function Person(this: any, name: string, age: number): void {
    this.name = name;
    this.age = age;
}
# 자바스크립트에서는 아래와 같이 작성할 경우 오류가 발생하지 않는데
const person1 = new Person("Maddison", 21);
# 타입스크립트에서는 아래와 같이 작성할 경우 오류 발생
const person1:Person = new Person("Maddison", 21);
# 오류이유는 생성자 함수가 따로 정의되지 않아서, Person타입을 받을 수 없고
# 이를 any로 형변환 시켜서 사용할 수 있음
const person2: any = new (Person as any)("Maddison", 21);

```

```typescript
// 모듈을 import 할 때 @ 표시 루트 경로는 tsconfig.json 안에
// paths 값 안에 특정 경로를 별칭으로 등록할 때 사용할 수 있음
// @가 아닌 다른 것을 사용할 수 있지만 관습적으로 @를 사용
// tsconfig.json 예
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@src/*": ["src/*"]
    }
  }
} 
import HttpStatusCodes from '@src/constants/HttpStatusCodes';
```
