# JavaScript - 객체

> 2017-11-09

#### 1. 기본자료형은 변경 불가능한 값이다 

 : Booolean, null, undefined, Number, String, Symbol



#### 2. 기본자료형 이외의 모든 값은 객체(Object) 타입이며 변경 가능한 값이다.

user2는 객체타입으로 값을 변경 할수있지만, user1과 같은 어드레스를 참조하고있기때문에 값이 함께 변한다.

```js
var user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

var user2 = user1; // 변수 user2는 객체 타입이다.

user2.name = 'Kim';

console.log(user1.name); // Kim
console.log(user2.name); // Kim
```



#### 3. 불변데이터 패턴

객체를 불변객체로 만들어 레퍼런스를 참조한 다른객체에서 값을 의도치않게 변경하는일을 막는다.

-  [__Object.assign__](http://poiemaweb.com/js-immutability#21-objectassign) : 객체의 방어적 복사
-  [__Object.freeze__](http://poiemaweb.com/js-immutability#22-objectfreeze) : 불변객체화를 통한 객체 변경 방지
-  [__Immutable.js__](http://poiemaweb.com/js-immutability#23-immutablejs) : List, Stack, Map, OrderedMap, Set, OrderedSet, Record와 같은 영구 불변 (Permit Immutable) 데이터 구조를 제공





자바스크립트에서 객체를 만드는 방법 2가지 {}, new

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

