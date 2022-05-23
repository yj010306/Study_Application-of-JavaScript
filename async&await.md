# async & await
---
## 1. async
``` javascript
function hello() {
  return "hello";
}

async function helloAsync() {
  return "hello async";
}

console.log(hello());
console.log(helloAsync());

helloAsync().then((res) => {
  console.log(res);
});
```
* `async`의  `return`값은 `promise`의 `resolve`값이다.

## 2. await
``` javascript
function delay(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function helloAsync() {
  await delay(3000);
  return "hello async";
}

async function main() {
  const res = await helloAsync();
  console.log(res);
}

main();
```
* `await`은 마치 비동기 함수가 동기 함수 처럼 작동하게 함
* `await`이 끝나길 기다렸다가 다음 동작이 실행 됨






