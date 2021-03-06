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

# _2022-05-30 MON_

## <em>3.0 The Document Object</em>

- JavaScript는 HTML에 이미 연결되어 있음
- 브라우저에서 제공하는 document 객체를 이용하여 JS에서 html의 항목을 읽거나 변경할 수 있음

## 3.1 HTML in JavaScript

- document.getElementById("");
  - 인자값으로 id 작성 // string
  - JavaScript에서 id를 통해 HTML의element를 가져올 수 있음
- console.dir();
  - element를 더 자세하게 보여줌
  - 이름앞에 on이 붙어있으면 event listener임

## 3.2 Searching For Elements

```
	document.getElementByClassName("");
	document.getElementByTagName("");
```

- 이 경우 array의 형태로 return함 // object가 아니기 때문에 method() 사용 불가

- document.querySelector("");
  - element를 css방식으로 검색할 수 있음
  - (".className tagName");
  - 단 하나의 element를 return해줌
  - _cf) 해당되는 모든 element를 return 하고 싶다면 .querySelectorAll 사용 // array형태_

## 3.3~3.5 Events

- 모든 event들을 JS가 listen할 수 있음
- addEventListener("eventName ", call funcName );
  - Event를 listen하기 위함
  - listen하고 싶은 event이름
  - event발생시 호출 하고 싶은 func 이름

```
const title = document.querySelector("div.hello h1");

function handleTitleClick() {
  title.style.color = "blue";
}

function handleTitleEnter() {
  title.innerText = "Mouse is here !!";
}

function handleTitleLeave() {
  title.innerText = "Mouse is gone..";
}

title.addEventListener("click", handleTitleClick);
title.addEventListener("mouseenter", handleTitleEnter);
title.addEventListener("mouseLeave", handleTitleLeave);

```

// click이벤트 발생시 title의 색상을 blue로 바꿈
<br> // mouse이벤트 발생시 text 변경

- 이벤트 사용 2가지 방식

  - .addEventListener("event Name", func Name );
    - .removeEventListener 하기에 더 편리함
  - .onclick = func Name ;

- window 이벤트 (JS에서 기본제공)
  - window.addEventListener("resize", func Name)
    - // resize 화면크기 바뀜
      <br>//document의 body,head,title 이런것들은 중요하기 때문에
      document.body.style~의 명령이 허용되지만, div같은것들은 호출이 안됨
      <br> document로 호출하면 .body / .head / .title 사용가능
  - window.addEventListener("on/offline", func Name) // WIFI 연결 여부

## <em>3.6~3.8 CSS in Javascript</em>

- element의 style을 JS에서 변경하는건 좋은 방법이 아님

- 똑같은 raw string이 있을 때 변수를 만들어서 사용 할 것

- .classList

  - .className은 이전 class들을 보호하지 못하고 모든걸 교체함
  - h1.classList.contains("clickedClass")
  - clickedClass가 h1의 classList에 포함되는지 판별

- toggle
  - class name이 존재 하는지 확인
  - class name이 존재한다면 toggle은 class name을 제거
  - class name이 존재하지 않는다면 toggle은 class name을 추가

```
  const clickClass = "clicked";
 if (h1.classList.contains(clickClass)) {
    h1.classList.remove(clickClass);
  } else {
    h1.classList.add(clickClass);
  }
// toggle 내용
=== h1.classList.toggle("clicked");
```

# _2022-05-31 TUE_

## 4.0 Input Values

- input의 내용을 가져오려면 value property사용
- html에서 value값 설정 시 input의 값을 미리 설정

## 4.1 Form Submission

- user의 input값을 유효성 검사를 하기 위해서 input이 form안에 있어야함
- form안에 있는 btn을 누르거나 input의 type이 submit일 경우
  - form이 submit될 때 마다 브라우저는 페이지를 새로고침 함

## 4.2~4.3 Events

- 모든 EventListener func의 첫번째 argument는 항상 지금 막 벌어진 일들에 대한 정보 담고있음 - 정보를 얻기 위해선 첫번째
  parameter를 설정
