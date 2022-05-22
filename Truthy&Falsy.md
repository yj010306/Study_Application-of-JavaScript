# Truthy&Falsy
---
## 1. 참 같은 값?, 거짓 같은 값?
* 자바스크립트에는 `boolean` 자료형이 아니라도 `True`나 `False`로 인식이 되는 것이 있다.
``` javascript
let a = [];
let a = {};
let a = 123;
let a = "0";
let a = Infinity;

if (a) {
  console.log("true");  // 실행
} else {
  console.log("false");
}
```
* `[]`, `{}`, `숫자`, `값이 있는 문자열`, `Inginity` 등은 `True`로 인식한다.
* 위와 같은 것을 `참 같은 값`이라 해서 `Truthy`라 한다.
``` javascript
let a = undefined;
let a = 0;
let a = NaN;
let a = "";

if (a) {
  console.log("true");
} else {
  console.log("false");
}
```
* `undefined`, `숫자 0`, `NaN`, `""`등은 `False`로 인식한다.
* 위와 같은 것을 `거짓 같은 값`이라 해서 `Falsy`라 한다.

## 2. `Truthy` & `Falsy` 활용
``` javascript
const getName = (person) => {
  if (!person) {
    return "객체가 아닙니다.";
  }
  return person.name;
};

let person;
const name = getName(person);
console.log(name);
```
* 일치하는 데이터가 없는 값이 함수로 전달이 된다면 오류가 발생한다.
* `undefined`와 `null`을 찾아내기 위해서 조건문에 `!(찾는값)`을 이용한다.










