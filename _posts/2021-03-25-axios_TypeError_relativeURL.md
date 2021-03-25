---
{"layout": "post", "categories": "TroubleShooting", "title": "axios TypeError relativeURL", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
TypeError: relativeURL.replace is not a function

t.replace is not a function
```

# Cause
```
let queryString = "/contracts/?search=   2021-03-25"
await HttpClient.get(queryString).then((response) => {
```

# Solution
```

```



