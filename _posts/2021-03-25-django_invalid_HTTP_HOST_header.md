---
{"layout": "post", "categories": "TroubleShooting", "title": "django invalid HTTP HOST header", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
Invalid HTTP_HOST header: 'web_backend_1:22222'. 
The domain name provided is not valid according to RFC 1034/1035.
```

# Cause
1. I used react webpack proxy server
```
"proxy": "http://web_backend_1:22222"
```

2. settings.py
```
ALLOWED_HOSTS = [ 'web_backend_1' ] ??
```

# Solution
- clean browser history
- set ALLOWED_HOSTS properly
- rebuild image, rerun server

# Issue
- in docker container, docker container name can be used?
