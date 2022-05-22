# Promise
---
## 1. `비동기 작업`이 가질 수 있는 상태
* `Pending(대기상태)` : 현재 비동기 작업이 진행중이거나 무언가 문제가 발생한 것을 의미
* `Fulfilled(성공)` : 비동기 작업이 의도한대로 정상적으로 완료한 상태
* `Rejected(실패)` : 모종의 이유로 인해 비동기 작업이 완료되지 못함
* `Pending -> Fulfilled` : resolve(해결)
* `Pending -> Rejected` : reject(거부)

## 2. resolve & reject
### `resolve & reject`의 예
``` javascript
function isPositive(number, resolve, reject){
	setTimeout(() => {
		if(typeof number === 'number'){
			resolve(number >= 0 ? "양수": "홀수";
		} else {
			reject("주어진 값이 숫자형 값이 아닙니다");
		}
	}, 2000);
}

isPositive(
	10, 
	(res)=>{
		console.log("성공적으로 수행 됨 : ", res);					
	}, 
	(err)=>{
		console.log("실패 : ", err);
	});

isPositive(
	[], 
	(res)=>{
		console.log("성공적으로 수행 됨 : ", res);					
	}, 
	(err)=>{
		console.log("실패 : ", err);
	});
```
### 호출부를 `promise`를 활용하여 다시 작성
``` javascript
function isPositiveP(number){
	const executor = (resolve, reject)=>{
		setTimeout(() => {
			if(typeof number === 'number'){
				resolve(number >= 0 ? "양수": "홀수";
			} else {
				reject("주어진 값이 숫자형 값이 아닙니다");
			}
		}, 2000);
	};

	const asyncTask = new Promise(excutor);
	return asyncTask;
}

const res = isPositiveP(101);

res
	.then(
		(res)=> {
			console.log("성공 : ", res)
	})
	.catch(
		(err)=>{
			console.log("실패 : ", err)
	});
```
* 함수가 반환값으로 `Promise` 객체를 반환하는 것은 함수가 `비동기작업`을 미리 실행하고 그 결과를 `Promise` 객체로 반환받아 사용할 수 있는 함수가 된다는 것을 의미.
* `Promise` 객체에서 `executor`의 `콜 백`은 각각 `resolve : then`, `reject` : `catch`의 `콜 백` 함수로 매칭 됨. 
* `Promise` 객체의 `then` 메서드를 통해서 `resolve`를 실행한다. 
* `Promise` 객체의 `catch` 메서드를 통해 결과에 대한 `reject`를 실행한다.

## 3. CALLBACK HELL
``` javascript
function taskA(a, b, cb) {
  setTimeout(() => {
    const res = a + b;
    cb(res);
  }, 3000);
}

function taskB(a, cb) {
  setTimeout(() => {
    const res = a * 2;
    cb(res);
  }, 1000);
}

function taskC(a, cb) {
  setTimeout(() => {
    const res = a * -1;
    cb(res);
  }, 2000);
}

taskA(3, 4, (a_res) => {
  console.log("A TASK RESULT : ", a_res);
  taskB(a_res, (b_res) => {
    console.log("B TASK RESULT : ", b_res);
    taskC(b_res, (c_res) => {
      console.log("C TASK RESULT : ", c_res);
    });
  });
});
```
### `Promise`객체를 사용하여 `CALLBACK HELL` 탈출
``` javascript
function taskA(a, b){
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const res = a + b;
			resolve(res);
		}, 3000)
	});
}

function taskB(a){
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const res = a * 2;
			resolve(res);
		}, 1000)
	});
}

function taskC(a){
	return new Promise((resolve, reject) => {
			setTimeout(() => {
			const res = a * -1;
			resolve(res);
		}, 2000)
	});
}

taskA(5, 1).then((a_res) => {
	console.log("A RESULT : ", a_res);
	return taskB(a_res);
}).then((b_res) => {
	console.log("B RESULT : ", b_res);
	return taskC(b_res);
}).then((c_res) => {
	console.log("C RESULT : ", c_res);
});
```
* 탈출 성공!!!!






