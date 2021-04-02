---
{"layout": "post", "categories": "Installation", "title": "forever nodemon", "feature-img": "assets/img/feature_img.png"}
---
### forever
소스 파일의 내용이 바뀌면 자동으로 node를 재시작
* -w 옵션 : 감시 시작
```
$ npm install -g --save-dev forever
$ forever start -w ./app.js
```
* -l 옵션 : 로그를 파일로 저장, -a 옵션 : 로그를 덧붙이기
```
forever start -l $PWD/logs/example.log -a -w ./app.js
```
* 감시에서 제외할 파일과 경로를 지정
```
.foreverignore

*.log
**/.git/**
**/upload/**
**/backup/**
**/public/**
```
꼭 .foreverignore 파일에서 로그파일을 제외를 시키지 않으면
로그가 파일에 저장될 때마다 forever가 node를 재시작 시킵니다.
* package.json 에 scripts 추가
```
"scripts": {
  "start:dev": "forever start --watch src/ src/index.js"
}
```

### nodemon
윈도우에서 개발할 때 forever보다 nodemon이 좀더 편리
```
$ npm install -g --save-dev nodemon
$ nodemon app.js
```
package.json 에 scripts 추가 : src 폴더를 감시하다가 변화시 src/index.js 재시작
```
"scripts": {
  "start:dev": "nodemon --watch src/ src/index.js"
}
```
재시작이 필요할 때 서버 시작 명령어
```
npm run start:dev
```





