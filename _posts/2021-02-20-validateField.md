---
{"layout": "post", "categories": "Installation", "title": "validateField", "feature-img": "assets/img/feature_img.png"}
---
### joi 모듈
* schema의 필드 유효값 설정
```
{
  필드명: joi.필드타입().required(),
  body : joi.string().required(),
  tags : joi.array().items( joi.string() ).required(),
}
```
* 검증
```
const validated = joi.validate(ctx.request.body, postSchema);
if ( validated.error ){
  ctx.status = 400; // Bad Request
  ctx.body = validated.error;
}
```



