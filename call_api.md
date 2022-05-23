# API & Fetch
---
## 1. API 호출
* `API 호출` : `서버`에게 데이터를 요청(Request)하고 전달(Response)받는 과정
* 프로그램끼리의 대화 방법
* 어떠한 데이터를 전달(Response)받기 위한 목적으로 사용

## 2. `API 호출`과 `함수`의 차이점
* 응답(Response)이 언제될 지 알 수 없음
  * 때문에 `비동기 호출`을 사용함
  
## 3. API 호출 실습(`fetch()`)
``` javascript
let response = fetch('https://jsonplaceholder.typicode.com/posts').then((res) => {
	console.log(res);
};
```
* `fetch()` : 자바스크립트에서 `API 호출`을 할 수 있도록 도와주는 내장 함수

## 4. `json`형식의 값을 뜯어오기
``` javascript
async function getData() {
  let rawresponse = await fetch("https://jsonplaceholder.typicode.com/posts");
  let jsonresponse = await rawresponse.json();
  console.log(jsonresponse);
}

getData();  // 100개의 객체배열 출력
```




