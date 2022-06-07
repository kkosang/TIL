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
