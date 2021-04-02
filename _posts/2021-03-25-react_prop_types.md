---
{"layout": "post", "categories": "TroubleShooting", "title": "react prop types", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
props type string
```


# Cause
```
컴포넌트에 props 전달 할 때 isblock={true}가 아닌 "true"로 전달해야
특히 a 태그는 props로 Boolean 타입을 전달 불가하므로 삼항연산자나 문자열로 전달
```




