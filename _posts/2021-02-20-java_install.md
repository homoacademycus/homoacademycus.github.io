---
{"layout": "post", "categories": "Installation", "title": "java install", "feature-img": "assets/img/feature_img.png"}
---
## Java openjdk 패키지 설치
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt update
sudo apt install openjdk-11-jre
sudo apt install openjdk-11-jdk
sudo apt install ppa-purge
sudo ppa-purge ppa:openjdk-r/ppa
```

## Java SE 8 (jdk1.8) 직접 설치
```
https://www.oracle.com/java/technologies/javase-jdk8-downloads.html
sudo mkdir -p /opt/jdk
sudo cp -rf jdk* /opt/jdk
cd /opt/jdk*
sudo tar -zxf jdk*
sudo mv jdk* jdk1.8.0
ls

sudo update-alternatives --display java
sudo update-alternatives --display javac

sudo update-alternatives --install /usr/bin/java java /opt/jdk1.8.0/bin/java 100
sudo update-alternatives --install /usr/bin/javac javac /opt/jdk1.8.0/bin/javac 100

sudo update-alternatives --config java
sudo update-alternatives --config javac

sudo  nano /etc/environment
  JAVA_HOME="/opt/jdk1.8.0"
  JRE_HOME="/opt/jdk1.8.0/jre"

source /etc/environment
echo $JAVA_HOME
sudo apt-get update
java -version
```

## 자바, 자바컴파일러 설치 확인
```
java
javac
```

## 환경 변수
1. 사용자 변수 : 사용자 별로 다르게 적용되는 지역 변수
2. 시스템 변수 : 시스템 전체에 적용되는 전역 변수
```
- application이 참조할 설정 값
- 특정 명령어 또는 실행 프로그램이 저장된 경로를 환경변수에 미리 저장
- 어떤 위치에서든 실행 가능하게 됨
```

## JAVA 환경변수 설정
자바 컴파일러 또는 클래스파일 로더를 어떤 위치에서든 실행시키려면
```
윈도우 : 고급 시스템 설정 > 고급 > 환경변수 > 시스템 변수 > JAVA_HOME
리눅스 : sudo $JAVA_HOME = /usr/java/default
```

## 기준 폴더 경로
1. 변수 이름 : JAVA_HOME
2. 변수 값 : JAVA 설치폴더 경로
```
윈도우 : C:\Program Files\Java\jdk1.8.0_221
리눅스 : /usr/
```
3. 목적 : PATH 변수에 상대경로로 %JAVA_HOME%\bin 만 써 놓고,
실제 JAVA의 경로가 변경되면 자동으로 적용되도록 기준점 설정
==> 여러 프로그램에서 내부적으로 JAVA_HOME을 참조하기 때문

## 실행 폴더 경로
1. 변수 이름 : PATH
2. 변수 값 : JAVA 실행파일 경로
```
윈도우 : %JAVA_HOME%\bin\
리눅스 : %JAVA_HOME%/bin/
```
3. 목적 : 자바 프로그램을 실행하기 위한 실행파일과 가상머신의 경로

## class 파일 경로
1. 변수 이름 : CLASSPATH
2. 변수 값 : JAVA 라이브러리 경로
```
윈도우 : %JAVA_HOME%\lib
리눅스 : %JAVA_HOME%/lib
```
3. 목적 : JVM(자바가상머신)의 class loader가 라이브러리 class들을 참조하는 위치
==> J2JDK버전 부터는 \jre\lib\ext 폴더에 라이브러리를 복사하면 되므로
==> 특별한 경우가 아니면 이 변수를 설정하지 않는다(?)

## 특정 class 파일 참조할 때
```
java -classpath "경로" 파일명
```
