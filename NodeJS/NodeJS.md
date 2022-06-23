# _2022-06-07 MON_

## <em>1.3 What is Node JS </em>

- 웹 브라우저 밖에서 사용할 수 있는 JS
- Ryan Dahi이 개발함

## <em>1.4 What is NPM</em>

- JS를 위한 패키지 매니저
- nodeJS와 상호작용
- cf) yarn은 페이스북이 만든 패키지 매니저

## <em>2.0 First Node JS Project</em>

- nodeJS 프로젝트를 만들 때 가장 먼저 만들어야 할 파일 // package.json
  - json은 프로그래머가 파일에 정보를 저장하기 위해 만든 방식 중 하나임
  - nodeJS인 경우 파일에 정보를 입력하기 위해서 파일의 이름은 package.json이어야 함

## <em>2.1 Installing Express</em>

- js파일을 실행하는 방법으로는 2가지가 있다
- 1 .터미널에 node index.js 실행
- 2 . npm을 이용하는 방법

  - package.json의 scripts의 이용 // 코드 실행
  - npm run scripts의 name

- express 사용(npm)
  - npm i(=install) express
  - node_modules 폴더 // npm으로 설치한 모든 패키지가 저장
  - package.json의 dependencies // 패키지를 사용하기 위해 필요한 모듈들을 말함

## <em>2.2 Understanding Dependencies</em>

- npm i

  - package.json의 "dependencies"를 작성하면 알아서 npm이 설치해줌
  - 누구나 빠르게 필요한 패키지를 다운 받을 수 있음
  - package.json을 닫고 install하는 습관 // npm이 자동으로 package.json을 수정하기 때문

- package-lock.json
  - 패키지들을 안전하게 관리해줌
  - 패키지가 수정 됐는지 해시값으로 체크해줌
  - 똑같은 버전의 모듈 설치

## <em>2.3 The Tower of Babel</em>

- Babel
  - JS compiler
  - NodeJS가 이해하지 못하는 최신 JS를 Babel을 통해 compile
- "dependencies"
  - 프로젝트를 실행하기 위해 필요한 dependencies
- "devDependencies"
  - 프로젝트를 실행하기 위해 개발자에게 필요한 dependencies
  - npm install --save-dev @babel/core // --save-dev는 babel을 설치 할 때 "devDependencies"에 저장하기 위함
- babel.config.json파일
  - babel을 설정해주기 위한 파일
  - babel이 babel.config.json파일을 찾아서 설정함

## <em>2.4 Nodemon</em>

- scripts를 이용해 babel 실행

  - npm install @babel/node --save-dev // babel/node 설치
  - "babel-node index.js" // 최신 문법 실행

- nodemon
  - 파일이 수정되는걸 감시 해주는 패키지
  - 파일이 명령어 필요 없이 알아서 재시작을 해줌
  - scripts에 nodemon 추가
    - "nodemon --exec babel-node index.js" // index.js를 수정할 때 마다 최신코드로 실행
    - Ctrl + c로 nodemon 종료가능

# _2022-06-08 WED_

## <em>3.0 Your First Server</em>

```javascript
import express from "express"; // "express"라는 node_modules안에 있는 package를 express라는 이름으로 import

const app = express(); // express func를 사용하여 express application생성

const handleListening = () => console.log("Server listening on port 3188");

app.listen(3188, handleListening); // port번호와 callback함수
```

- localhost:portNumber로 서버에 접속 할 수 있음

## <em>3.1~3.2 GET Requests</em>

- Cannot GET /
  - / 서버의 root, 첫 페이지
  - GET은 HTTP method
    - 우리와 서버가 소통 or 서버가 서로 소통하는 방법
    - 가장 안정적이고, 오래되고 처음 사용된 방식
    - 브라우저가 웹사이트를 request하고 페이지를 가져다 줌
    - 여러 종류의 request중 하나
- app.get("/",callbackfunc)
  - 누군가 home으로 get request를 보낸다면, callbackfunc 호출

## <em>3.3 Responses</em>

```javascript
const handleHome = (req, res) => {
  console.log(req);
}; // parameter1 : request object , parameter2 : response object / 반드시 parameter 2개가 필요
```

- request는 브라우저가 뭔가를 요청 함
  - 쿠키나 method 같은 정보를 얻을 수 있음 // 이 경우엔 GET method
- return res.end();
  - request를 종료 시키는 여러 방법 중 하나

## <em>3.4 Recap</em>

- request를 받으면 response을 받을 때 까지 실행
- express( )
  - Application
  - Request
  - Response

## <em>3.5~3.6 Middlewares</em>

- 브라우저가 request한 후 서버에서 response하기 전에 그 사이에 middleware가 존재
- response하지 않고 다음 func에게 넘기는 func임
- middleware는 3개의 parameter를 가짐
  - par1 : request
  - par2 : response
  - par3 : next
- 모든 controller는 middleware가 될 수 있다 // controller가 next함수를 호출하면 middleware
- .get( )

  - par1 : path
  - par2~n : handlers

