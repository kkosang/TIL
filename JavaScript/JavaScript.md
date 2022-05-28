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

- Booleans _cf) phyton에서는 대문자 표기 True / False_

  - true / false의 값을가짐
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
