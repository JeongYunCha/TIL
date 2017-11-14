^2017-11-06^

# jQuery 시작하기

```javascript
$(document).ready(function () { 

});

$(function() { }); // 간단한 형식
```

문서가 준비되면 매개변수로 넣은 콜백함수 실행 (`window.onload = function() { };` 와 비슷한 기능)

```
window.jQuery = window.$ = jQuery;
```

자바스크립트의 식별자`$`를 jQuery 식별자로 사용한다.



#### 1. 선택자 ([w3schools 실습예제 보기](https://www.w3schools.com/jquery/trysel.asp))

##### 1.1 기본 선택자

```javascript
$(*).css('color','red');			// 전체 선택자

$('h1,p').css('color','red');		// 태그 선택자

$('#target').css('color','red');	// 아이디 선택자
$('h1#target').css('color','red');	// 특정 id속성을 가지는 태그 선택

$('.item').css('color','red');			// 클래스 선택자
$('h1.item').css('color','red');		// 특정 클래스속성을 가지는 태그 선택
$('.item.select').css('color','red');	// 복수의 클래스속성을 모두 가지는 태그 선택
```

##### 1.2 자손/후손 선택자

```javascript
$('body > *').css('color','red');	// 자손 선택자 (body태그 바로 아래 요소만 선택)
$('body *').css('color','red');		// 후손 선택자 (body태그 안 요소 전체 선택)
```

##### 1.3 속성 선택자

```js
$('input[type="text"]').val("Hello")	// 속성 선택자
$('input[type|="text"]').val("Hello")	// 속성 값이 특정 값과 같은 문서객체 선택
$('input[type~="text"]').val("Hello")	// 속성 값이 특정 단어로 시작하는 문서객체 선택
$('input[type^="text"]').val("Hello")	// 속성 값이 특정 값으로 시작하는 문서객체 선택
$('input[type$="text"]').val("Hello")	// 속성 값이 특정 값으로 끝나는 문서객체 선택
$('input[type*="text"]').val("Hello")	// 속성 값이 특정 값을 포함하는 문서객체 선택
```

##### 1.4 입력양식 필터 선택자

```javascript
$('input:text').val("Hello")			// 입력양식 필터선택자로 간단하게 표현
$('select > option:selected').val()		// option객체 중 선택된 태그의 값 
$('요소:checked')		
$('요소:disabled')
$('요소:enabled')
$('요소:focus')
$('요소:input')
```

##### 1.5 위치 필터 선택자 

```js
$('요소:odd')		// 홀수 번째 위치한 문서객체 선택
$('요소:even')	// 짝수 번째 위치한 문서객체 선택
$('요소:first')	// 첫 번째에 위치한 문서객체 선택
$('요소:last')	// 마지막에 위치한 문서객체 선택
```

##### 1.6 함수 필터 선택자 

```javascript
$('요소:contain(문자열)')	// 특정 문자열 포함한
$('요소:eq(n)')			// n번째 위치
$('요소:gt(n)')			// n번째 초과한 위치
$('요소:lt(n)')			// n번째 미만에 위치
$('요소:has(h1)')			// h1 태그가 있는
$('요소:not(선택자)')		// 선택자와 일치하지 않는
$('요소:nth-child(3n+1)')	// 3n+1번째에 위치하는
```



#### 2. 문서객체 검색/탐색

##### 2.1 필터 메서드: $.filter()

````js
$(selector).filter(selector);

// 매개변수로 함수를 넣을 경우
$('h3').filter(function (index) {
  	return index % 3 == 0;
}).css({
    background:'white',
 	color:'red'
});
// 문서 객체 탐색 메서드 체이닝과 탐색 종료 메서드.end() 
$('hi').filter(':even').css('color','red')
  .end().filter(':odd').css('background','white');
````

##### 2.2 특정 위치 선택 메서드: $.eq(), $.first(), $.last()

````js
$('h1').eq(0).css('background','white');
$('h1').first().css('background','white');
$('h1').last().css('background','white');
````

##### 2.3 추가 선택 메서드: $.add()

```js
$('h1').css('background','white').add('h2').css('float','left');
```

##### 2.4 특징 판별 메서드: $.is()

```js
$('h1').each(function(){
 	 if($(this).is('.select')){
		$(this).css('background','white');
 	 }
})
```

##### 2.5 특정 태그 선택 메서드: $.find() 와 $.parseXML()로 문서 탐색하기

```js
var xml = '<friend> </friend>...';
var xmlDoc = $.parseXML(xml);

$(xmlDoc).find('friend').each(function(index){
	var output = '';
  	output +='<h1'
});

```

##### 2.7 $.parent() 메서드              

```js
$('button').click(fuction(){
    $(this).text('비활성화하기');
	$(this).parent().css('background','white');
	$(this).parent().find('span').text('활성화');
});
```

##### 2.8 배열 관리: $.each() , $.forEach()

````js
[].forEach(function(item, index){  }); 	// ECMAScript 5 에서 추가됨
$.each(function(index, item){  });
````

````js
$(document).ready(function () { 
  // $.each() 사용법
  $('h1').each(function(index, item){	
       $(item).addClass('cassName-'+ index);
       //$(this).addClass('cassName-'+ index); 
  });
  
  // $.addClass() 유사사용법 참고
  $('h1').addClass(function(index){	
		return 'className-' + index;
  }); 
});
````

##### 2.9 객체 확장: $.extend()

````js
$(document).ready(function () { 
	var object ={ name : '홍길동'};
  	
  $.extend(object,{
    	region: '서울',
    	age: '30',
    	hobby: '기타연주'
  });
});
````

````js
// $.extend()로 객체 결합
var object = $.extend({a:10},{a:20,b:20},{c:30});
````

