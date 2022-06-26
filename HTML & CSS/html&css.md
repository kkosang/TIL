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

# 2022-06-25 SAT

- inline-block
  : display : inline-block을 사용하면 box들이 양 옆에 놓일 수 있음
  // 반응형 디자인을 지원하지 않음!

- flexbox
  : 박스들을 원하는곳에 놓을 수 있음

  - rule
    - 1. 자식 엘리먼트에는 어떠한것도 적지 X // 부모 엘리먼트에만 말함 //부모에게 명시 display:flex;
    - 2. justify-content: flex-start; 가 기본값
    - 3. main axis / cross axis ( 수평, 수직 축) 메인축, 교차축
      - justifiy-content ( main axis에 적용)
      - aline-items ( croos axis에 적용)
      - 기본값: 주축= 수평 / 교차축= 수직
      - align-items을 이용하기 위해서는 부모의 height를 지정해줘야 하는데 이때 100vh를 이용하여 (viewpoint height) 반응형 웹을 만들어 줄 수 있음
      - main axis와 cross axis를 바꾸기 위해서는 flex-direction column으로 설정하면 바뀜
      - flex-direction 은 기본 값으로 row를 가짐

- position
  : 레이아웃 보다는 위치를 아주 조금씩 옮길 때 사용
  - position: fixed // 처음 레이아웃한 위치에서 고정
  - 모든 레이어보다 가장 위에 있음
  - top: px;을 설정해주면 다른 레이어로 변경 됨 // 즉 box끼리 겹칠 수 있음
  - static : 레이아웃이 처음 위치한 곳에 설정 (디폴트)
  - relative : 처음위치에서 아주 조금씩 옮기기 위함
  - absolute : 가장 가까운 relative부모 기준으로 옮겨줌
    - 부모가 relative가 아니면 그 다음 부모가 relative인지 확인 전부 relative가 아닐경우 body가 부모가 됨
    - 따라서 제대로 적용하기 위해서는 작성하고자 하는 클래스 부모에 relative를 설정해 준 뒤 사용

# _2022-06-26 SUN_

- pesudo selectors
  : 특별하게 지정할 수 있음

  - tagname : attribute{ }
  - id나 class를 만드는것보다 훨씬 좋은 코드
  - first-child() / last-child() / nth-child()
  - nth-child(even/odd/2n+1 ... 모든수식

- Combinators ( 바로 밑 자식 > // 바로 형제 + )
  : 부모와 자식으로 지정함

  - 부모tagname 자식tagname { }
  - 부모 밑에 같은 태그의 여러 자식이 있을 경우
    - 부모tagname > 자식tagname을 하면 부모 바로 밑 자식에게 적용 할 수 있음
  - 형제태그
    - 형제 tagname + 대상 tagname을 하면 형제태그 다음에 오는 대상태그에 적용

- pesudo selectors part two

  - 형제 바로 뒤에 오지 않을때
    - 형제 ~ 대상을 하면 형제태그 바로 다음이 아니여도 적용 가능 _여러개의 형제에도 적용 가능_
  - 포함하고 있을 때
    - input[placeholder~="name"] { } // name을 포함하고 있으면 적용

- Colors and Variables
  : 색상 표현과 변수 사용
- CSS에서 색상은 3가지 방식으로 표현 됨
  - 1. 16진수 #FE3O03 // #fff 블랙 #000화이트
  - 2. RGB(252,206,0); // rgba a=> 투명도 0~1
  - 3. 변수 :root { } // 모든 document의 출발점
    - 변수 사용시 var(--변수명)
