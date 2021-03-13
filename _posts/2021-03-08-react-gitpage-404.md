---
{"layout": "post", "categories": "TroubleShooting", "title": "react-gitpage-404", "feature-img": "assets/img/feature_img.png"}
---
## 증상
react로 빌드해서 배포했는데 index.html에서 react 컴포넌트가 안뜸
![gitpage_only_show_index](/images/gitpage_only_show_index.png)

package.json에 이렇게 설정했다면
```
"homepage": "https://homoacademycus.github.io/ip-calculator",
```
빌드된 index.html 에서 이렇게 나와야 하는데
```
<script src="/ip-calculator/static/js/2.39c7dd06.chunk.js"></script>
```

나의 빌드된 index.html 에서는 하위프로젝트 경로가 안잡힘
```
<script src="/static/js/main.c5dffee1.chunk.js"></script>
```

개발자도구로 network 요청 상태를 보니
![gitpage_react_network](/images/gitpage_react_network.png)
react 로딩에 필요한 파일들을 서버경로에서 못찾아서 404 에러를 내고 있음
```
GET 200 username.github.io /ip-calculator/
GET 404 username.github.io main.c5dffee1.chunk.js
```

## 원인
```
github page는 static file지원만 가능합니다
말하자면 CDN같은거죠. SPA가  로컬에선 잘 돌아갑니다, 왜냐면  webpack-dev-server같은 것들이 웹서버 역할을 하거든요, 이게 웹상에서 정상적으로 작동하려면 웹서버가 있어야 하고, 404가 전부 index.html로 redirect되어야만 합니다. github page는 웹서버(apache, nginx)가 없어 이 redirect를 고의로 지원하지 않습니다.  

React 앱에서 라우팅이 제대로 이루어지려면 모든 요청에 대하여 index.html을 반환해주어야 합니다. 그런데 Github Page로 배포하면 그것이 불가능합니다. 앞서 서버사이드 렌더링을 사용할 수 없는 것과 같은 이유로 말이죠. / 이외의 경로로 접근한다면 서버 입장에서는 식별할 수 없는 경로이므로, 404 Not Found 페이지를 반환해줍니다.
```

## 해결
1. 브라우저가 경로를 못찾나 싶어 index.html 에서 다음을 추가
```
<base href="https://homoacademycus.github.io/ip-calculator" />
```

2. 리액트 라우터의 basename에 하위 프로젝트경로 추가
```
<BrowserRouter basename={process.env.PUBLIC_URL}>
```
그런데 echo $PUBLIC_URL 치니 아무것도 안나와서 그냥 통째로 박음
```
<BrowserRouter basename="/ip-calculator">
```

3. 혹시 몰라 404.html과 index.html 에 리다이렉트하는 스크립트도 추가

4. 이건 바벨이 빌드할 때 문제인 것 같아서 그냥 빌드된 index.html을 수정함
```
<script src="/프로젝트폴더명/static/js/main.c5dffee1.chunk.js"></script>
```

해결.