- preventDefault( )
  - 어떤 event의 기본 행동이든지 발생되지 않도록 막음
  - 기본 행동이란 어떤 func에 대해 브라우저가 기본적으로 수행하는 동작임 // form을 submit하면 브라우저가 기본적으로 페이지를 새로고침하는 동작

```
function onLoginSubmit(event) {
  event.preventDefault(); //페이지 새로고침 막아줌
  console.log(loginInput.value);
}

loginForm.addEventListener("click", onLoginSubmit);
```

# _2022-06-01 WED_

## 4.4 Getting Username

- 일반적으로 string만 포함된 변수는 대문자 표기 // string을 저장하고 싶을 때
- display:none;과 visibility:hidden; 차이점
  - visibility:hidden; // 공간은 그대로 두고 보이지만 않음
  - display:none; // 공간도 사라짐
- string과 변수를 합치는 방법
  - "Hello " + username;
  - \`Hello ${username}`;

## 4.5 Saving Username

- local storage
  - 브라우저에 데이터를 저장할 수 있게 해줌
  - localStorage.setItem(" ", ); // key(저장될 값의 이름)와 value
  - localStorage.getItem(" ");
  - localStorage.removeItem(" ");

## 4.6 Loading Username

```
const savedUsername = localStorage.getItem(USERNAME_KEY);

if (savedUsername === null) { // 저장된 이름이 없을 경우
  loginForm.classList.remove(HIDDEN_CLASSNAME); // form을 보여주고
  loginForm.addEventListener("submit", onLoginSubmit); // submit이벤트
} else { // 저장된 이름이 있을 경우
  paintGreetings(savedUsername); // 저장된 이름을 화면에 출력
}
```

## 4.7 Recap

## 5.0 Intervals

- '매번' 일어나야 하는 무언가를 뜻함
  // 매 n초마다
- setInterval( arg1, arg2 );
  - arg1 // 호출하고자 하는 func
  - arg2 // 호출하는 func 간격 ms

## 5.1 Timeouts and Dates

- setTimeout( arg1, arg2 );
  - func를 일정 시간이 흐른뒤에 한번만 호출
  - arg1 // 호출하고자 하는 func
  - arg2 // 몇ms후 func를 호출할지
- new Date()
  - 날짜나 시간을 보여주는 object
  - date.getHours(); // 시간
  - date.getMinutes(); // 분
  - date.getSeconds(); // 초

```
function getClock() {
  const date = new Date();
  clock.innerText = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
}

getClock(); //1초를 안기다리고 호출하기 위함
setInterval(getClock, 1000);
```

## 5.2 PadStart

- padStart(arg1, arg2);
  - pads the current string with a given string
  - string에 쓸 수 있는 func
  - arg1 // string의 길이를 맞춰줌
  - arg2 // arg1의 길이를 충족하지 못한다면 string의 앞쪽에 arg2의 string을 채워줌
  - _cf) padEnd(arg1, arg2); // 뒤쪽에 string 채워줌_

## 5.3 Recap

# _2022-06-02 THU_

## 6.0 Quotes

- Math.random()
  - 0부터 1사이의 랜덤 숫자 제공
- Math.round()
  - 숫자를 반올림 시켜줌
- Math.Ceil()
  - 올림
- Math.floor()
  - 내림

## 6.1 Background

- js이용해서 html파일에 랜덤이미지 추가하기
- document.createElement(arg1);
  - create an instance of the element
  - arg1 // tagName

```
//make array
const images = ["0.jpeg", "1.jpeg", "2.jpeg", "3.jpg", "4.jpg", "5.jpg"];
// choose random images
const chosenImage = images[Math.floor(Math.random() * images.length)];
// make tag => <img>
const bgImage = document.createElement("img");
// make src => <img src="img/">
bgImage.src = `img/${chosenImage}`;
// append html body
document.body.appendChild(bgImage); // prepend 가장 위에 생성
```

## 6.2 Recap

## 7.0 Setup

```
const toDoForm = document.getElementById("todo-form");
const toDoInput = toDoForm.querySelector("input");
const toDoList = document.getElementById("todo-list");

function handleToDoSubmit(event) {
  event.preventDefault();
  const newTodo = toDoInput.value;
  toDoInput.value = "";
}

toDoForm.addEventListener("submit", handleToDoSubmit);
```

