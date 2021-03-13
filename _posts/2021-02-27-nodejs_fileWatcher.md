---
{"layout": "post", "categories": "TroubleShooting", "title": "nodejs fileWatcher", "feature-img": "assets/img/feature_img.png"}
---
# symtom
```
Error: ENOSPC: System limit for number of file watchers reached
```

# reason
```
cat /proc/sys/fs/inotify/max_user_watches
```
Watchers are part of the inotify Linux kernel subsystem1 that extend the filesystem to notice changes and report on those changes to applications listening for them

# slove
1. run as production mode

2. set on vscode watcher's ignore list
```
settings.json

"files.watcherExclude": {
    "**/.git/objects/**": true,
    "**/.git/subtree-cache/**": true,
    "**/node_modules/*/**": true,
    "**/package-lock.json": true,
    "**/yarn.lock": true,
    "**/dist/*/**": true,
    "**/vendor/*/**": true,
    "**/dist_electron/**": true,
},
```

3. increase temporary
```
sudo sysctl fs.inotify.max_user_watches=10000
sudo sysctl -p 
```

4. increase forever
```
echo fs.inotify.max_user_watches=10000 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p 
```


