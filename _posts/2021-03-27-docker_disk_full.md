---
{"layout": "post", "categories": "TroubleShooting", "title": "docker disk full", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
disk space is almost full
```

# Cause
```
sudo du -h / | grep '[0-9\,]\+G'
```
/var/lib has the most biggest size. seems like docker data cause this.

# Solution
- remove unused docker related data
```
docker system prune -a -f

Total reclaimed space: 4.922GB
```

- change docker data dir into big size disk
```
echo -n "enter new docker data dir path: "
read dirpath
sudo lsof | grep /var/lib/docker
sudo systemctl stop docker
sudo mv /var/lib/docker $dirpath
sudo ln -s $dirpath/docker /var/lib/docker
sudo ls -al /var/lib/docker
sudo lsof | grep /var/lib/docker
```

