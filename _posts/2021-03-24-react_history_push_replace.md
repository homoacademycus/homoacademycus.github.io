---
{"layout": "post", "categories": "TroubleShooting", "title": "react history push replace", "feature-img": "assets/img/feature_img.png"}
---
Home > Item > Login > Item 순으로 페이지를 이동했을 때 Login 페이지에서 history.push를 사용할 때와 history.replace를 사용할 때의 차이점은 다음과 같다.
Push

import React from 'react';

function Login({ history }) {
  history.push('/item');
  return <div>Login</div>;
}

export default Login;

Home > Item > Login > Item 순으로 history에 쌓여서, 마지막 페이지에서 뒤로가기 버튼을 누르면 Login 페이지로 되돌아간다.
Replace

import React from 'react';

function Login({ history }) {
  history.replace('/item');
  return <div>Login</div>;
}

export default Login;

Home > Item > Item 순으로 history에 쌓여서, 마지막 페이지에서 뒤로가기 버튼을 누르면 Item 페이지로 되돌아간다.
정리

history를 스택이라고 생각했을 때, push는 history 제일 위에 쌓는 것이고, replace는 history 제일 위에 있는 원소를 지금 넣을 원소로 바꾸는 것이다.
