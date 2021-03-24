---
{"layout": "post", "categories": "TroubleShooting", "title": "react local installation not found", "feature-img": "assets/img/feature_img.png"}
---
# eslint
installed as Global dev modules
```
RUN npm install -y -g --save-dev eslint prettier eslint-config-prettier
```
must install ESLint in Local?
```
eslint --init

Local ESLint installation not found.
The config that you've selected requires the following dependencies:
    eslint-plugin-react@latest eslint@latest
```
don't need to install in Local. just enter ctrl+C.
```
ESLint was installed locally. 
We recommend using this local copy instead of your globally-installed copy.
```
add module names in package.json, and run npm install. will fetch from global path.
