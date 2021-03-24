---
{"layout": "post", "categories": "TroubleShooting", "title": "react image upload", "feature-img": "assets/img/feature_img.png"}
---
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



