---
{"layout": "post", "categories": "Installation", "title": "sqlDeveloper", "feature-img": "assets/img/feature_img.png"}
---
# Running SQL Developer in a Docker container
Docker is a hot topic at the moment and many have written interesting articles about how to use Docker in combination with Oracle. I especially liked Frits Hoogland’s article on installing an Oracle 12c database in a Docker container. It got me thinking about running SQL Developer in a container and how we can achieve this. There have been several other articles about this but I use a somewhat different approach than most.

I wanted to be able to use my standard setup where I run a minimal Oracle Enterprise Linux server in Virtualbox and use MobaXterm to access the server. MobaXterm is a great product because in contains everything you need to access a server including Putty, sFTP and even an Xserver. It is my favorite client as it contains everything I one portable executable. Because I run my Xserver locally I don’t have to run the complete desktop in my Virtualbox guest. If you also switch on port forwarding in your virtualbox image you can connect to localhost:2222 via ssh (I usually forward port 22 to 2222 locally, you can choose your own).

What do you need:

- A virtualbox image which runs Oracle Enterprise Linux 6.7 with Docker installed (Frits Hoogland explains how to create this in detail) and will be the Docker host system.
- MobaXterm
- Java JDK RPM
- SQL Developer RPM (you need an Oracle Technet account)

In the newly created OEL image I add an account to run SQL Developer. This account must have privileges to run Docker containers. Adding a user to the Docker group has serious security implications, see Docker daemon attack surface for details.
```
$ groupadd -g 54321 oinstall
$ groupadd -g 54322 dba
$ useradd -m -g oinstall -G oinstall,dba -u 54321 oracle

$ usermod -aG docker oracle
```
Following Frits’ lead I put my docker files in /var/lib/docker/dockerfiles where I created a folder build-sqldev-411. I also placed the downloaded java and SQL Developer rpm’s in a sub-folder called oracle-install-files. This way I can easily add the files to my container during the build. My Dockerfile looks like this:
```
FROM    oraclelinux:6
MAINTAINER l.parren@thedoc.nl
RUN groupadd -g 54321 oinstall
RUN groupadd -g 54322 dba
RUN useradd -m -g oinstall -G oinstall,dba -u 54321 oracle
RUN yum -y install xterm xauth libXtst
ADD oracle-install-files/jdk-8u60-linux-x64.rpm /tmp/
RUN yum -y install /tmp/jdk-8u60-linux-x64.rpm
RUN rm -f /tmp/jdk-8u60-linux-x64.rpm
ADD oracle-install-files/sqldeveloper-4.1.1.19.59-1.noarch.rpm /tmp/
RUN yum -y install /tmp/sqldeveloper-4.1.1.19.59-1.noarch.rpm
RUN rm /tmp/sqldeveloper-4.1.1.19.59-1.noarch.rpm
USER oracle
WORKDIR /home/oracle
ENV JAVA_HOME=/usr/java/latest
CMD sqldeveloper
```
3-5: Add user oracle
6: Add X-window related files (I usually just add xterm so I don’t have to list packages independently)
7-9: Install Java JDK from RPM
10-12: Install SQL Developer from RPM
13-15: Set user to oracle, set the working directory and make sure the JDK can be found
16: Run SQL DeveloperThe folder structure looks like this:

```
$ pwd
/var/lib/docker/dockerfiles/build-sqldev-411
$ ll -R
.:
total 4
-rw-r--r--. 1 root root 697 Aug 28 22:00 Dockerfile
drwxr-xr-x. 1 root root 118 Aug 29 01:52 oracle-install-files

./oracle-install-files:
total 471316
-rw-r--r--. 1 root root 160084320 Aug 21 10:28 jdk-8u60-linux-x64.rpm
-rw-r--r--. 1 root root 322535748 Aug 21 10:29 sqldeveloper-4.1.1.19.59-1.noarch.rpm
```
After we have created the Dockerfile and placed the rpm’s in the right location we can generate the image:
```
$ cd /var/lib/docker/dockerfiles/build-sqldev-411
$ docker build -t "sqldev-411" .
```
Wait for the process to finish after which we can check which images are available:
```
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
sqldev-411          latest              7d4cb24d9146        2 hours ago         2.037 GB
oracle-12102        latest              8ffdfb9acb44        7 days ago          12.22 GB
oraclelinux         6                   cfc75fa9f295        4 weeks ago         156.2 MB
```
We now have a image which contains everything we need to run sqldeveloper, so let’s give it a go:
```
$ docker run -ti sqldev-411

 Oracle SQL Developer
 Copyright (c) 1997, 2015, Oracle and/or its affiliates. All rights reserved.

/opt/sqldeveloper/sqldeveloper/bin/../../ide/bin/launcher.sh: line 1159: file: command not found
```
And nothing happens. The reason for this is that the container does not know how to connect to an Xserver, we did not install one in the virtual machine and there is none running on the client. I use MobaXterm to run a local Xserver. It will also automatically switch on X11-forwarding in a ssh session. The following statement will start SQL Developer in a Docker container:
```
$ docker run -ti --rm -e DISPLAY -v $HOME/.Xauthority:/home/oracle/.Xauthority --net=host sqldev-411
```
This setup is particularly useful in a test environment on a virtual machine. I can have several applications installed which will not interfere with each other, each can have it’s own versions of libraries and settings. I can have multiple versions of SQL Developer installed with each it’s own Java JDK in a completely isolated environment, yet on one virtual machine, saving space nd memory on my laptop. Furthermore as long as I keep my Dockerfile I can quickly rebuild the container when needed and distribute it to my colleagues.
