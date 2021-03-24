---
{"layout": "post", "categories": "TroubleShooting", "title": "nginx request options", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
request as POST
response as OPTIONS
```

# Cause
```
ask server first with OPTIONS if POST method is possible to use
```

# Solution
```
should add OPTIONS method into response header's 'Access-Control-Allow-Methods'
```




