# JavaScript - 객체


프로토타입 객체 - 객체의 원형. 새로운 인스턴스 객체들을 만들도록 정의한 함수

new 연산자로 호출되는 함수(인스턴스) 안에서 사용되는 this는 그함수를 호출한 객체 자기자신. 

```js
// 프로토타입 객체 = Person함수 정의
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.walk = function(speed){
  console.log(speed + 'km속도로 걸어갑니다.');
}

// 생성자 = new 연산자로 호출되는 함수
// 생성자 함수로 객체를 만들면 그 객체 안에서 사용하는 this는 그함수를 호출하는 객체 자신.
var person01 = new Person('소녀시대', 20);
var person02 = new Person('걸스데이', 22);

console.log(person01.name + '객체의 walk(10)호출');
person01.walk(10);
```



1. Built-in Object(자바스크립트 내장객체)
2. Native Object(브라우져 내장 객체)
3. Host Object(사용자 정의 객체)

