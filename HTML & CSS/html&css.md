# 2022-06-18 SAT

- < !DOCTYPE html >

  - 브라우저에게 text파일이 아닌 html이라고 알려주기 위함

- 웹페이지를 만들기 위한 설정

```html
<html></html>
태그안에서 사용해야함
<head></head> 웹페이지의 환경 설정 // 브라우저상에 보이지 않음
<body></body>
웹페이지의 컨텐츠 설정
```

```html
<head tag>
// <title> 구글 검색시 브라우저에 보이는 내용
<meta> 구글 검색시 웹페이지 설명 칸
<meta charset ="utf-8" /> // 글자가 깨져 보이는것을 방지
<html lang="kr"> // 검색엔진에게 이 웹페이지가 무엇으로 이루어져 있는지 알려줌

<label>과 <input>은 같이 작성해야함
<label> => for
<input> => id
// 둘이 들어가는 내용은 똑같이 작성해야함

id는 body안의 어떤 태그에든 넣을 수 있는 attribute
// id는 고유식별자 => 태그 하나당 하나의 id unique

<div> </div>
// 웹페이지를 분할 => 박스
// 기본적으로 박스는 양 옆에 있을 수 없음
// 의미단위로 나눠줌

//시맨틱 태그
<header> </header>
<main> </main>
<footer> </footer>
=> <div id="header"> </div> 방식과 같지만 header 태그로 작성 해주는게 더 좋음

<span> 짧은 text

<p> 긴 문단

<tagname attrName="value">anything</tagname>
```

# 2022-06-20 MON

- CSS 코드 작성 방법

```html
selector {property} // html을 가리키고 속성 적용 from TOP to BOTTOM // cascading
위에서 부터 아래로 적용
```

- BOX
  - 어떠한 박스를 만들던지 박스 옆에 또 다른 박스 X
  - p도 옆에 아무것도 올 수 없음
  - 다른요소 옆에 X => block
  - 다른요소 옆에 O => inline ( in the same line )
  - 대부분의 box들은 block => inline종류를 알도록
  - inline => span / a / image
  - display 속성을 설정하면 inline과 block으로 변경 가능
  - inline은 높이와 너비가 없음
  - margin : box의 border의 바깥 공간
  - margin : 10px 20px; 상하 10 좌우 20
  - margin : 10px 20px 5px 15px; // 위쪽 오른쪽 아래 왼쪽
  - collapsing margins : 위아래에서 하나의 박스로 취급하는 현상 // 두 박스의 경계가 같을때 하나의 마진으로 처리
  - pading : box의 border의 안쪽 공간
  - border : box의 경계 // inline과 box모두 적용
- inline의 특징
  : 높이와 너비가 없음 // 따라서 margin은 좌우 padding 사방

- Classes
  : id는 태그당 하나의 고유값을 가지지만 classes는 여러태그를 같은 이름으로 작성하고 싶을 때 사용
  - don't unique
  - 여러개의 클래스를 가질 수 있음

```html
<tag class="classname classname2 classname3 .. "></tag>
=> .classname 사용
<tag id="idname"></tag>
=>#idname 사용
```

- inline-block
  : display : inline-block을 사용하면 box들이 양 옆에 놓일 수 있음
  - 반응형 디자인을 지원하지 않음!