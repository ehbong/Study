# Typescript

* [공식 페이지](https://www.typescriptlang.org/)
* [Typescript 기본설명](https://www.samsungsds.com/kr/insights/TypeScript.html)
* [TypeScript 가이드북](https://yamoo9.gitbook.io/typescript/)

* [TyepScript 환경설정 및 시작하기](https://mine-it-record.tistory.com/578)

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
