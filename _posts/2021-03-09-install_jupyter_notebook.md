---
{"layout": "post", "categories": "Installation", "title": "install jupyter notebook", "feature-img": "assets/img/feature_img.png"}
---
# Jupyter Notebook
웹 브라우저(Tornado web 프레임워크) 기반의 인터프리터. 문서화/학습 기능
로컬 서버의 kernel이 IPython 인터프리터를 실행시킴

1. python pip로 설치하기
```bash
python3 -m pip install --upgrade pip
sudo pip3 install jupyter
```

2. anaconda 설치하기(포함되어 있음)

3. bash shell 또는 anaconda shell에서 실행하기
```
jupyter notebook
```

4. 로컬 서버의 8888포트에서 웹앱 사용 가능
http://localhost:8888/tree

5. theme 적용
```bash
sudo pip3 install jupyterthemes
jt -l
jt -t [테마명]
```

# Paths
```
config:
    ~/.jupyter
    /usr/etc/jupyter
    /usr/local/etc/jupyter
    /etc/jupyter
data:
    ~/.local/share/jupyter
    /usr/local/share/jupyter
    /usr/share/jupyter
runtime:
    ~/.local/share/jupyter/runtimes
```

# available sub commands
```
bundlerextension console kernel kernelspec migrate nbconvert nbextension notebook qtconsole run serverextension troubleshoot trust
```

# 도커 컨테이너 내에서 서버 실행
```
docker run -it -p 포트:포트 ...
jupyter notebook --ip=0.0.0.0 --port=포트 --allow-root
```
호스트의 웹브라우저에서 도커 컨테이너의 주소:포트로 접속
```
http://컨테이너의 주소:포트
```
토큰을 입력하라는 화면이 표시되면,
도커 컨테이너에서 서버 실행 시 터미널에 출력된 토큰을 복사 붙여넣기

** 매번 토큰인증 안하려면?

# 주피터 노트북 원격에서 실행
```
ssh -N -f -L 호스트1:포트:호스트2:포트 remoteuser@remotehost
```



