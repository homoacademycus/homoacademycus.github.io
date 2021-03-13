---
{"layout": "post", "categories": "Installation", "title": "react-gitpage", "feature-img": "assets/img/feature_img.png"}
---
1. gh-pages 설치
```
npm install --save-dev gh-pages
```

2. package.json 설정
```
{
  "homepage": "https://username.github.io/repoName",
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
    //"deploy": "npm run build&&gh-pages -d build"
  },
}
```

3. App.js의 react-router에 basename 경로 설정
```
<BrowserRouter basename="/myrepo">
또는
<BrowserRouter basename={process.env.PUBLIC_URL}>
```

4. 빌드된 index.html의 src에서 bundle.js 파일 경로에 프로젝트경로 추가
```
/repoName/build/bundle.js
```

5. 배포
```
npm run deploy
git add *
git commit -m "publish it to github pages"
git push
```

* .nojekyll :  깃허브 페이지의 Jekyll 사용 제거
