---
{"layout": "post", "categories": "TroubleShooting", "title": "npm module not found", "feature-img": "assets/img/feature_img.png"}
---
# symtoms
```
when running scripts with create-react-app,
MODULE_NOT_FOUND ~~ ./node_modules/react-scripts/bin/ ~~
```

# cause
```
global module path and local module path related with react-scripts
```

# solution
```
rm -rf node_modules
npm install -g npm@latest
npm intstall
```

