# JAR, WAR 차이 및 빌드 방법

1. JAR? WAR?

기본적으로 JAR, WAR 모두 Java의 jar 옵션(java -jar)을 이용해 생성된 압축(아카이브) 파일로, 애플리케이션을 쉽게 배포하고 동작시킬 수 있도록 관련 파일(리소스, 속성 파일 등)을 패키징 한 것

<br>

![Untitled](https://user-images.githubusercontent.com/80576569/186606853-dc5eb93c-39bb-40d0-8191-3088d9779133.png)

***JAR(Java Archive)***

- Java 어플리케이션이 동작할 수 있도록 Java 프로젝트를 압축한 파일
- Class (Java 리소스, 속성 파일), 라이브러리 파일을 포함한다.
- JRE (Java Runtime Environment)만 있어도 실행 가능하다. (Java -jar 프로젝트네임.jar)

<br>

***WAR (Web Application Archive)***

- Servlet/JSP 컨테이너에 배치할 수 있는 웹 애플리케이션(Web Application) 압축 파일 포맷
- 웹 관련 자원을 포함함 (JSP, Servlet, JAR, Class, XML, HTML, JavaScript)
- 사전 정의된 구조를 사용한다. (WEB-INF, META-INF)
- 별도의 웹 서버(WEB) or 웹 컨테이너(WAS) 필요하다.
- 즉, JAR 파일의 일종으로 웹 애플리케이션 전체를 패키징 하기 위한 JAR 파일이다.

<br>

***Spring boot에서의 JAR와 WAR***

두 방식 모두 WAS 컨테이너 위에서 동작하게 되는데, 이는 JAR 파일에 WAS가 내장되어 있기 때문, embedded tomcat을 jar에 내장해서, jar 파일로도 필드가 가능하다. 따라서 기존 톰캣과 같은 컨테이너를 이용해야 했던 스프링보다 훨씬 간단하게 애플리케이션을 제작/배포할 수 있는 것이다.

하지만 필요에 따라 외부 WAS를 이용해야할 경우도 생기는데, 때문에 이때는 WAR 파일로 패키징 해야 한다.

<br>

2. IntelliJ Spring Boot 프로젝트 배포 jar 파일 생성 (Maven)

(1) pom.xml에 관련 내용 작성 및 추가

```xml
<groupId>com.package</groupId>
<artifactId>XXX</artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>war</packaging>
<name>example</name>
<description>example</description>
```

<br>

(2) IntelliJ Maven 탭의 package를 실행

![Untitled 1](https://user-images.githubusercontent.com/80576569/186606896-aa69bf42-51fa-4b26-b0a8-dfbc9d0a9455.png)

<br>

(3) target 폴더 내에 정해진 양식으로 배포파일이 생성됨

![Untitled 2](https://user-images.githubusercontent.com/80576569/186606953-9e58dd61-21ce-4157-a4ce-38aa394ec99a.png)

<br>

3. IntelliJ Spring Boot 프로젝트 배포 war 파일 생성 (Maven)

(1) pom.xml에 packaging 항목에 war를 추가

(2) [Application.java](http://Application.java) 에서 SpringBootServletInitializer를 extends 해준다. 이후 SpringApplicationBuilder 메서드를 Override 한다.

```java
@ServletComponentScan
@SpringBootApplication
public class Application extends SpringBootServletInitializer {
	
	@Bean
	public ExitCodeGenerator exitCodeGenerator() {
		return () -> 42;
	}
	
	@Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder){
        return builder.sources(KisaApplication.class);
    }
	
	@PostConstruct
	public void started() {
		TimeZone.setDefault(TimeZone.getTimeZone("Asia/Seoul"));
	}
	
	public static void main(String[] args) {
		SpringApplication.run(KisaApplication.class, args);
	}
}
```

(3) 파일 > 프로젝트 구조 > 아티팩트 > + > 웹 애플리케이션: Archive > 프로젝트 명: war exploded에 대해 선택

![Untitled 3](https://user-images.githubusercontent.com/80576569/186606996-8dfbf290-f269-4746-9cda-27891068b94f.png)

(4) 빌드 > 아티팩트 빌드에서 아까 추가해준 아티팩트에 빌드

out 폴더 하위에 war 파일이 생성된다고 하나, 나는 jar 파일 생성과 동일하게 target 폴더 하위에 생성되었다.
