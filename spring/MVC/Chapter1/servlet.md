# Servlet



## Request

#### 1. GET :

   - /url?username=hello&age=20

   - 검색, 필터 페이징에서 많이 쓰임

#### 2. POST : HTML Form

   - content-type:application/x-www-form-urlencoded

   - 메시지 바디에 쿼리 파라미터 형식으로 전달

#### 3. HTTP Message Body에 데이터를 담아서 요청한다

   - HTTP API에서 주로 사용 (**JSON**, XML, TEXT)

   - POST, PUT, PATCH



## Response



### 1. 단순 텍스트 응답

```java
@WebServlet(name = "reponseHeaderServlet", urlPatterns = "/response-header")
public class ResponseHeaderServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request,HttpServletResponse response) throws ServletException, IOException {
        //[status-line]
        response.setStatus(HttpServletResponse.SC_OK);// http 응답코드
        response.setHeader("Cache-control", "no-cache, no-store, must-validate");
        response.setHeader("Pragma", "no-cache");
        response.setHeader("my-header", "hello");

        // Content 설정
        response.setContentType("text/plain");
        response.setCharacterEncoding("utf-8")
		
        // Cookie 설정
        Cookie cookie = new Cookie("myCookie", "good");
	    cookie.setMaxAge(600);
    	response.addCookie(cookie);
        
        // Redirect
        response.sendRedirect("/basic/hello-form.html");
        
        PrintWriter writer = response.getWriter();
        writer.println("안녕하세요");

    }
```



### 2. HTML 응답
```java
@WebServlet(name="responseHtmlServlet", urlPatterns = "/response-html")
public class ResponseHtmlServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Content-Type: text/html; charset=utf-8
        response.setContentType("text/html");
        response.setCharacterEncoding("utf-8");

        PrintWriter writer = response.getWriter();
        writer.println("<html>");
        writer.println("<body>");
        writer.println("    <div>안녕</div>");
        writer.println("</body>");
        writer.println("</html>");
    }
}
```



### 3. JSON 응답

```java
@WebServlet(name = "responseJsonServlet", urlPatterns = "/response-json")
public class ResponseJsonServlet extends HttpServlet {
    private ObjectMapper objectMapper = new ObjectMapper();
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("application/json");
        response.setCharacterEncoding("utf-8");

        HelloData helloData = new HelloData();
        helloData.setAge(20);
        helloData.setUsername("홍길동");

        String result = objectMapper.writeValueAsString(helloData);
        // Jackson lib가 제공하는 writeValueAsString 쓰기
        response.getWriter().write(result);
    }
}

```