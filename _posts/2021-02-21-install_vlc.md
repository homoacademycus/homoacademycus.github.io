---
{"layout": "post", "categories": "Installation", "title": "install vlc", "feature-img": "assets/img/feature_img.png"}
---
# centos7
sudo subscription-manager repos --enable "rhel-*-optional-rpms" --enable "rhel-*-extras-rpms"
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum install https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm
sudo yum install vlc
