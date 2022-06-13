# Filter

스프링과 무관한 서블릿 컴포넌트(톰캣 같은 웹 컨테이너가 관리하는 것이다!)

Request, Response 객체가 필터를 거친다



#### 생명주기

> init() 👉doFilter() 👉 destroy()



디스패처 서블릿(Dispatcher Servlet)에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가작업을 처리할 수 있는 기능을 제공



### init

반드시 구현해야 하며, config 객체를 저장한다

필터 객체를 초기화하고 서비스에 추가하기 위한 메소드이다.

웹 컨테이너가 1회 init 메소드를 호출하여 필터 객체를 초기화하면 이후의 요청들은 doFilter를 통해 처리된다.

```java
public void init(FilterConfig config) throws ServletException{
	this.filterConfig = config;
}
```



### doFilter

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException{
    ...
        chain.doFilter(request,response); // 다음에 실행될 필터 또는 서블릿을 호출하는 것!
}
```

doFilter 메소드는 url-pattern에 맞는 모든 HTTP 요청이 디스패처 서블릿으로 전달되기 전에 웹 컨테이너에 의해 실행되는 메소드이다.

doFilter의 파라미터로는 FilterChain이 있는데, FilterChain의 doFilter 통해 다음 대상으로 요청을 전달하게 된다.

chain.doFilter() 전/후에 우리가 필요한 처리 과정을 넣어줌으로써 원하는 처리를 진행할 수 있다.



오 실습 때 했던 서블릿 코드와 거의 똑같다! 와~~ 매개변수에 FilterChain만 추가했다!

```java
@WebServlet(name = "helloServlet", urlPatterns = "/hello")
public class HelloServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        ...
            response.getWriter().write("hello " + username);
}
```

쪼금 찾아보니까 HTTP 등장 후 Web Container에서 HttpServletRequest를 사용했다고 한다



### destroy

destroy 메소드는 필터 객체를 서비스에서 제거하고 사용하는 자원을 반환하기 위한 메소드이다.

이는 웹 컨테이너에 의해 1번 호출되며 이후에는 이제 doFilter에 의해 처리되지 않는다.





## Wrapper

doFilter에서 봤듯이 필터를 하려면 ServletRequest, ServletResponse를 받아서 처리해야 한다.

Response는 예전에 서블릿 코드 예제에서 작성한 ```response.getWriter().write("hello " + username);``` 와 같이 OutputStreamWriter 객체를 참조한다.

이를 클라이언트에 전달하기 때문에 필터에서는 response 객체에 접근할 수 없다.

그래서 필터가 기존 Request, Response에 포장을 해서 진짜 Response 대신 자신이 꾸민 Response를 전달하게 된다.

```java
public class MyWrapper extends HttpServletResponseWrapper{
    public MyWrapper(HttpServletResponse response){ // 매개변수는 꼭 HttpServletResponse로!
        super(response);
    }
    
    public void myMethod(){..}
}
```







## 참고

https://mangkyu.tistory.com/173

<https://webfirewoord.tistory.com/58>