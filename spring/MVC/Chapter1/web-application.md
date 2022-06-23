## 웹 어플리케이션의 이해



#### WS(웹 서버)

HTTP 기반으로 동작
정적 리소스 제공, 기타 부가기능
HTTP를 요청하면 HTTP Protocol로 응답한다



#### WAS(웹 어플리케이션 서버)

HTTP기반 동작, 정적 리소스 제공(WS 역할 수행)
프로그램 코드를 실행해서 애플리케이션 로직 수행
Servlet,  JSP, Spring MVC
ex) Tomcat Jetty



#### WS / WAS 차이
웹 서버는 정적리소스, WAS는 애플리케이션 로직



#### 웹 시스템 구성
WAS가 너무 많은 역할을 담당해서 서버 과부하가 우려된다.
-> WS를 WAS 앞에 두어 정적 리소스를 처리하고, 동적인 처리는 WAS가 한다

>Client --- Web Server --- Web Application Server --- DB

WAS는 쉽게 다운된다!<br>(bc. 애플리케이션 로직 수행이 과부하가 잘 걸린다)

- 만약 API만 설계한다면 ? : WAS 만 사용하기도 한다



### Servlet
```java
@WebServlet(name='helloServlet',urlPatterns="/hello")
public class HelloServlet extends HttpServlet {
    @Override
    protected void service (HttpServletRequest request, HttpServletResponse response){
        // 애플리케이션 로직
    }
}
```

- urlPatterns('hello') 실행시 서블릿 코드가 실행됨

- __HttpServletRequest__ : HTTP Request를 편하게 사용할 수 있음

- __HttpServletResponse__ : HTTP Response를 편하게 사용할 수 있음



#### HTTP 요청시 

- WAS는 `Request`, `Response`객체를 생성
- 개발자는 `Request`, `Response`객체에서 값을 꺼내서 사용
- `Response`객체에 HTTP 응답 정보를 편리하게 입력
- WAS는 `Response`객체에 담겨있는 내용으로 HTTP 응답 정보를 생성



#### Servlet Container

WAS 안에는 Servlet Container가 존재한다

Sevlet이 여러 개 있으면 Servlet의 __생명주기__를 Servlet Container가 관리한다

**서블릿 객체는 싱글톤**으로 관리된다.

- 최초 로딩 시점에 Servlet 객체를 미리 만들고 재활용한다.

- 모든 클라이언트 요청은 서블릿 객체 인스턴스에 접근한다 :point_right: 그러므로 공유 변수 사용을 주의해야 한다

- 서블릿 컨테이너 종료시 같이 종료된다

JSP 역시 서블릿으로 변환된다

동시 요청을 위한 **<u>멀티 쓰레드 처리</u>**를 지원한다



### 동시 요청 - 멀티 쓰레드 :star:

#### Thread

애플리케이션 코드를 순차적으로 실행 - **Line By Line**

ex ) java 실행 시 main Thread  실행

> Client --- [ Connection) :point_right: **Thread** (Servlet 객체 생성) :point_right: WAS]

만약에 하나의 쓰레드로만 동시 요청을 Cover한다면, 하나의 요청이 실행되지 못할 때 모든 Request가 죽어버린다

-> Request 마다 Thread를 생성하자!

* :disappointed: Thread 비용은 비싸며, Context Switching의 발생 비용이 높다
* :disappointed: 너무 많은 요청이 오면, 서버가 죽을 수 있다



#### Thread Pool

WAS 내부에 있는 **Thread Pool**의 Thread를 갖다 <u>쓰고,</u> 사용이 끝나면 Thread Pool에 <u>반환</u>한다

Thread Pool이 가득 차거나 없으면 **대기**, **거절**을 한다

* :happy: 쓰레드 생성/종료 비용이 절약되며, 응답 시간이 빠르다
* :happy: 생성 쓰레드 최대치(Max Thread)가 있으므로 많은 요청이 들어와도 기존 요청은 안전하게 처리한다

Max Thread

- 너무 낮게 설정시 : CPU 사용률이 현저히 낮게 된다. Thread들이 거절/대기된다
- 너무 높게 설정시 : CPU, 메모리 리소스 임계점 초과로 서버 다운
- 적정 숫자를 찾는 법 : 로직의 복잡도, CPU, 메모리, IO 리소스 상황에 다르다 & **성능 테스트** with Apache ab, nGrinder



#### 이 멀티 쓰레드 문제를 WAS가 처리해준다 :happy:

-> 싱글톤 객체(Spring Bean)는 주의하자!



#### 정적 리소스

HTML, CSS, JS, 이미지, 파일



#### 동적 페이지

HTML을 동적으로 생성해서 전달



#### HTTP API

주로 JSON 형태로 데이터 통신

- WebClient - Server
- Web Browser - Server
- AppClient - Server
- Server - Server (주문 서버 - 결제 서버 / 기업 - 기업)



#### SSR - 서버 사이드 렌더링

- 서버에서 HTML을 생성해서 클라이언트에 전달한다

ex) JSP, Thymeleaf



#### CSR - 클라이언트 사이드 렌더링

- 자바스크립트를 이용해서 **웹 브라우저**에서 동적으로 생성해서 적용

ex) 구글 지도, Gmail



#### 자바 웹 기술

Spring MVC(어노테이션 기반) -> Spring Boot(서버 내장, 빌드 결과에 WAS 서버 포함!)



#### 자바 뷰 템플릿(HTML 생성)

 Freemarker, Velocity >>> **ThymeLeaf**  >>> JSP

이 중 Thymeleaf 가 Spring MVC에 적합하다