- .use( )

  - global middleware를 만들 수 있게 해줌 // 어느 url에도 작동

  - middleware는 순서가 중요함

# _2022-06-09 THU_

## <em>3.7 Setup Recap</em>

- package.json
  - text 파일
- script
  - scripts entry 생성하고 script를 입력하면 npm run scriptName을 사용
- dependencies
  - 프로젝트가 실행되기 위해 필요함
- devDependencies
  - 좀 더 편리한 개발환경을 위해
  - nodemon
    - 파일의 변화가 생기면 commend 재시작
  - balbel
    - ES6를 사용하기 위해
    - ES6 -> 평범한 node.js 방식 -> node.js 서버 작동
    - babel.config.json 파일 설정 // plugin추가

## <em>3.8 Servers Recap</em>

- server
  - 서버는 항상 켜져 있고, 인터넷에 연결 돼 있으면서 req를 listen하고 있음
  - request는 브라우저를 통해 웹사이트에게 하는 모든 상호작용
- import express
- create app variable
  - const app = express( );
- request listen
  - app.listen(PORT, handleListening);
  - 서버가 PORT 번호만 listen
- handleListening
  - listening이 시작되면 호출되는 함수
- 브라우저가 서버에게 페이지를 request

## <em>3.9 Controllers Recap</em>

- controller
  - 모든 controller에는 request와 response가 존재 + next
- 모든것들이 route를 만들고 그 route를 다룸 // controllers로
- arrow function은 return을 포함한다
  - const handleHome = (req,res) => res.end()
  - const handleHome = (req,res) => { return res.end() } - 둘이 같음

## <em>3.10 Middleware Recap</em>

- request와 response 중간에 있는 software
- parameter로 req, res, next를 가짐
- 요청을 응답하거나 next로 다음 함수에게 넘겨줌
- 관습적으로, 응답을 해주는 마지막 controller에는 next를 안씀
- middleware를 global하게 사용하고 싶으면 app.use( )를 이용할것 // 단 , 순서 중요함

# _2022-06-12 SUN_

## 3.11 External Middlewares

- morgan
  - node.js용 request logger middleware를 return 해줌
  - cf) https://www.npmjs.com/package/morgan
  - morgan("dev")
    - GET, URL, status code, 응답시간

## <em>4.0 What are Routers?</em>

- Router
  - url의 시작부분
  - controller와 url의 관리를 쉽게 해줌
  - URL들을 그룹화 시킴
  - 글로벌 라우터 / 유저 라우터 / 비디오 라우터 처럼 그룹화

## <em>4.1 Making Our Routers </em>

- url을 깔끔하게 만들면 마케팅하는데도 도움이 됨
- app.get("/", homeRouter )
  - 사용자가 GET요청을 보내면 요청이 homeRouter로 라우팅됨
- const homeRouter = express.Router()
  - 다음과 같이 homeRouter라는 상수 변수를 생성함
- const handleReq = (req, res) => res.send("Do something");
  - 다음과 같이 핸들러 함수 생성
- routerOne.get("/",handleReq);
  - 라우터를 핸들러에 연결
- 사용자가 URL "/"을 GET하도록 요청하면 사용자는 express앱에서 라우터 homeRouter, 핸들러 함수 handleReq으로 라우팅 됨

## <em>4.2 Cleaning the Code</em>

- JS파일은 각자 독립적임 // 하나의 모듈
- import를 하기전에 export를 해줘야 함
  - export default globalRouter;
  - 파일 전체를 export한게 아니라 globalRouter(변수)만 export

## <em>4.3 Exports </em>

- 컨트롤러는 함수
- 라우터는 그 함수를 사용하는 입장
- 따라서 둘이 같은 곳에 두지 말것
- export default로는 한가지 밖에 못함
- 여러개를 export 하기 위한 방법

```javascript
export const trending = (req, res) => res.send("Home Page Videos");
export const watch = (req, res) => res.send("Watch");
export const edit = (req, res) => res.send("Edit");
```

- import를 하기 위한 방법
  - object사용

```javascript
import { edit, watch } from "../controllers/videoController";
```

- export default 와 export const의 차이점 - import 할 때 default는 사용자가 원하는 이름을 사용할 수 있지만
  const는 실제 이름을 그대로 써야 함

# _2022-06-13 MON_

## <em>4.4 Router Recap</em>

- 공통 시작부분을 기반으로 url을 정리해주는 방법

## <em>4.5 Architecture Recap</em>

- 변수를 다른 파일에서 가져옴
- 한가지만 공유 할 때
  - export default
  - import시 이름을 사용자 마음대로 정의 할 수 있음
- 한가지 이상을 공유 할 때
  - export
  - import시 이름을 오브젝트안에 같은 이름을 사용해야 함

## <em>4.6 Planning Routes</em>

- 각 기능에 따라 Router와 Controller 연결

# _2022-06-16 THU_

## <em>4.7~4.8 URL Parameters</em>

