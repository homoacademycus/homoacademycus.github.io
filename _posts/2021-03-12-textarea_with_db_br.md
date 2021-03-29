---
{"layout": "post", "categories": "TroubleShooting", "title": "textarea with db br", "feature-img": "assets/img/feature_img.png"}
---
DB 데이터를 불러와서 노출하거나 textarea로 부터 입력받은 데이터를 DB에 저장하려 할 때
```
var str = document.getElementById("textarea").value;
str = str.replace(/(?:\r\n|\r|\n)/g, '<br />');
document.getElementById("result").value = str;
```



