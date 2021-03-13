---
{"layout": "post", "categories": "Installation", "title": "dockerRootless", "feature-img": "assets/img/feature_img.png"}
---
# install non-root user docker
```
Rootless mode executes the Docker daemon and containers inside a user namespace. This is very similar to userns-remap mode, except that with userns-remap mode, the daemon itself is running with root privileges, whereas in rootless mode, both the daemon and the container are running without root privileges.

Rootless mode does not use binaries with SETUID bits or file capabilities, except newuidmap and newgidmap, which are needed to allow multiple UIDs/GIDs to be used in the user namespace.
```
- Rootless mode : SETUID bits, 파일 capabilities 사용 안함

* pre-requisites
```
newuidmap, newgidmap
```
같은 네임스페이스에서 여러 UID,GID를 사용가능하게 매핑

# limitation
Only vfs graphdriver is supported.
However, on Ubuntu and Debian 10, overlay2 and overlay are also supported.
Following features are not supported:
```
        Cgroups (including docker top, which depends on the cgroups)
        AppArmor
        Checkpoint
        Overlay network
        Exposing SCTP ports
```
To use ping command, see Routing ping packets
To expose privileged TCP/UDP ports (< 1024), see Exposing privileged ports

# install-ubuntu
```
sudo curl -fsSL https://get.docker.com/rootless | sh
sudo docker rm `sudo docker ps -aq`
sudo docker rmi hello-world
```

# install-centos7.7+
```
sudo sysctl -a | grep namespaces
/etc/sysctl.conf
	user.max_user_namespaces=28633
sudo sysctl --system
```

# Cgroup2
* to enable cgroup in root-less mode
```
The default cgroup driver (dockerd --exec-opt native.cgroupdriver) is “systemd” on v2, “cgroupfs” on v1.
The default cgroup namespace mode (docker run --cgroupns) is “private” on v2, “host” on v1.
The docker run flags --oom-kill-disable and --kernel-memory are discarded on v2.

/sys/fs/cgroup/memory/docker/<longid>/ on cgroup v1, cgroupfs driver
/sys/fs/cgroup/memory/system.slice/docker-<longid>.scope/ on cgroup v1, systemd driver
/sys/fs/cgroup/docker/<longid/> on cgroup v2, cgroupfs driver
/sys/fs/cgroup/system.slice/docker-<longid>.scope/ on cgroup v2, systemd driver
```

* pre-requisite
```
    containerd: v1.4 or later
    runc: v1.0.0-rc91 or later
    Kernel: v4.15 or later (v5.2 or later is recommended)
```

* cgroup 버전 변경
```
sudo sysctl -a | grep cgroup
/etc/sysctl.conf
	systemd.unified_cgroup_hierarchy=1
sudo sysctl --system
또는
sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=1"
```


# run
```
systemd start dockerd
```
centos7 : systemctl --user 작동 안하므로 스크립트로 직접 실행해야
```
dockerd-rootless.sh
```

# check UID, GID
```
id -u
whoami
grep ^$(whoami): /etc/subuid
	100000:65536
grep ^$(whoami): /etc/subgid
	100000:65536
```


