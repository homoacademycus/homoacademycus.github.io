---
{"layout": "post", "categories": "TroubleShooting", "title": "django3 sqlite version", "feature-img": "assets/img/feature_img.png"}
---
# sypmtoms
```
Django 3.1.7.

django.core.exceptions.ImproperlyConfigured: SQLite 3.8.3 or later is required (found 3.7.17).
```

# solution
1. downgade django version into 2.1
```
pip3 install django==2.1
```

2. install sqlite 3.8.3
```
wget files
make install
```

