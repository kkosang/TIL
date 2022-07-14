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

# _2022-07-01 FRI_

## <em>5.10 Recap</em>

- iteration
  - array의 모든 element에 대해 특정 행동을 취할 때 사용
  - each x in y의 형태로 사용
    - y가 우리가 가지고 있는 array
  - else
    - 배열안에 element가 없을 경우 사용
- mixin
  - 다른 데이터를 포함하면서 똑같은 형태의 html을 반복할 때 사용
  - each x in y의 형태
    - y는 우리가 만든 object
    - x는 object 각각의 item에 접근

## <em>6.0~6.1 Array Database </em>

- back end에 데이터를 보내는 방법
  - data를 post한 후에 database에 추가
- #{ } 방식은 attribute에서 사용불가
  - 따라서 `${}` // JS방식 사용

```javascript
 a(href=`/videos/${video.id}`)=video.title
```

- ternary operator
  - #{video.views === 1 ? "view" : "views"}
- absolute와 relative url
  - url에 "/aaa" // absolute url
    - root 경로 + /aaa로 이동
  - url에 "aaa" // relative url
    - 이전 경로 + 현재경로를 /aaa로 바꿔줌 // 끝 부분 변경

## <em>6.2~6.3 Edit Video</em>

- form(action="")
  - data를 어디로 보낼지 정함
  - 값으로 url을 가짐
- method
  - form과 back end사이의 정보 전송에 관한 방식
  - 기본값으로 method는 GET
    - 주로 검색할 때 사용
    - form의 정보가 url에 들어감
  - method POST
    - 파일을 보내거나 , DB의 값을 바꾸고 싶을 때
- get request와 post request의 차이점
  - get form을 화면에 보여줌
  - post form의 변경사항을 저장해줌
- res.redirect(); // url
  - 브라우저가 자동으로 이동하도록 함
- express.urlencoded([options])
  - application이 form의 body를 이해 하도록 해줌
  - app.use(express.urlencoded({ extended: true })); - middleware를 route 사용하기 전에 사용
    - express app이 form의 value들을 이해할 수 있도록 하고 JS형식으로 변형 시켜줌
- req.body

# _2022-07-03 SUN_

## <em> 6.4 Recap </em>

- req.body에서 내용을 읽어 오려면 모든 input에 name을 넣어줘야함

## <em> 6.5~6.6 More Practice </em>

- Make getUpload, postUpload controller
- What is the thing that execute a controller ?
  - route // videoRouter
- videoRouter.get("/upload", getUpload);
  - import getUpload
- videoRouter.post("/upload",postUpload);
- Make link : /upload
  - base.pug
    - a(href="/videos/upload") Upload Video
- Make pug : upload.pug
  - extends base.pug
- Make form
  - block content  
    form(method="POST")
    input(placeholder="Title", required,type="text" name="title")
    input(type="submit", value="Upload Video")
  - 현재의 url로 post request를 보냄
    - action을 이용하여 다른 url로 전송가능
- Get Data
  - req.body
    - input의 name이 없다면 비어 있음
- Push Data
  - const newVideo = { title: req.body.title, id: videos.length+1};
  - videos.push(newVideo)

## <em>6.7 Introduction to MongoDB</em>

- document-based( 문서 기반 )
  - 보통 DB는 sql-based( 행 기반 )
  - 저장물은 JSON-like-document

## <em>6.8 Connecting to Mongo</em>

- mongoose
  - node.js와 mongoDB를 이어줌 // package
  - mongoDB와 대화 할 수 있게 해줌
  - npm i mongoose
- mongod: MongoDB 시스템의 기본 데몬 프로세서 (서버와 같은 느낌)
- mongo: MongoDB에 대한 쉘 인터페이스 (클라이언트 같은 느낌)
- 그래서 mongod로 서버를 키고 -> mongo로 인터페이스를 실행하여 mongoDB와 소통한다
- Mongo연결
  - db.js 생성
  - import mongoose
  - mongoose.connect(" mongo url/nameofyourdb " ) // mongodb에 새로운 db 만들기
- 서버에서 db파일 사용
  - 파일 자체를 import
  - import "./db";
  - import되는 순간 자동적으로 실행됨
- db의 연결 성공여부나 에러 출력

```javascript
const handleOpen = () => console.log("Connected to DB👌");
db.on("error", (error) => console.log("DB Error", error));
db.once("open", handleOpen);
//	- on : 여러번 계속 발생할 수 있음
//	- once : 오로지 한번만 발생
```

# _2022-07-08 FRI_

## <em>6.9 CRUD Introduction</em>

- Create
- Read
- Update
- Delete
- DB에게 data가 어떻게 생겼는지 알려주기 위해 model을 만듬

## <em>6.10 Video Model</em>

- import mongoose

```javascript
import mongoose from "mongoose";
```

- model schema
  - 데이터의 형식 지정 // shape of the data

```javascript
const videoSchema = new mongoose.Schema({
  title: String,
  description: String,
  createdAt: Date,
  hashtags: [{ type: String }],
  meta: {
    views: Number,
    rating: Number,
  },
});
```

- create model

```javascript
const movieModel = mongoose.model("Video", videoSchema);
// name of the model, name of the schema
```

- export default
  - 다른 파일에 video를 import 하기 위함
- init.js파일에 video파일 import
  - import "./models/Video"; // db를 import 한 후에 해야 함
- db를 mongoose와 연결시켜 video model을 인식 시킴

## <em>6.11~6.12 Our First Query</em>

- server.js
  - server 관련 코드만 처리
-     init.js
  - app에 필요한 모든 것들을 import 시키는 역할
