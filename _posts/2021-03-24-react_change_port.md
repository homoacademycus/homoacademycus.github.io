---
{"layout": "post", "categories": "TroubleShooting", "title": "react change port", "feature-img": "assets/img/feature_img.png"}
---
# Symtom
```
react's default dev port is 3000.
I'd like to use another port(80).
```

# Cause
```
react server use env PORT=3000
```

# Solution
1. use env for current shell
```
export PORT=80
```

2. or use .env in project dir
```
PORT=80
```

3. or use react-scripts
```
"scripts": {
    "start": “PORT=80 react-scripts start"
```


