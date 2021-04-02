---
{"layout": "post", "categories": "Installation", "title": "buildAutoTools", "feature-img": "assets/img/feature_img.png"}
---
# Build Tool
1. 빠른 기간동안에 계속해서 늘어나는 라이브러리의 추가
2. 프로젝트를 진행하며 라이브러리의 버전을 동기화

# Apache Ant
1. 각 프로젝트에 대한 XML기반 빌드 스크립트 개발
2. 형식적인 규칙이 없음 : 결과물을 넣을 위치를 정확히 알려줘야 하며, 프로젝트에 특화된 Target과 Dependency를 이용해 모델링 --> 스크립트 재사용 어려움
3. 절차적 : 명확한 빌드 절차 정의가 필요
4. 생명주기를 갖지 않기 때문에 각각의 target에 대한 의존관계와 일련의 작업을 정의해 주어야 함

# Apache Maven
1. multi poject 환경에서 여러 라이브러리들을 연결 및 업데이트
2. pom.xml을 이용한 정형화된 빌드 시스템

# Gradle
1. multi project 환경에서 설정을 상속받을 필요 없이 다른 모듈에 주입
2. xml 대신 Groovy라는 언어(JVM 위에서 동작하는 스크립트 언어) 사용
3. 안드로이드 스튜디오의 공식 빌드 시스템
4. 다양한 언어 지원

# Gradle
settings.gradle 파일--> multi project 여부 설정, project의 인스턴스생성

# build.gradle 파일

# Gradle 사용자 메뉴얼
https://docs.gradle.org/current/userguide/userguide_single.html#producing_and_consuming_variants_of_libraries
