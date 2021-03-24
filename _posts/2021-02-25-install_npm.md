---
{"layout": "post", "categories": "Installation", "title": "install npm", "feature-img": "assets/img/feature_img.png"}
---
* nodejs
크롬 V8 엔진으로 빌드된 js 실행환경. 웹브라우저 외에서도 js 사용가능.

* npm 설치
```
apt install nodejs
yum install nodejs
```

* alpine 리눅스에서 설지
```
apk add --update nodejs nodejs-npm
```

* n 모듈 : nodejs 버전 관리 --> nvm과 다른점은?
```
npm cache clean -f
npm install -g n
n stable
installing : node-v14.15.0
```

* npx : npm 모듈을 로컬에 설치해도 global처럼 실행가능하게 해줌
```
node ./node_modules/.bin/mocha 대신에 npx mocha
```

* 전역 모듈 설치 : $(npm root -g)/모듈명
```
npm root -g
/usr/local/lib/node_modules

npm install -g 모듈명
/usr/local/bin/create-react-app -> $(npm root -g)/create-react-app/index.js
```
Node.js와 npm 모듈은 발전속도가 빨라서 버전 때문에 API가 바뀌거나 호환이 안될때가 많음.
버전을 고정하거나 최신 버전을 사용하고자 할 때 유용

* 로컬 모듈 설치 : $HOME/node_modules/모듈명
```
npm install 모듈명

export PATH=$PATH:$HOME/node_modules/.bin/

$HOME/.npm/vue-cli/모듈정보
$HOME/node_modules/.bin/실행파일의 심볼릭링크
```

* /프로젝트root/package.json 에 로컬모듈 목록을 정의해놓고 한꺼번에 설치하기
package.json 파일 생성
```
npm init
```
package.json 파일 수정
```
{
  "name": "Example Application",
  "version": "0.0.1",
  "main": "app.js",
  "dependencies": {
    "express": "3.4.x"
  , "foo" : "1.0.0 - 2.9999.9999"
  , "bar" : ">=1.0.2 <2.1.2"
  , "baz" : ">1.0.2 <=2.3.4"
  , "boo" : "2.0.1"
  , "qux" : "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0"
  , "asd" : "http://asdf.com/asdf.tar.gz"
  , "til" : "~1.2"
  , "elf" : "~1.2.3"
  , "two" : "2.x"
  , "thr" : "3.3.x"
  }
}
```
~1.2는 가장 근접한 버전, 2.x는 2.으로 시작하는 가장 최신 버전

* 개발용 의존 모듈 설치
```
npm install --save-dev 모듈명
npm install --save-dev eslint
```
package.json에 반영됨
```
"dependencies": {
    "jsonwebtoken": "^7.3.0",
    "log4js": "^0.6.38"
  },
"devDependencies": {
    "eslint": "^5.6.0"
  }
```

* 전역 모듈 환경변수 설정 : 불안정
```
echo 'export NODE_PATH=$(npm root -g)' >> ~/.bashrc
source ~/.bashrc

export NODE_ENV="production" node app.js
```




