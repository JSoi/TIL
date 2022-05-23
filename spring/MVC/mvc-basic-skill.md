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

**RestController** : viewname 이 아닌 값을 전달받게 된다.

controller는 반환 값이 String이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰를 렌더링 하게 되는데

RestController는 반환 값으로 뷰를 찾는 것이 아니라 HTTP 메시지 바디에 바로 입력한다.