- /:
  - parameter
  - url안에 변수를 포함 시킬 수 있음
  - express한테 변수라는고 알려줌
  - 변수의 이름은 아무거나 써도 상관 없음

```javascript
videoRouter.get("/upload", upload);
videoRouter.get("/:id", see);
videoRouter.get("/:id/edit", edit);
```

    - upload와 see의 순서 중요
    - 위에서부터 코드를 읽기 때문에 upload가 :id밑으로 가게되면 express가 uplaoad를 id로 인식하게 됨

- express 정규식
  - 문자열로부터 특정 정보를 추출해내는 방법
  - 숫자만 선택하는 방법
    - (\d+) // digit

## <em>5.0 Returning HTML</em>

- HTML을 return하는데 2가지 옵션이 있음
  - 1.  그냥 HTML의 문자열을 써서 보내는 방법 // 좋은 방법이 아님 / 긴급상황에 가끔 필요
  - 2.  PUG사용 // 코드 복붙 할 필요 없어짐 // Template Engine // html helper

## <em>5.1 Configuring Pug</em>

- npm i pug // pug 설치
- app.set("view engine", "pug"); // view engine으로 pug설정
- pug 파일 생성
  - views폴더에서 express가 뷰를 찾음
  - process.cwd() + '/views' // current working directory
- 작동 방식
  - 파일을 pug에게 보내고 pug가 파일을 렌더링해서 평범한 html로 변환
- cwd()는 서버를 기동하는 파일의 위치에 따라 결정됨 // 어디서 노드를 부르고 있는지에 따라 결정
  - node.js를 실행하는 디렉토리
  - package.json
- app.set("views", process.cwd() + "/src/views"); // view 설정 바꾸기

# _2022-06-21 TUE_

## <em>5.2 Partials </em>

- 변경사항이 생기면 모든 페이지에서 수정 할 필요 없이 partials폴더 만들고 그 안에 반복되는 내용을 파일로 만듬
- include partials/footer.pug와 같이 파일을 include 해주기만 하면 됨
- pug 사용 하는 이유
  - 깔끔한 html 작성 가능
  - html에 JS를 포함 시킬 수 있음
  - 반복하지 않고 파일로 모든 템플릿을 업데이트 할 수 있음

## <em>5.3 Extending Templates</em>

- inheritance
  - 일종의 base개념
  - 레이아웃의 베이스, HTML의 베이스
- extends
  - html의 베이스를 가질 수 있게 해줌 // 베이스가 되는 파일을 가져다 그대로 씀
  - 파일을 확장하기 위해
  - // block을 이용하여 원하는 부분만 수정 가능
  - 확장하고 싶은 파일에 가서 // extends 파일명.pug
- block
  - 템플릿 안에 내용을 넣을 수 있음
  - 템플릿의 창문 같은느낌 ( 공간 마련 )
  - 블록을 만드는 방법
    - block blockName
      - 수정내용

## <em>5.4 Variables to Templates</em>

- 템플릿에 변수를 사용하기
  - #{VariableName} // JS의 변수를 사용하기 위함
- 템플릿으로 변수 보내기
  - 누가 템플릿을 렌더링하고 있는지 파악 // 컨트롤러

```javascript
export const trending = (req, res) =>
  res.render("home", { pageTitle: "Comes from your controller" });
// render함수는 2가지 parameter를 가짐 / view와 템플릿에 보낼 변수들
```

# _2022-06-23 THU_

## <em> 5.5 Recap </em>

## <em>5.6 MVP Styles</em>

- MVP.css // middleware
  - HTML 태그에 몇가지 기본 스타일을 입혀줌

```css
link(rel="stylesheet" href="http://unpkg.com/mvp.css")를 추가하여 사용
```

## <em>5.7 Conditionals</em>

- = variable을 쓰면 #{variable}과 같음
  - #{variable}은 변수와 text를 같이 사용할 때
  - = variable은 오직 변수만 사용할 때

## <em>5.8 Iteration</em>

- 리스트, 즉 array가 필요함
- elements의 list를 보여줌
- each 보여주고 싶은 variable 이름

```javascript
each video in videos
            li=video
// videos array안의 각 element에 대해서 list item을 만들어서 그 안에 넣어줌
// video는 loop상의 현재 값이라 이름 아무렇게나 해도 상관 없음
// videos는 controller 부분의 이름과 같아야 함
// 통상적으로 each 단수 in 복수 형태로 사용
```

- error
  - Cannot read property 'length' of undefined
    // each X in Y를 할 때 Y가 undefined이라는 뜻

## <em>5.9 Mixins</em>

- 데이터를 받을 수 있는 partial을 뜻함
- 같은 형태를 지니지만 서로 다른 데이터를 가져야 할 때 사용
- mixin파일

```pug
mixin video(info)
  div
      h4=info.title
           ul
                li  #{info.rating}/5.
                li #{info.comments} comments.
                li Posted #{info.createdAt}.
                li #{info.views} views.
```

- mixin사용

```pug
include mixins/video
each item in videos
          +video(item)
        else
            li Sorry nothing found.
```
