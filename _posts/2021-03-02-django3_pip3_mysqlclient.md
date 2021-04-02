---
{"layout": "post", "categories": "TroubleShooting", "title": "django3 pip3 mysqlclient", "feature-img": "assets/img/feature_img.png"}
---
pip3 install mysqlclient

Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-7c89pqoy/mysqlclient/

pip3 install --upgrade setuptools
pip3 install ez_setup
yum install python3-devel


mysql_config 파일을 찾지 못해 설치 못되는 경우도 발생한다.


위와 같은 경우에는 PATH에 해당 경로를 삽입해주면 된다.

 export PATH="....MSQL바이너리경로:$LD_LIBRARY_PATH"
