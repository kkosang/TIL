# _2022-05-28 SAT_

## <em>2.0 First JS Project</em>

- 브라우저가 html을 열고 html이 css와 javascript를 가져옴
- 일반적으로 css파일은 head 윗부분에 가져오고 js파일은 body 마지막부분에서 가져옴

## <em>2.1 Basic Data Types</em>

- integer, float , string

## <em>2.2 Variables</em>

- 콘솔에게 메시지 보냄
  : console.log( 숫자 or "문자열" , '문자열' )
  : 콘솔에 log 또는 print함

- 변수 만들기
  1. const사용 => constant(상수)
     - ex) const a = 5;
     - const // 값 변경 불가
- 변수이름 규칙
  - 공백사용 X
  - 공백이 필요하다면 다음 단어의 첫 글자를 대문자로 작성
  - ex) veryLongVariableName // camelcase
  - _cf) 파이썬에서는 \_로 표시함 // snakecase_

## <em>2.3 const and let</em>

- 변수 만들기 2
  - let사용 // let은 값 변경 가능
- const & let
  - _cf)예전에는 var 사용_
  - 대부분 const 사용하고 때에 따라 let
  - var는 값을 보호해 주지 못함
    - most => const
    - sometime => let
    - never => var

## <em>2.4 Booleans</em>

- Booleans

  - true / false의 값을가짐
  - _cf) phyton에서는 대문자 표기 True / False_
  - const amIFat = false;

- Null
  - 값이 존재하지 않음을 뜻함
  - 비어있음을 뜻함
- undefined
  - 변수 선언하고 초기화 하지 않은 경우
  - undefined값
  - 메모리공간은 존재하지만 값이 들어가지 않음

## <em>2.5 Arrays</em>

- 주로 같은타입 나열
- ex) const week = [ "mon" , "tue" , "wed" .. "sat" ];
- week[0] ;
- 선언시 배열 크기를 지정하지 않음
- 배열에 값 추가
  - week.push("sun"); // 배열의 맨 마지막에 값이 추가됨

# _2022-05-29 SUN_

## <em>2.6 Objects </em>

- Object만들기
  - const player = { name: "sanghyun" , points 10, fat : true ,}; // 주로 여러가지 타입 나열
  - =를사용하지 않고 :를 사용
- Object사용
  - console.log(player.name);
  - console.log(player["name"]);
- Update Error
  - player.fat = false; // 변경 가능
  - const player인데 값 변경? // object안에 변수를 변경하기 때문에가능
  - player = false ; // error 전체를 하나의 값으로 업데이트 할 때, player는 object타입인데 boolean으로 변경시 에러 발생
- Add property
  - player.lastName ="Ko"; // property추가 가능

## <em>2.7~2.8 Functions part One / Two</em>

- 함수정의 - function plus ( a, b ) {
  } //여기서 a,b는 parameter

- 함수호출
  - plus(a,b); // 여기서 a,b는 argument
- Object안에 func 만들기

```
const player={
  name: "kosang",
  sayHello: function(){

  }
}
// object.function(argument) 사용가능
```

## <em>2.9~2.10 Recap</em>

## <em>2.11 Returns</em>

- Func에서 연산한 결과 return하지 않으면 func을 빠져 나올 때 value를 얻을 수 없음
- Func 호출 시 func의 결과값을 return하여 variable에 할당하여 func외부에서 사용하기 위함
- Func에서 Return하면 func은 결과 값을 return하고 실행종료

## <em>2.12 Recap</em>

## <em>2.13~2.15 Conditionals </em>

- Prompt() : 사용자에게 창을 띄워 줌
  - how to use
  - Prompt( message , default );
    - 사용시 javascript 일시정지
    - css 적용불가
    - 최근에는 사용하지 않고 html , css로 이용함
    - return => string => 크기 비교 불가
- parseInt() : A string to convert into a number.
  - How to use
  - parseInt(string);
    - 숫자로 변경할 수 없을 때
    - return => NaN ( Not a Number )
    - return => Int
- isNaN( number ) : number가 number인지 판단
  - return => boolean
  - number라면 false number가 아니라면 true
- if/else

```
If(condition) {
	// condtion1 == true
}
Else if(condition) {
	// condition1 == false
	// &&
	// condition2 == true
}
Else{
	// condition1 == false
	// &&
	// condition2 == false
}
	: condition은 boolean으로 판별

```