## 7.1 Adding ToDos

```
//submit event에서 발생한 value의 값을 html에 만들기
function paintToDo(newToDo) {
  //html에 <li>만들기
  const li = document.createElement("li");
  // html에 <span>만들기
  const span = document.createElement("span");
  // html <li> <span></span> </li> 만들기
  li.appendChild(span);
  // text를 span에 넣음
  span.innerText = newToDo;
  // todo-list에 방금 만들 li를 집어넣기
  toDoList.appendChild(li);
}

//발생 event를 parameter로 받음
function handleToDoSubmit(event) {
  event.preventDefault();
  const newToDo = toDoInput.value;
  toDoInput.value = ""; // input을 비워주기 위함
  paintToDo(newToDo);
}
```

# _2022-06-03 FRI_

## 7.2 Deleting To Dos

- event.target // 이벤트가 발생 했을 때 해당 객체를 알 수 있음
  - event.target.parentElement // 해당 객체의 부모 태그를 알 수 있음

```
// click event발생시 deleteToDo func 호출
function deleteToDo(event) {
  // event를 불러와야 path를 통해 어떤 버튼이 클릭 됐는지 알 수 있음
  const li = event.target.parentElement;
  li.remove();
}
```

## 7.3 Saving To Dos

- todo-list에 나타난 텍스트를 저장하는 기능이 필요하다
- localstorage에 array저장 불가 // only text

- todo-list의 배열 생성
  - const toDos = []; // toDo에 들어오는 텍스트를 배열로 묶어 보관하기 위해 빈 array 생성해준다
- JSON.stringify( )
  - JS object나 array나 어떤 것이든 string으로 바꿔주는 기능

## 7.4~7.5 Loading To Dos part

- JSON.parse("")

  - string을 JS object로 만들어줌

- .forEach( funcName )
  - 배열 각각의 원소에 func실행 방법 //배열 순회
  - function funcName (item) { }
    - 배열의 현재 item의 정보를 알 수 있음
    - 더 좋은 방법은 arrow func을 이용하는방법 - .forEach( (item) => console.log(item));

## 7.6~7.8 Deleting To Dos

- To Do를 지울 때 마다 local storage를 업데이트 하지 않음 이걸 수정할거임
- 어떤 item을 지워야 할 지 알 수 없음
  - 화면에서는 어떤 element를 지워야 하는지 알고 있지만 DB에서는 어떤 item을 지워야 하는지 모름
  - text대신에 object로 만들어서 id 부여
    - Date.now()를 통해서 id에 랜덤 숫자를 부여
- array에서 어떤 item을 지울 때 실제로 item을 지우지 않음
  - 지우고 싶은 item을 제외하고 새로운 array를 다시 만듬
  - .filter(arg)를 이용하여 item을 제외 시킬 수 있음
    - arg : true를 retrun하는 func name
    - 만약 func가 false를 return한다면 그 배열의 원소를 새 array에 포함시키지 않음
    - array의 각 원소를 func의 arg로 호출함

```
function filterFunc (item){
return item !==3;
}

[1,2,3,4].filter(filterFunc)

filterFunc(1) = 1 // true
filterFunc(2) = 2 // true
filterFunc(3) 	   // false
filterFunc(4) = 4 // true
```

# _2022-06-05 SUN_

## 8.0 Geolocation

- 유저의 위치를 가져오는 방법
  -     navigator.geolocation.getCurrentPosition(arg1, arg2);
    - arg1 : 성공했을 때 func 실행
    - arg2 : 에러가 발생했을 때 func 실행

## 8.1 Weather API

- Current weather data를 API로 가져오기 - API 호출 후 latitude , longitude , API key 적을 것
- fetch( url ) // promise
  - JS가 URL 요청하기 위함
  - promise는 당장 일어나지 않고 시간이 걸린 뒤에 일어남 // 서버의 응답시간

```
fetch(url)
    .then((Response) => Response.json())
    .then((data) => {
      const weather = document.querySelector("#weather span:first-child");
      const city = document.querySelector("#weather span:last-child");
      city.innerText = data.name;
      weather.innerText = `${data.weather[0].main} / ${data.main.temp} °C `;
    });
```
