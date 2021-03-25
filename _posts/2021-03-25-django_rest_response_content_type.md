---
{"layout": "post", "categories": "TroubleShooting", "title": "django rest response content type", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
django rest response object should return correspond content type with request.
```
REST framework supports HTTP content negotiation by providing a Response class 
which allows you to return content that can be rendered into multiple content types, depending on the client request.

from https://www.django-rest-framework.org/
```

Response(data, status=None, template_name=None, headers=None, content_type=None)
```
Typically, this will be set automatically by the renderer as determined by content negotiation, but there may be some cases where you need to specify the content type explicitly.
```

but when request is application/json, response was text/html. why?
```
Request Header's Accept: application/json, text/plain, */*
Response Header's Content-Type: text/html
```

# Cause & Solution
1. you didn't set default parser, renderer for REST framework in settings.py
```
REST_FRAMEWORK = {
    'DEFAULT_PARSER_CLASSES': [
        'rest_framework.parsers.JSONParser',
        'rest_framework.parsers.FormParser',
    ],
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
        'rest_framework.renderers.BrowsableAPIRenderer',
    ],
    ...
}
```
When request.data is accessed, REST framework will examine the Content-Type header on the incoming request, and determine which parser to use to parse the request content.

2. you used BrowsableAPI or Admin site, and it cashed
check header
```
HttpRequest.META
HttpResponse.headers
```

* BrowsableAPIRenderer
```
.media_type: text/html
.charset: utf-8
```
브라우저를 통한 요청에서는 Accept 헤더에 text/html 이 포함되어 Browsable API 방식으로 처리됨

* AdminRenderer
```
.media_type: text/html
.charset: utf-8
```