````js
// $.extend()로 옵션객체 보완
function test(options) {
  options = $.extend({
    valueA:10,
    valueB:20,
    valueC:30
  },options);
};
````

##### 2.10 충돌 방지: $.noConflict()

````js
// 자바스크립트 프레임워크, 플러그인간 충돌 방지
$.noConflict();
jQuery(document).ready(function(){

});

// 간단한 표현: 충돌 제거와 사용 분리
$.noConflict();
var J = jQuery;
J(document).ready(function(){

});
````



#### 3. 문서 객체 조작

##### 3.1 문서 객체 클래스 속성 조작: $.addClass(),  $.removeClass()

```js
$('h1').addClass('className');
$('h1').removeClass('className');

$('h1').toggleClass('className');
```

##### 3.2 문서 객체 속성 조작: $.attr(), $.removeAttr()

```js
// $(selector).attr(name, value);
$('img').attr('width',200);

// $(selector).attr(name, funcrtion(index, attr){ });
$('img').attr('width', function(index){
  	return (index + 1) * 100;
});

// $(selector).attr(object);
$('img').attr({
    width: function (index){
      	return (index + 1) * 100;
    }
});
```

```js
$('h1').removeAttr('data-index');
```

##### 3.3 문서 객체 스타일 조작: $.css()

```js
// 스타일 값 검사
var color = $('h1').css('color');

// 스타일 값 추가
$('h1').css('color','red');

// 스타일 값 추가-2
var color =['red','green','blue']
$('h1').css('color', function(index){
  	return color[index];
});

// 스타일 값 추가-3
var color =['red','green','blue']
$('h1').css({
  color: function (index){
    return color[index];
  },
  background: 'black'
});
```

##### 3.4 문서 객체 내부 조작: $.html(), $.text()

````js
// text(), html() 차이 비교
$('div').html(function(index){
  	return '<h1> 제목' + index + '</h1>';
})
$('div').text(function(index){
  	return '<h1> 제목' + index + '</h1>';
})

// 매개변수 두개 사용한 경우
$('h1').html(function(index,html){
  	return '***'+ html + '***';
})
````

##### 3.5 문서 객체 삭제:  $.remove(), $.empty() 

```js
$('h1').first().remove();
$('div').empty();
```

##### 3.6 문서 객체 생성: $('요소').attr('속성', '값')

```js
$('<h1></h1>');

// 문서 객체 생성. 텍스트 노드 추가. 문서 객체 연결 
$('<h1></h1>').html('Hello World..!').appendTo('body');

// 문서 객체 생성. 이미지 속성 추가. 문서 객체 연결 
$('<img/>').attr('src', 'img.jpg').appendTo('body');
```

##### 3.7 문서 객체 삽입과 이동

````js
$(A).appendTo(B)		// A를 B의 뒷부분에 추가
$(A).prependTo(B)		// A를 B의 앞부분에 추가
$(A).insertAfter(B)		// A를 B의 뒤에 추가
$(A).insertBefore(B)	// A를 B의 앞에 추가
$(A).append(B)		// B를 A의 뒷부분에 추가
$(A).prepend(B)		// B를 A의 앞부분에 추가
$(A).after(B)		// B를 A의 뒤에 추가
$(A).before(B)		// B를 A의 앞에 추가
````

```js
$(document).ready(function () { 
	// 첫번째 사진을 마지막으로 보낸다.
	$('img').first().appendTo('body');
  
  	// 2초마다 첫번째 사진을 마지막으로 보낸다.
    setInterval(function(){
      	$('img').first().appendTo('body');
    },2000);
});
```

##### 3.8 문서 객체 복제: $.clone()

```js
$(select).clone()
$(select).clone(Boolean dataAndEvents)
$(select).clone(Boolean dataAndEvents, Boolean deepDataAndEvents)
```

```js
$(document).ready(function () { 
	$('div').append($('h1').clone());
});
```



#### 4. 이벤트 

##### 4.1 이벤트 연결/제거

```js
// 이벤트 연결
$('h1').on('click', function(){
    $(this).html(function(index,html){
        return html + '+';
    });
});

$('h1').on({
	mouseenter: function () { $(this).addClass('reverse');},
	mouseleave: function () { $(this).removeClass('reverse');}
});
```
```js
// 간단한 이벤트 연결.hover()
$('h1').hover(function(){
  	$(this).addClass('reverse');
}, function(){
  	$(this).removeClass('reverse');
});

// 이벤트 제거하기.off()
$('h1').click(function(){
  	alert('이벤트 발생!');
  	$(this).off();
});

// 한번만 연결하기.one()
$('h1').one('click',function(){
  	alert('이벤트 발생!');
});
```

##### 4.2 이벤트 연결 범위 한정하기 (delegate)

```js
$('h1').on('click','h1', function(){
    $(this).html(function(index,html){
        return html + '+';
    });
});
```

##### 4.3 이벤트 객체

```js
event.pageX 			// 브라우저 화면기준 마우스 X좌표 위치
event.pageY				// 브라우저 화면기준 마우스 Y좌표 위치
event.preventDefault()	// 기본 이벤트 제거
event.stopPropagation()	// 이벤트 전달을 제거
```

##### 4.4 이벤트 강제 발생 $.trigger()

```js
// 1초마다 함수 실행하기
setInterval(function (){
  	$('h1').last().click();
},1000);

// 매개변수 전달
$('h1').click(function (event, data1, data2){ alert(data1 + data2); });
$('h1').eq(1).trigger('click',[232,123]);
```

##### 4.5 마우스 이벤트

##### 4.6 키보드 이벤트

##### 4.7 윈도우 이벤트 

##### 4.8 입력 양식 이벤트

##### 4.9 화살표 함수 사용하기



#### 5. 효과 



##### 



