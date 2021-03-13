---
{"layout": "post", "categories": "Installation", "title": "install createreactapp", "feature-img": "assets/img/feature_img.png"}
---
### create-react-app 모듈
번거로운 webpack, balel 설정을 대신하여 facebook 에서 공식지원하는 틀 생성 도구
```
프로젝트명/
  README.md
  package.json
  node_modules/package.json 파일에는 명시되지 않은 로컬모듈들
  public/static 파일들
    index.html //create-react-app의 엔트리포인트(파일명 변경불가)
    favicon.ico
  src/
    index.js //create-react-app의 엔트리포인트(파일명 변경불가)
    App.js
    App.test.js
    App.css
    index.css
    logo.svg
```
react-scripts 명령어 : 사용자가 설정을 건들지 못하도록 package.json 과 webpack 설정을 캡슐화
```
package.json

"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject" //캡슐화 봉인해제
  }
```
src/index.js
```
import React from 'react'; //JSX 문법 사용 위해 필요. 모든 컴포넌트에 필수적

import ReactDOM from 'react-dom'; //엔트리포인트에서 최초렌더링을 위해. SSR도 지원.

import registerServiceWorker from './registerServiceWorker'; //자원을 cache하는 서비스
registerServiceWorker();

import './index.css'; //웹팩의 css-loader로 기본 css 파일 로드

import App from './App'; //컴포넌트명 App 로드

ReactDOM.render(<App />, document.getElementById('root')); //컴포넌트를 DOM 요소에 렌더링
```

### npm 으로 설치
프로젝트 생성시 node_modules/ 디렉터리에 react 모듈이 설치됨
```
npm install -g create-react-app
npm create react-app 프로젝트명
npx create-react-app 프로젝트명
cd 프로젝트명; npm start
```

### yarn 으로 설치
```
yarn create react-app 프로젝트명
cd 프로젝트명; yarn start
```

### 설치 후 실행
```
npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!
```

### 로컬에서 실행?
오프라인 상태에서 실행하니 안된다. 에러 로그를 보니 registry 에 요청하는데 왜 굳이?
```
0 info it worked if it ends with ok
1 verbose cli [
1 verbose cli   '/usr/local/bin/node',
1 verbose cli   '/usr/local/bin/npm',
1 verbose cli   'view',
1 verbose cli   'create-react-app',
1 verbose cli   'version'
1 verbose cli ]
2 info using npm@6.14.8
3 info using node@v14.15.0
4 verbose npm-session a37f03b9feb585b9
5 verbose type system
6 verbose stack FetchError: request to https://registry.npmjs.org/create-react-app failed, reason: getaddrinfo EAI_AGAIN registry.npmjs.org
6 verbose stack     at ClientRequest.<anonymous> (/usr/local/lib/node_modules/npm/node_modules/node-fetch-npm/src/index.js:68:14)
6 verbose stack     at ClientRequest.emit (events.js:315:20)
6 verbose stack     at TLSSocket.socketErrorListener (_http_client.js:469:9)
6 verbose stack     at TLSSocket.emit (events.js:315:20)
6 verbose stack     at emitErrorNT (internal/streams/destroy.js:106:8)
6 verbose stack     at emitErrorCloseNT (internal/streams/destroy.js:74:3)
6 verbose stack     at processTicksAndRejections (internal/process/task_queues.js:80:21)
7 verbose cwd /opt/gopath/treeconnectorPrj/hlfApp/frontend
8 verbose Linux 4.18.0-15-generic
9 verbose argv "/usr/local/bin/node" "/usr/local/bin/npm" "view" "create-react-app" "version"
10 verbose node v14.15.0
11 verbose npm  v6.14.8
12 error code EAI_AGAIN
13 error errno EAI_AGAIN
14 error request to https://registry.npmjs.org/create-react-app failed, reason: getaddrinfo EAI_AGAIN registry.npmjs.org
15 verbose exit [ 1, true ]
```

