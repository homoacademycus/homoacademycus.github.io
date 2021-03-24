---
{"layout": "post", "categories": "TroubleShooting", "title": "nginx proxy django 502", "feature-img": "assets/img/feature_img.png"}
---
# symtom
```

```

# possible cause and solution
1. nginx and django communicate with WSGI protocol, not HTTP protocol
- in response header
```

```
- setup a WSGI HTTP server

2. 
