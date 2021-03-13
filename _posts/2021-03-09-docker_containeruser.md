---
{"layout": "post", "categories": "TroubleShooting", "title": "docker containeruser", "feature-img": "assets/img/feature_img.png"}
---
# Container user

```
Docker container's root is fake user.
container에서만 root이지 실제로 호스트에서는 제대로 작동하지 않는다.

컨테이너를 root계정으로 실행되면 docker가 file을 root권한으로 write하기 때문에
어플리케이션에서 write한 파일을 사용자가 root권한이 아니라면 수정하거나 삭제할 수 없다

개발 시 호스트에 mount 해서 사용하는 볼륨 권한 문제
컨테이너 속 볼륨권한을 호스트 사용자와 동일한 gid를 가지도록
```

# dockerfile

```
RUN useradd --groups hostuser --create-home containeruser
RUN chown -R containeruser:hostuser /path
```

# Host volume

```
drwxrwx---.  hostuser hostuser

uid=1001(hostuser) gid=1001(hostuser) groups=1001(hostuser),980(docker),
```

# Container volume

```
drwxrwx---.     1001 containeruser

uid=1000(containeruser) gid=1001(containeruser) groups=1001(containeruser),1000(hostuser)
```
??? expected as containeruser:hostuser

# added groupadd to dockerfile
```
RUN groupadd --gid ${hostgid} ${hostuser}
```

# modified --groups into --gid
```
RUN useradd --gid ${hostgid} --create-home containeruser
```
