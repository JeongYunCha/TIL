# 콜백함수: 비동기 프로그래밍 이해하기

> 2017-11-09

- 이벤트리스너: 해당 이벤트가 발생되었을때 실행되기위해 대기하고 있음
- 콜백: 이벤트가 실행되었을때 사용자에게 다시 알려준다.

```js
// on<이벤트명>
window.onload = function () {
  alert('I\'m clicked!');
};
```

```js
// addEventListener('<이벤트명>',function(){})
// removeEventListener('click',function(){})

function onClick() {
  alert('I\'m clicked!');
}
function onClick2() {
  alert('또다른 이벤트');
}
document.getElementById('clickMe').addEventListener('click', onClick); 
document.getElementById('clickMe').addEventListener('click', onClick2); 
document.getElementById('clickMe').removeEventListener('click', onClick)
```



- 콜백함수와 이벤트 리스너: 이벤트가 실행되었을때 사용자에게 다시 알려준다.

```js
var cbExample = function(number, cb) {
  setTimeout(function() {
    var sum = 0;
    for (var i = number; i > 0; i--) { sum += i;};
    cb(sum);
  }, 0);
};
cbExample(10, function(result) { console.log(result); }); // 55
console.log('first');
```



### 자바스크립트 실행 순서 

- 웹브라우저에 처리를 부탁하는 함수( 타이머 함수 , 웹 요청 관련 함수)의 처리는 실행코드가 끝난 이후.
- 익명함수와 선언함수의 실행순서 차이 : 익명함수는 순서대로 실행, 선언함수는 호이스팅 됨
- hoisting 호이스팅* :  모든 선언부를 위로 올려 실행



- 반복문과 콜백함수

```js
for (var i=0;i<3;i++) {
  (function ( closed_i ) {
    setTimeout (function ( ) { alert ( closed_i ); }, 0 );
  })( i );
}
```

