---
{"layout": "post", "categories": "Installation", "title": "install react", "feature-img": "assets/img/feature_img.png"}
---
### 모듈만 설치해서 import
```
https://cdnjs.cloudflare.com/ajax/libs/react/버전/react.js, react-dom.js

https://unpkg.com/react@16/umd/react.development.js
https://unpkg.com/react-dom@16/umd/react-dom.development.js
```

### babel
최신 버전의 문법으로 작성된 js 코드를 ES5 형태로 변환(for 구버전 브라우저, JSX 문법)
preset, plugin을 통해 여러 문법(새로 만든 문법도)을 지원
```
https://unpkg.com/babel-standalone@6.26.0/babel.js
https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0-alpha1/JSXTransformer.js
https://cdnjs.cloudflare.com/ajax/libs/babel-core/버전/browser.min.js
```
자바스크립트 태그를 jsx 를 위한 바벨 태그로 바꿔야
```
<script type="text/javascript"></script>
<script type="text/babel"></script>
```

npm 또는 npx, yarn 으로 실행
```
create-react-app 프로젝트명 //최신 버전
create react-app 프로젝트명 //옛날 버전
```
registry에 요청해야 해서 온라인이어야 함


