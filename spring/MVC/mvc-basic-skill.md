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