- mongoose model 사용방법
  - Query func // https://mongoosejs.com/docs/queries.html
    - Model.find() // 두 가지 사용법
      - callback 활용
        - js에서 기다림을 표현 하는 하나의 방법 - 실행과 동시에 적용되지 않음
        - configuration과 호출할 func필요

```javascript
Video.find({}, (error, videos) => {
  console.log("errors", error);
  console.log("videos", videos);
});
// {}는 search terms을 뜻 함, 비어 있는 경우 모든 형식을 찾음
// err와 docs라는 signature를 가짐
```

- promise 활용

# _2022-07-14 THU_

## <em>6.13 Async Await </em>

- promise
  - callback의 최신 버전
  - callback과의 차이점
    - await를 find 앞에 적으면 find는 callback을 필요로 하지 않는다고 알게 됨
    - await가 database를 기다려줌
  - 규칙상 await는 func 안에서만 사용 가능
    - 해당 func가 asynchronous 일 때만 가능

```javascript
export const home = async (req, res) => {
  try {
    const videos = await Video.find({});
    return res.render("home", { pageTitle: "Home", videos: [] });
  } catch {
    return res.render("server-error");
  }
};
// 코드 실행중 오류 발생시 await내 출력 값을 출력하지 않고 catch의 에러 출력코드 실행
```

## <em>6.14 Returns and Renders</em>

- return이 아니라 실행되는 func들에 집중
  - render뒤에 redirect 같은 func은 실행되지 않음

## <em>6.15~6.16 Creating a Video</em>

- document를 만들어 줘야함
  - 데이터를 가진 비디오
  - document를 db에 저장해야함
- Data의 형태 미리 지정
  - 데이터 타입의 유효성 검사를 도와줌
  - 올바른 정보가 아니라면 자동으로 doc data에 포함되지 않음
- .save()
  - mongoose model에서 사용
  - promise를 return 해줌 // save 작업이 끝날 때 까지 기다려야함
  - save는 promise를 return하고 이걸 await하면 document가 return됨
- mongo console
  - show dbs
    - db들을 보여줌
  - use nameofdb
  - show collections
    - document들의 묶음을 보여줌
- save방식과 create방식

```javascript
//save방식
const video = new Video({
  title,
  description,
  createdAt: Date.now(),
  hashtags: hashtags.split(",").map((word) => `#${word}`),
  meta: {
    views: 0,
    rating: 0,
  },
});
await video.save();
```

```javascript
//create방식
await Video.create({
  title,
  description,
  createdAt: Date.now(),
  hashtags: hashtags.split(",").map((word) => `#${word}`),
  meta: {
    views: 0,
    rating: 0,
  },
});
```

# _2022-07-15 FRI_

## <em> 6.17 Exceptions and Validation</em>

```javascript
try {
  // 오류가 없을 때 실행
  await Video.create({});
} catch (error) {
  // 오류가 발생하면
  return res.render("upload", {
    // upload page에 errorMessage 렌더링
    pageTitle: "Upload Video",
    errorMessage: error._message,
  });
}
```

## <em> 6.18 More Schema </em>

- String
  - trim
    - 단어 사이에 있는 하나의 공백을 제외하고 모든 공백을 제거
  - min/maxLength
    - 단어의 최소 길이와 최대 길이를 지정해줌
    - 사용자와 해당 코드를 연결
      - form에서 Min과 Max 설정
      - 하나는 사용자를 위해 다른 하나는 DB를 위해 // 일종의 보안 구축

## <em> 6.19 Video Detail </em>

- regular expression
  - Can be a 24 byte hex string
  - /[0-9a-f]{24}
- findOne
  - 요청하는 모든 condition을 적용시켜줌
- findById
  - id로 영상을 찾을 수 있음

## <em> 6.20~6.22 Edit Video </em>

- 비디오가 존재 하지 않는 경우
  - null인경우 처리

```javascript
if (video === null) {
  // 에러체크를 먼저 할 것
  return res.render("404", { pageTitle: "Video not found." });
}
return res.render("watch", { pageTitle: video.title, video });
```

- 주어진 array를 string으로 format하기
  - .join()
- 주어진 해쉬태그가 무엇으로 시작하는지 파악
  - word.startsWith("#")
- Id로 video를 찾고 update하기
  - findByIdAndUpdate( )
    - 2개의 argument
    - 업데이트 하고자 하는 영상의 ID
    - 업데이트 할 정보 혹은 내용
- 존재하는지 파악 하기
  - .exists( )
    - argument로 filter
    - 존재시 return true
- object가 저장 되기 전에 처리 // 중복 파악등
  - middleware사용

## <em> 6.23 Middlewares </em>

- mongoose middleware
  - 반드시 model이 생성되기 전에 만들어야 함

```javascript
videoSchema.pre("save", async function () {
  //save 되기 전에 실행
});
```

- hashtags array의 첫 element 포맷

```javascript
this.hashtags = this.hashtags[0]
  .split(",")
  .map((word) => (word.startsWith("#") ? word : `#${word}`));
```

- mongo사용

```mongo
1. 몽고 사용하기

> mongo

2. 내가 가진 db 보기

> show dbs

3. 현재 사용 중인 db 확인

> db

4. 사용할 db 선택하기

> use dbName
(현재 수업에서는 `use wetube`)

5. db 컬렉션 보기

> show collections

6. db 컬렉션 안에 documents 보기
>
 db.collectionName.find()
(현재 수업에서는 `db.videos.find()`)

7. db 컬렉션 안에 documents 내용 모두 제거하기

> db.collectionName.remove({})
(현재 수업에서는 `db.videos.remove({})`)
```
