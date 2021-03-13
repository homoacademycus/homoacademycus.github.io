---
{"layout": "post", "categories": "TroubleShooting", "title": "vscode CPU", "feature-img": "assets/img/feature_img.png"}
---
# vscode CPU 점유율 너무 높음
https://github.com/Microsoft/vscode/wiki/Performance-Issues

1. Disable useless extensions
```
code --status
code --disable-extensions
code --inspect-extensions=ANY_PORT
developer: Show Running Extensions
```

2. install vscode-insider
```
Try to reproduce the issue in the VS Code Insider version. This will run our latest code and use a different setup (settings, extensions). You can install the insider version here https://code.visualstudio.com/insiders
```
worst. freezed.

3. Previous versions of Visual Studio Code can be downloaded here:
```
https://code.visualstudio.com/updates/
```
solved.
