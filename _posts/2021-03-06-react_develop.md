---
{"layout": "post", "categories": "TroubleShooting", "title": "react develop", "feature-img": "assets/img/feature_img.png"}
---
# eslint
installed as Global dev modules
```
RUN npm install -y -g --save-dev eslint prettier eslint-config-prettier
```
must install ESLint in Local?
```
eslint --init

Local ESLint installation not found.
The config that you've selected requires the following dependencies:
    eslint-plugin-react@latest eslint@latest
```
don't need to install in Local. just enter ctrl+C.
```
ESLint was installed locally. 
We recommend using this local copy instead of your globally-installed copy.
```
add module names in package.json, and run npm install. will fetch from global path.

# temporary change port
```
export PORT=80
```

# props type string
```
컴포넌트에 props 전달 할 때 isblock={true}가 아닌 "true"로 전달해야
특히 a 태그는 props로 Boolean 타입을 전달 불가하므로 삼항연산자나 문자열로 전달
```

# label for
input 태그를 순수 html이 아니라 제어를 위해 컴포넌트로 쓰면 이게 필요할까?
```
<label htmlFor="" />
```

# form
- native html 폼에서 제출 버튼을 누르면 현상태의 input값들을 data 전송 + 페이지 이동
- react에서는 핸들러 함수로 axios 통신 처리+페이지 이동
- react는 폼에서도 화면전환없이 데이터를 전달하기 위해서 FormData를 사용

#   이미지 업로드
JSON 형태가 아닌 폼 형식으로 전송해야 : axios로 보낼 때 header에 추가
```
headers: {
        "content-type": "multipart/form-data"
      }
```



