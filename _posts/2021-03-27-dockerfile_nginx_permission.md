---
{"layout": "post", "categories": "TroubleShooting", "title": "dockerfile nginx permission", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
Cannot start service nginx-container: OCI runtime create failed: container_linux.go:370: starting container process caused: exec: "/path": permission denied: unknown
```

# Cause
```
container user's permission != execute path's permission
```

# Solution
add below into Dockerfiles
```
RUN chmod -R 775 /usr/share/nginx/html
```


