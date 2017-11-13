# JavaScript - 함수 



함수 (= 메소드) : 작업을 수행하거나 값을 계산하는 문장 집합

```js
// 1. 선언적 함수
function add(a, b){ return a+b };	
// 2. 익명 함수
function (a, b){ return a+b };	
// 3. 변수에 익명함수 할당하기 
var add = function (a, b){ return a+b }; 
// 4. 번수에 함수 호출결과 값 할당하기
var result = add(10,10);

console.log(add(10, 20)); // 1,2,3. 함수호출
console.log(result);	// 4. 함수호출
```



즉시호출 함수표현식<br>글로벌 스코프에 정의된 함수는 어디서든지 접근가능 --> 즉시실행함수 내에 처리로직 모아두면 변수명 충돌 방지 가능

```js
// 기명 즉시실행함수
(function myFunction() {
  var a = 3;
  var b = 5;
  return a * b;
}());
// 익명 즉시실행함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
}());
```



내부함수: 함수 내부에서 선언된 함수. <br>내부/자식에서 외부/부모함수 변수에 접근가능하지만 에서 외부/부모함수에서  내부/자식 호출할 수없다.

```js
function parent(param) {
  var parentVar = param;
  function child() {
    var childVar = 'lee';
    console.log(parentVar + ' ' + childVar); // Hello lee
  }
  child();
  console.log(parentVar + ' ' + childVar);
  // Uncaught ReferenceError: childVar is not defined
}
parent('Hello');
```





콜백함수 :  파라미터로 전달되는 함수

```js
// 함수를 호출했을 때 또다른 함수를 파라미터로 전달하는 방법
function add(a, b, callback) {
  var result = a + b;
  callback(result);
};

add(10, 10, function(result){ 
  console.log(result);
}); 
```



클로저: 리턴값으로 함수를 반환해 외부에서 내부함수에 접근할수 있다.

```js
// 함수 안에서 값을 반환할 때 새로운 함수를 만들어 반환하는 방법
function add(a, b, callback) {
  var count = 0
  var result = a + b;
  callback(result);
  
  var history = function() {
    count++;
    return count +':'+ a +'+'+ b +'='+ result;
  };
  return history;
};

// 리턴값으로 반환된 history를 실행하기 위해 호출문 끝에 ()를 붙인다. 
add(10, 10, function(result){ 
  console.log(result) 
})();

// 반환된 함수를 통해 내부함수 접근하기
var add_history = add(10, 10, function(result){ 
  console.log(result);
}); 

// 반환된 함수를 add_history에 기억해 뒀다가 추가작업을 할수있다.
console.log(add_history());
console.log(add_history());
console.log(add_history());
```



