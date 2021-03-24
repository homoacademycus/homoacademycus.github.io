---
{"layout": "post", "categories": "TroubleShooting", "title": "docker container user", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
when volume is mounted between host and container,
if container user is root, if you work in container,
all file's permission is root.
so you can't access that files on host as non-root user.
```

# Solution - temporary
run container as non-root user
```
(create) docker run -it --user {non-root-user} {containername}
or
(existed) docker exec -it --user {non-root-user} {containername} {entrypoint}
```

# Solution - permanate - create new container user
set non-root container user's gid as host user's gid
```
RUN groupadd --gid ${hostgid} ${shared-group-name}
RUN useradd --gid ${hostgid} --create-home containeruser
RUN chown -R containeruser:hostuser /path
RUN chmod -R 770 /path
```

* Host volume

```
drwxrwx---.  hostuser hostuser

uid=1001(hostuser) gid=1001(hostuser) groups=1001(hostuser),xxx(docker),
```

* Container volume

```
drwxrwx---.     1001 containeruser

uid=1000(containeruser) gid=1001(containeruser) groups=1001(containeruser)
```

# Solution - permanate - modify existed container user
add host user's group into non-root container user's group
```
RUN groupadd --gid ${hostgid} ${shared-group-name}
RUN usermod --gid ${hostgid} ${containeruser} 
RUN chown -R ${containeruser}:${hostgid} /path
RUN chmod -R 770 /path
```

* Host volume

```
drwxrwx---.  hostuser hostuser

uid=1001(hostuser) gid=1001(hostuser) groups=1001(hostuser),xxx(docker),
```

* Container volume

```
drwxrwx---.     1001 containeruser

uid=1000(containeruser) gid=1000(containeruser),1001(hostuser) groups=1000(containeruser), 1001(hostuser)
```

