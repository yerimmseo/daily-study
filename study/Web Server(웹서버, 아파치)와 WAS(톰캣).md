# Web Server(웹서버, 아파치)와 WAS(톰캣)

1. Web Server(웹서버)
- 정적 페이지 (Static Pages)
    - Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.
    - 항상 동일한 페이지를 반환한다.
    - ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 파일들

![Untitled](https://user-images.githubusercontent.com/80576569/186608096-263f4150-0929-4b53-9273-1e581e8ed79e.png)


- 동적 페이지 (Dynamic Pages)
    - 인자의 내용에 맞게 동적인 contents를 반환한다.
    - 즉, 웹 서버에 의해서 실행되는 프로그램을 통해서 만들어진 결과물
        
        (* Servlet: WAS 위에서 돌아가는 Java Program)
        
    - 개발자는 Servlet doGet()을 구현한다

![Untitled 2](https://user-images.githubusercontent.com/80576569/186608190-744569f2-7ac3-4421-a52a-70850bfeb0a4.png)

<br>

2. Web Server의 개념

소프트웨어와 하드웨어 두 분야에서 다른 의미로 부른다.

- 하드웨어: 웹 서버 소프트웨어와 웹 사이트의 구성 요소 파일을 저장하는 컴퓨터를 의미
- 소프트웨어: 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html, .jpeg, .css 등)를 제공하는 컴퓨터 프로그램

<br>

3. Web Server의 기능
- HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스하는 기능을 담당
- 기능1)
    - 정적인 컨텐츠 제공
    - WAS를 거치지 않고 바로 자원을 제공
- 기능2)
    - 동적인 컨텐츠 제공을 위한 요청 전달
    - 클라이언트 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)
    - 클라이언트는 일반적으로 웹 브라우저를 의미

<br>    
    
4. Web Server 종류

Apache Server(아파치), Nginx, IIS(Windows 전용 Web 서버) 등

<br>

5. Web Server 단점
- JSP나 PHP 같은 응용 프로그래밍 언어를 해석할 수 없다.
- 이러한 단점 극복을 위해 Java 기반 서버 사이드 언어를 처리할 수 있는 엔진을 개발함 → WAS(Web Application Server)인 Tomcat 탄생

<br>

6. WAS(Web Application Server)

![Untitled 3](https://user-images.githubusercontent.com/80576569/186608222-0051bc30-1028-4ffa-b329-31f32366ba5f.png)

DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server, HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다. “웹 컨테이너(Web Container)” 혹은 “서블릿 컨테이너(Servlet Container)”라고도 불린다.

- Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다.
- 즉, WAS는 JSP, Servlet 구동 환경을 제공한다.

<br>

7. WAS(Web Application Server)의 역할
- WAS = Web Server + Web Container
- Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시되었다.
- 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.
- 주로 DB 서버와 같이 수행된다.
- 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는데 있어서 성능상 큰 차이가 없다.

<br>

8. WAS(Web Application Server)의 종류

Tomcat, JBoss, Jeus, Web Sphere 등

<br>

9. Tomcat(톰캣)이란?

![Untitled](Web%20Server(%E1%84%8B%E1%85%B0%E1%86%B8%E1%84%89%E1%85%A5%E1%84%87%E1%85%A5,%20%E1%84%8B%E1%85%A1%E1%84%91%E1%85%A1%E1%84%8E%E1%85%B5)%E1%84%8B%E1%85%AA%20WAS(%E1%84%90%E1%85%A9%E1%86%B7%E1%84%8F%E1%85%A2%E1%86%BA)%20ece48311a0624869b1f64285d08308ff/Untitled%203.png)

동적인 데이터를 처리, DB와 연결되어 데이터를 주고 받거나 프로그램으로 데이터 조작이 필요한 경우에 사용, Apache Tomcat(이하 Tomcat)은 JSP 페이지의 실행 환경을 제공하는 웹 애플리케이션 서버(WAS)

- 톰캣은 ‘WAS(Web Application Server)’라고 해서 자바코드를 이용해 HTML 페이지를 동적으로 생성해주는 프로그램
- WAS는 웹 서버와 웹 컨테이너의 결합으로 다양한 기능을 컨테이너에 구현하여 다양한 역할을 수행할 수 있는 서버
- 클라이언트의 요청이 있을 때 내부의 프로그램을 통해 결과를 만들어내고 이것을 다시 클라이언트에 전달해주는 역할을 하는 것이 웹 컨테이너
- 아파치와 톰캣은 컨테이너 기능이 가능하냐 하지 않느냐의 차이가 있음
- 톰캣 6버전 이상부터는 조금씩 웹 서버의 기능이 추가되어서 현재는 톰캣만 설치해도 어느 정도의 웹 서버 역할이 가능
- 아직도 많은 JSP를 사용하는 웹 프로그래머들은 Apache + Tomcat을 병행해서 사용. 그 이유는 정적 데이터를 처리할 때 아파치의 성능이 더 좋음
- 톰캣도 좋아지고 있지만 이미지나 CSS 같은 정적 데이터는 아파치에서 처리하고, 톰캣은 본 목적인 동적 페이지 생성에 주력하는게 효율면에서 좋음


<br><br>

***Apache(웹 서버)를 같이 쓰는 이유?***

- 하나의 웹 서버에서 다른 언어의 어플리케이션을 함께 사용할 경우
- 로드밸런싱이 필요한 경우 - 특정 서버에서 에러/과부하가 발생할 경우 다른 서버가 정상 작동
- 보안을 강화할 경우 - 아파치에서 해킹 당해도 WAS는 정상 작동
