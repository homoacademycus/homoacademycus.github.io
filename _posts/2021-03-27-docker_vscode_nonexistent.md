---
{"layout": "post", "categories": "TroubleShooting", "title": "docker vscode nonexistent", "feature-img": "assets/img/feature_img.png"}
---
# symtoms
vscode remote container with docker
```
[379 ms] Start: Run in container: cat /etc/passwd
[382 ms] Start: Run in container: test -d /nonexistent/.vscode-server
[383 ms] Exit code 1
[384 ms] Start: Run in container: set -o noclobber ; mkdir -p '/nonexistent/.vscode-server/data/Machine' && { > '/nonexistent/.vscode-server/data/Machine/.writeMachineSettingsMarker' ; } 2> /dev/null
[386 ms] mkdir: cannot create directory '/nonexistent': Permission denied
```

# cause
vscode tried to make execute binary in container user's home directory, but it doesn't exist.

# solution
make home dir in dockerfiles or do it directly


