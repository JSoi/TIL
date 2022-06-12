# RestControllerAdvice

@ExceptionHandler, @ModelAttribute, @InitBinder 가 적용된 메서드들을 AOP를 적용해 컨트롤러 단에 적용하기 위해 고안된 애너테이션이다.

**@ControllerAdvice**와 **@ResponseBody**를 합친 것!

👉 그렇기 때문에 View가 아닌 값(JSON, String)을 반환하게 될 것이다



### 목적

- 프로젝트 전역에 걸쳐 존재하는 Exception을 처리하고 싶을 때

- 입맛대로 Response를 반환하고 싶을 때 :yum:



### 구현 순서

1. 나만의 Exception을 만들자! (사실 직접 구현한 Exception 아니어도 상관은 없다 ^^)..!

   ```java
   @Getter
   public class EmptyException extends RuntimeException {
       private ErrorCode code;
   
       public EmptyException(ErrorCode code) {
           super(code.toString());
           this.code = code;
       }
   }
   ```

2. ResponseEntityExceptionHandler를 상속받는 클래스 구현 (이게 RestControllerAdvice)

   ```java
   @RestControllerAdvice(basePackages = "com.jsoi.myblog.controller") // AOP 타겟이 되는 패키지를 설정
   public class RequestException extends ResponseEntityExceptionHandler {
       @ExceptionHandler(MyException.class) //    @ExceptionHandler(value={A.class, B.class}) 도 사용가능
       protected ExceptionMessage handleDataException(MyException myException) {
           return new ExceptionMessage(myException.getCode().getDesc());
       }
   }
   ```
   








--------

#### 참고 사이트

https://www.bezkoder.com/spring-boot-restcontrolleradvice/#RestControllerAdvice_with_ResponseEntity

<https://javachoi.tistory.com/253>

<https://mangkyu.tistory.com/205>