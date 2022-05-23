## 스프링 MVC - 구조 이해

**HandlerMapping**

핸들러 매핑에서 이 컨트롤러를 찾을 수 있어야 한다.

*<u>RequestMappingHandlerMapping</u>* : 애노테이션  기반의 컨트롤러인 @RequestMapping에서 사용

*BeanNameUrlHandlerMapping* : 스프링 빈의 이름으로 핸들러를 찾음

**HandlerAdpater**

핸들러 매핑을 통해서 찾은 핸들러를 실행할 수 있는 핸들러 어댑터가 필요한다.

Controller 인터페이스를 실행할 수 있는 핸들러 어댑터를 찾고 실행해야 한다.

*<u>RequestMappingHandlerAdapter</u>* : 애노테이션 기반의 컨트롤러인 @RequestMapping에서 사용

*HttpRequestHandlerAdapter* : HttpRequestHandler 처리

*SimpleControllerHandlerAdapter*: Controller 인터페이스 처리

**@RequestMapping**

- RequestMappingHandlerMapping
- requestMappingHandlerAdapter

애노테이션 기반의 컨트로럴를 지원하는 핸드럴 매핑과 어댑터이다

@RequestMapping기반의 MVC패턴 만들어보자

**@Controller**

- 스프링이 자동으로 스프링 빈으로 등록한다.
- 스프링 MVC에서 애노테이션 기반 컨트롤러로 인식한다

@Component : 컴포넌트 스캔의 대상이 되어서 자동으로 빈으로 등록됨

(@Controller안에 @Component 포함되어있다)

**@RequestMapping**

요청 정보를 매핑한다. 애노테이션을 기반으로 동작하기 때문에, 메서드 내임은 임의로 지으면 된다.

RequestMappingHandlerMapping은 스프링 빈 중에서 @RequestMapping 또는 @Controller가 클래스 레벨에 붙어 있는 경우 매핑 정보로 인식한다.

