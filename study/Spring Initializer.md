# Spring Initializer

프로젝트 시작 전, Maven과 Gradle의 효율 차이점을 조사 후, Gradle을 이용해 프로젝트 초기 세팅을 진행했다.

| Project | Gradle Project | Language | Java |
| --- | --- | --- | --- |
| Spring Boot | 2.6.5 | Packaging | Jar |
| Java | 18 | Gradle Version | 7.4.1 |

<br>

# Dependencies

*DEVELOPER TOOLS*

- **Spring Boot DevTools** *v2.6.5*
    
    브라우저로 전송되는 내용들에 대한 코드가 변경되려면, 자동으로 어플리케이션을 재시작하여 브라우저에도 업데이트를 해주는 역할을 함.
    
    ```jsx
    developmentOnly 'org.springframework.boot:spring-boot-devtools'
    ```
    
- **Lombok** *v1.18.22*
    
    getter, setter, toString 메서드를 정의해야했던 사항을 자동으로 처리해줌
    
    ```jsx
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
    ```
    
- **Spring Configuration Processor** *v2.6.5*
    
    Configuraion Metadata는 IDE에서 yml 혹은 properties에서 사용하는 Configuration의 자동 완성을 도와주는 메타 데이터
    
    ```jsx
    annotationProcessor 'org.springframework.boot:spring-boot-configuration-processor'
    ```
    
- **Elasticsearch** *v7.15.2*
    
    elasticsearch를 사용하기 위한 라이브러리 추가
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-data-elasticsearch'
    ```
    

    <br>

*WEB*

- **Spring Web** *v5.3.17*
    
    Spring MVC를 사용하여 RESTful을 포함한 웹 어플리케이션을 빌드함. Apache Tomcat을 기본 내장 컨테이너로 사용함
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-web'
    ```
    
- **Spring Session** *v2.6.2*
    
    서버에 저장되는 HTTP 세션의 한계로부터 세션 관리를 자유롭게 한다는 목표를 가지고 있음. 사용자 세션 정보를 관리하기 위한 API 및 구현을 제공. 스프링 세션은 JDBC, MongoDB, Redis 등을 사용하여 데이터를 유지할 수 있음
    
    ```jsx
    implementation 'org.springframework.session:spring-session-jdbc'
    ```
    

<br>

*SECURITY*

- **Spring Security** *v2.6.5*
    
    보안과 관련해서 체계적으로 많은 옵션들로 이를 지원해줌. spring security는 filter 기반으로 동작하기 때문에 spring MVC와 분리되어 관리 및 동작함
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-security'
    ```
    
<br>

*SQL*

- **JDBC API** *v2.6.5*
    
    클라이언트가 데이터베이스에 연결하고 쿼리하는 방법을 정의하는 데이터베이스 연결 API
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-jdbc'
    ```
    
- **Spring Data JPA** *v2.6.5*
    
    CRUD 처리를 위한 공통 인터페이스 제공. repository 개발시 인터페이스만 작성하면 실행 시점에 스프링 데이터 JPA가 구현 객체를 동적으로 생성해서 주입
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    ```
    
- **Mybatis Framework** *v2.2.2*
    
    Java에서 SQL Mapper를 지원해주는 Framework, SQL 작성을 직접하여 객체와 매핑시켜줌. JPA를 사용한다면 사용하지 않아도 됨
    
    ```jsx
    implementaion 'org.mybatis.spring.boot:mybatis-spring-boot-stater:2.2.2'
    ```
    
- **MariaDB Driver** *v2.7.5*
    
    MariaDB를 연결하기 위한 라이브러리
    
    ```jsx
    runtimeOnly 'org.mariadb.jdbc:mariadb-java-client'
    ```
    

<br>

*NOSQL*

- **Spring Data Redis (Access+Driver)** *v2.6.5*
    
    Key-Value 형태로 데이터를 관리하는 오픈소스. 빠른 속도와 간편한 사용법으로 인해 캐시, 인증 토큰, 세션 관리 등 여러 용도로 사용됨. redis cache를 사용
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-stater-data-redis'
    ```
    
    - Cache
        - 캐시는 서버의 부하를 감소시키고 빠른 성능(조회)을 확보하여 보다 쾌적한 서비스를 제공하는 것이 목적
        - 캐시의 대상이 되는 항목
            - 정보의 단순성
            - 빈번한 동일 요청의 반복
            - 높은 단위 처리 비용
            - 정보의 최신화가 반드시 실시간으로 이루어지지 않아도 서비스 품질에 영향을 주지않는 정보
        - 예) 검색어, 베스트셀러, 추천 상품, 카테고리, 방문자수, 조회수, 추천수, 1회성 인증정보 등
        - 캐시를 이용한 서비스를 구성할 때는 캐시 정책(정보의 선택, 정보의 유효기간(TTL), 정보의 갱신 시점)을 수립하는게 좋음
        - 많은 캐시 서버 중에서도 Redis를 사용하는 이유는 추상화된 API와 어노테이션 및 Spring Boot Stater Kit 제공과 Spring Boot의 Auto Configuration 적용으로 캐시 서버 설정이 간결하기 때문
        

<br>

*I/O*

- **Validation** *v2.6.5*
    
    검증하기 위한 어노테이션 사용을 위해 추가(@NotNull, @Min, @Max …)
    
    ```jsx
    implementation 'org.springframework.boot:spring-boot-starter-validation'
    ```
    

<br><br>

*[참고]*

Spring Boot의 의존성 확인, version 2.6.5: [https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html)
