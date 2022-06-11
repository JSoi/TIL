## MVC - 기본 기능

#### Logging

```java
@Slf4j
@RestController
public class LogTestController {
    
// private final Logger log = LoggerFactory.getLogger(getClass());

...
log.trace("trace log = {}", name);
    // +를 사용하지 말아야 한다. 연산이 발생하면서 리소스가 낭비된다
log.debug("debug log = {}", name);
log.info("info log = {}", name);
log.warn("warn log = {}", name);
log.error("error log = {}", name);
```

```
# application.properties
# hello.springmvc 패키지와 그 하위 로그 레벨 설정
logging.level.hello.mvc=debug
```

**레벨 : TRACE > DEBUG > INFO(default) > WARN > ERROR**

----

### @RestController

 viewname 이 아닌 값을 전달받게 된다.

controller는 반환 값이 String이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰를 렌더링 하게 되는데

RestController는 반환 값으로 뷰를 찾는 것이 아니라 HTTP 메시지 바디에 바로 입력한다.



### @ResponseBody

View 조회를 무시하고, HTTPBody에 직접 해당 내용을 입력한다



### @RequestParam

```java
public String requestParamV3(
@RequestParam String username, // 파라미터 이름이 변수 이름과 같으면 @ReuestParam 생략가능
@RequestParam int age) {
```

```@RequestParam(required = false)``` (default)

```@RequestParam(required = true)``` 시 빈 값이 들어가면 400 예외 발생



``@RequestParam(required = false) int age`` 에서 null을 int에 입력하게 되면 500에외 발생

👉 이를 방지하기 위해 Integer로 변경 혹은 defaultValue를 사용한다.

```@RequestParam(required = false, defaultValue = "-1") int age```를 통해 빈 문자를 입력받아도 -1이 입력되게 한다. (사실 defaultValue를사용하게 되면 required가 큰 의미가 없어짐)



```java
@ResponseBody
@RequestMapping("/request-param-map")
public String requestParamMap(@RequestParam Map<String, Object> paramMap) {
    log.info("username-{}, age={}", paramMap.get("username"), paramMap.get("age"));
    return "ok";
}
```

파라미터의 값이 2개 이상인 것 같다면 **MultiValueMap**을 사용해야 한다.

MultiValueMap은 ```key=[value1,value2]``` 형식으로 되어 있으며

> ?userIds=id1&userIds=id2

형식으로 들어오면 MultiValueMap을 사용하면 된다.(많이 안쓴다고..한다)





@ModelAttribute

객체를 생성해서 요청 파라미터의 이름으로 



----

정리

HTTP  요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법을 알아보자

1. GET

   - ```/url?username=hello&age=20```

   - 메시지 바디 없이, url 쿼리 파라미터에 데이터를 포함해 전달

   - 검색, 필터, 페이징에서 많이 사용

2. POST - HTML Form

   - content-type : application/x-www-form-urlencoded
   - 메시지 바디에 쿼리 파라미터 형식으로 전달
   - 회원가입, 상품 주문, HTML Form

3. HTTP Message Body

   - HTTP API에서 많이 사용, JSON / XML / TEXT
   - 데이터 형식은 주로 JSON
   - POST, PUT, PATCH



### HTTP 요청 메시지 - TEXT

```java
public HttpEntity<String> requestBodyString(HttpEntity<String> httpEntity) throws IOException{
    String body = httpEntity.getBody();
    log.info("messageBody : {}", body);
    return new HttpEntity<>("ok");
}
```

#### HttpEntity

Http Header, Body 정보를 조회

요청 파라미터를 조회하지않음

응답에도 사용 가능(바디 & 헤더)

HttpMessageConverter가 바꿔주는 것!



HttpEntity를 상속받은 것 - ResponseEntity, RequestEntity



#### @ResponseBody

헤더 정보를 조회하기 위해서는 HttpEntity, RequestHeader를 사용하자

응답결과를 body에 담아준다





#### 정적 리소스

/static , /public, /resources, /META-INF/resources 등

스프링 부트가 파일을 변경 없이 서비스하는 것이다.
