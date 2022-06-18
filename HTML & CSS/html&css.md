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
