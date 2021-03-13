---
{"layout": "post", "categories": "TroubleShooting", "title": "docker compose", "feature-img": "assets/img/feature_img.png"}
---
# Exit state code
```
Exited(0) : 
Exited(1) : 
Exited(2) : 
Exited(125) : 
Exited(126) : 
```
- Entrypoint can't point to /bin/bash
- where there is nothing to run, entrypoint "npm run" cause exited. use "sleep 99"

# vscode
- remote-container extension needs permission to mkdir.
- needs to set capabilities below for develop purpose.
```
        cap_drop:
#            - ALL
            - MAC_ADMIN
            - NET_ADMIN
            - SYS_ADMIN
        cap_add:
            - ALL
#            - NET_BIND_SERVICE
```


