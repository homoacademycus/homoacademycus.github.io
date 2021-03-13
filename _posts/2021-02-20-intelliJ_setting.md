---
{"layout": "post", "categories": "Installation", "title": "intelliJ setting", "feature-img": "assets/img/feature_img.png"}
---
# eclipse 프로젝트를 IntelliJ 프로젝트로 변환하기
Workspace, Project --> Project, Module 로 이름 대응하여 import

# new Project 생성
Graddle > Java, Web

# Tomcat Run 설정
Run > Edit Configuration > Tomcat Server > Local > Deployment > + > Artifacts > (exploded)

# Enable Annotation Processing
Settings > Build, Execution, Deployment > Compiler > Annotation Processors

# build/run using Gradle(default) or IDE
Settings > Build, Execution, Deployment > Build Tools > Gradle
```
IntelliJ가 Graddle을 default로 run하는 이유 ?
Local PC와 Continuous Integration Server에서 모두 동일한 테스트 결과를 얻기 위해 gradle로 실행
```

# src/main/webapp/WEB-INF/web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/dispatcher-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```
