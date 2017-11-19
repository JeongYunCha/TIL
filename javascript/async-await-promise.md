# async-await-promise

> 2017-11-10
>
> 요즘 진행하고 있는 [스터디(그룹웨어 API 만들기)](https://github.com/chachooon/typescript-node-express)에서 테스트 코드를 작성하며 콜백 중첩 문제를 접하게 되었다. 해결책으로 async-await-promise를 사용해보라는 피드백을 받고 ECMA Script6 스펙에 정식포함 되었다는 Promise 패턴을 공부하며 정리해보았다. 스터디 피드백과 검색을 통해 찾은 [블로그](http://programmingsummaries.tistory.com/325), [API 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)를 참고하였다.

<br>

자바스크립트는 거의 대부분의 작업들이 비동기로 이루어지고 비동기로 진행되는 작업이 완료되면 완료결과를 콜백함수로 알려주는 패턴이 많이 사용된다. 특정 이벤트가 발생하였을때 사용되는 콜백함수 호출 정도의 간단한 작업에서는 문제가 되지 않지만, 작업의 복잡도가 높아지게 되면 콜백으로 결과를 받은 뒤 다음 작업들을 순차적으로 진행하고자 할때 콜백 중첩으로 코드 관리가 어려지고 비동기작업으로 얻을 수있는 작업 성능 향상도 기대 할수 없게 된다.

[Promise 패턴]()을 사용하면 비동기 작업의 컨트럴이 수월해지고 코드의 가독성이 좋아진다. 또 예외처리에 대한 구조가 탄탄하기 때문에 오류 처리를 가시적으로 관리해 줄수 있다.



#### 1. Promise 선언부

```js
// Promise 선언
const myPromise = (param) => {
  return new Promise((resolve, reject) => {
    // 비동기를 표현하기 위해 setTimeout 함수를 사용 
    window.setTimeout(function () {
      if (param) {
        resolve("해결 완료");
      }	else {
		reject(Error("실패!!"));
      }
    }, 3000);
  });
};         
```

- pending : new 연산자로  Promise가 생성된 직후부터 resolve나 reject가 호출되기 전까지의 상태.
- fulfilled: 결과를 약속되로 잘줄수 있는경우, resolve함수를 호출한다.
- rejected: 약속된 결과 반환에 실패한 경우, reject함수를 호출한다.
- settled: 약속이 지켜졌든 실패했든 결론이 난 상태.




#### 2. Promise 실행부

__2.1. Promise.prototype.then(onFulfilled, onRejected)__<br>myPromise() 호출로 Promise 객체 리턴한다. 비동기 작업이 완료되었을 때 then()이 호출된다.

```js
myPromise(true).then((text) => {
  	console.log(text);
}, (error) => {
	console.log(error);
});
```

__2.2. Promise.prototype.catch(onRejected)__<br>promise가 연결(체이닝) 되어 있을때, `.then(null, function(){ })` 을 `catch()` 메서드 형태로도 표현할 수 있다.

```js
myPromise(true)
.then(JSON.parse)
.catch(() => { 
	console.log("체이닝 중간에 에러!"); 
})
.then((text) => {
	console.log(text);
});
```



#### 3. Promise.all API

여러개의 비동기 작업이 선행되고 이들이 모두 완료된 후  그다음 작업을 진행하고 싶다면 Promise.all API를 사용한다.

```js
var promise1 = () => {
	return new Promise(function (resolve, reject) {
		// 비동기를 표현하기 위해 setTimeout 함수를 사용 
		window.setTimeout(function () {
			resolve("첫번째 Promise 완료");
		}, Math.random() * 20000 + 1000);
	});
};

var promise2 = () => {
	return new Promise(function (resolve, reject) {
		// 비동기를 표현하기 위해 setTimeout 함수를 사용 
		window.setTimeout(function () {
			resolve("두번째 Promise 완료");
		}, Math.random() * 10000 + 1000);
	});
};

Promise.all([promise1(), promise2()]).then(function (values) {
	console.log("모두 완료됨", values);
});
```

위 예제를 return 하지않고  new Promise로 바로 할당하면 호출시 익명함수가 즉각 실행되므로 promise1.then()등의 형태로 여러차례 체이닝하여 사용할 수 있다. 

```js
var promise1 = new Promise((resolve, reject) => {
	// 비동기를 표현하기 위해 setTimeout 함수를 사용 
	window.setTimeout(() => {
		resolve("첫번째 Promise 완료");
	}, Math.random() * 20000 + 1000);
});

var promise2 = new Promise((resolve, reject) => {
	// 비동기를 표현하기 위해 setTimeout 함수를 사용 
	window.setTimeout(function () {
		resolve("두번째 Promise 완료");
	}, Math.random() * 10000 + 1000);
});


Promise.all([promise1, promise2]).then((values) => {
	console.log("모두 완료됨", values);
});
```



#### 4. async-await-promise를 통한 성능향상 

A라는 API의 결과와 B라는 API결과를 취합해서 얻은 값으로 작업 하려할때 일반적으로 코드를 작성하면 다음과 같다.

```arr = [];
for (데이터 n개) {
	const a = A API 결과
  	const b = B API 결과
  	const c = A + B
 	arr.push(c);
}
```

데이터가 n 개가 있을때 n개만큼 돌면서 A 라는 API를 호출해서 결과를 받아 A 에 저장하고 B라는 API 를 호출해서 결과를 받아 A와 B 결과를 취합하는 위 코드 에서 작업할 데이터 개수(n개)가 2000개고 A 라는 API가 0.5초의 응답속도를 B 라는 API도 0.5초의 응답속도를 보장한다 했을때 걸리는 작업시간은 최소 2000초가 된다. 

이것을 node + async + await + promise 를 이용하면 다음과 같이 구성할 수 있다. (psudo 코드)

```const a_api = () => request...
const a_api = () => request...
const b_api = () => request...
const a_b_sum = () => Promise.all([a_api(), b_api()]);
const fn = () => a_b_sum();
const actions = arr.map(fn);
const run = () => Promise.all(actions);

async () => {
  const result = await run();
  consol.log(result) ;
}
```


간단하게 설명하면 request 라는 비동기 API 라이브러리를 이용해서 a_api, b_api 를 호출 할 수있는 함수를 만들고 a, b api 결과를 취합해서 반환된 결과를 arr.map() 배열로 돌리면서 호출하도록 정의하고 모든 결과가 반환되면 처리해라. 이렇게 하면 API 가 2000 리퀘스트를 받아줄수있따는 전제로 API 호출결과는 for문이 도는 시간을 감안해도 1~2초 안에 끝나게 된다.

약 1000배의 성능향상과  콜백 지옥을 거의 해결 할 수 있다.
