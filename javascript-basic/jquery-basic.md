

### jQuery 

##### 1. jQuery 시작하기

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



#### 2. 문서객체 선택과 탐색

##### 2.1 jQuery 선택자

```javascript
$(*).css('color','red');			// 전체 선택자

$('h1,p').css('color','red');		// 태그 선택자

$('#target').css('color','red');	// 아이디 선택자
$('h1#target').css('color','red');	// 특정 id속성을 가지는 태그 선택

$('.item').css('color','red');			// 클래스 선택자
$('h1.item').css('color','red');		// 특정 클래스속성을 가지는 태그 선택
$('.item.select').css('color','red');	// 복수의 클래스속성을 모두 가지는 태그 선택
```

```javascript
$('body > *').css('color','red');	// 자손 선택자 (body태그 바로 아래 요소만 선택)
$('body *').css('color','red');		// 후손 선택자 (body태그 안 요소 전체 선택)
```

```js
$('input[type="text"]').val("Hello")	// 속성 선택자
$('input[type|="text"]').val("Hello")	// 속성 값이 특정 값과 같은 문서객체 선택
$('input[type~="text"]').val("Hello")	// 속성 값이 특정 단어로 시작하는 문서객체 선택
$('input[type^="text"]').val("Hello")	// 속성 값이 특정 값으로 시작하는 문서객체 선택
$('input[type$="text"]').val("Hello")	// 속성 값이 특정 값으로 끝나는 문서객체 선택
$('input[type*="text"]').val("Hello")	// 속성 값이 특정 값을 포함하는 문서객체 선택
```

```javascript
// 입력양식 필터 선택자
$('input:text').val("Hello")			// 입력양식 필터선택자로 간단하게 표현
$('select > option:selected').val()		// option객체 중 선택된 태그의 값 
$('요소:checked')		
$('요소:disabled')
$('요소:enabled')
$('요소:focus')
$('요소:input')
```

```js
// 위치 필터 선택자
$('요소:odd')		// 홀수 번째 위치한 문서객체 선택
$('요소:even')	// 짝수 번째 위치한 문서객체 선택
$('요소:first')	// 첫 번째에 위치한 문서객체 선택
$('요소:last')	// 마지막에 위치한 문서객체 선택
```

```javascript
// 함수 필터 선택자
$('요소:contain(문자열)')	// 특정 문자열 포함한
$('요소:eq(n)')			// n번째 위치
$('요소:gt(n)')			// n번째 초과한 위치
$('요소:lt(n)')			// n번째 미만에 위치
$('요소:has(h1)')			// h1 태그가 있는
$('요소:not(선택자)')		// 선택자와 일치하지 않는
$('요소:nth-child(3n+1)')	// 3n+1번째에 위치하는
```

##### 2.2  메서드로 문서객체 선택하기

2.2.1 필터 메서드: $('요소').filter()

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
$('hi').filter(':even').css('color','red').end().filter(':odd').css('background','white');
````

2.2.2 특정위치 선택 메서드: $.eq(), $.first(), $.last()

````

````

2.2.3 추가 선택 메서드: $.add()

2.2.4 특징 판별 메서드: $.is()

2.2.5 특정 태그 선택 메서드: $.find()

2.2.6 $.parseXML()로 문서 탐색

2.2.7 $.parent() 메서드

##### 2.3. 배열 관리: $.each() , $.forEach()

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

##### 2.4. 객체 확장: $.extend()

````js
$(document).ready(function () { 
	var object ={ name : '홍길동'};
  	
  $.extend(object,{
    	region: '서울',
    	age: '30',
    	hobby: '기타연주'
  })
});
````

````js
// $.extend()로 객체 결함
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
}
````

##### 2.5. 충돌 방지: $.noConflict()

````js
// 자바스크립트 프레임워크, 플러그인간 충돌 방지
$.noConflict();
jQuery(document).ready(function(){
 	 //jQuery 사용
});

// 간단한 표현: 충돌 제거와 사용 분리
$.noConflict();
var J = jQuery;

J(document).ready(function(){
	  //jQuery 사용
});
````



#### 3. 문서 객체 조작

##### 3.1 문서 객체 클래스 속성 조작: $.addClass(),  $.removeClass()

##### 3.2 문서 객체 속성 조작: $.attr(), $.removeAttr()

##### 3.3 문서 객체 스타일 조작: $.css()

##### 3.4 문서 객체 내부 조작: $.html(), $.text()

````js
// text(), html() 차이 비교
$('div').html(function(index){
  	return '<h1> 제목' + index + '</h1>';
})
$('div').text(function(index){
  	return '<h1> 제목' + index + '</h1>';
})

// 매개변수 두개 사용
$('h1').html(function(index,html){
  	return '***'+ html + '***';
})
````

##### 3.5 문서 객체 삭제:  $.remove(), $.empty() 

##### 3.6 문서 객체 생성: $('요소').attr('속성', '값')

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

    $('h1').on('click', function(){
        $(this).html(function(index,html){
            return html + '+';
        });
    })


#### 5. 효과 



##### 







