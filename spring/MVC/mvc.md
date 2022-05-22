## MVC

하나의 서블릿이나, JSP로 처리하던 것을 Controller와 View라는 영역으로 서로 역할을 나눈 것

### Controller

HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다. 그리고 뷰에 전달할 결과 데이터를 조회해서 모델에 담는다.



### Model

뷰에 전달한 데이터를 담아 둔다



### View

모델에 담긴 값을 참고하여 화면(HTML)을 그린다.



![파일_000](https://user-images.githubusercontent.com/17975647/168481672-6b7b7b9d-832e-4359-ad53-3e53eeca9dd2.png)

### Redirect와 forward

Redirect는 클라이언트에 응답이 나갔다가, redirect 경로로 다시 요청한다.

Foward는 서버 내부에서 일어나기 때문에 클라이언트가 인지하지 못한다.



### Adapter Pattern

프론트 컨트롤러는 한 가지 방식의 컨트롤러 인터페이스만 사용한다

**핸들러 어댑터** : 중간에 어댑터가 추가되어 다양한 종류의 컨트롤러를 호출할 수 있다.

핸들러 : 컨트롤러의 이름을 더넓은 범위인 핸들러로 변경했다. 그 이유는 어댑터가 있기 때문에 컨트롤러의 개념 뿐만 아니라 어떤 것이든 해당하는 종류의 어댑터만 있으면 다 처리할 수 있기 때문이다.



### 강의를 들으며 정리하는 구현 순서 정리하기

- **myView**
  - jsp의 경로 설정
- **ModelView**
	 - viewName(String) 과 model(Map<String, Object>를 변수로 가지며 Constructor, Getter, Setter로 이루어진 객체
	

#### **FrontController를 이용한 구현**

1. Controller Inteface 생성
   -  process 함수를 선언한다 : request, response를 받아서 처리	
2. Controller package를 생성해 내부에 (form, list, save와 같은) Controller를 생성한다
3. HttpServlet을 상속받는 FrontControllerServlet을 구현한다 (protected service overriding 필요)

HandlerAdapter 추가

1. MyHandlerAdapter Interface 생성

2. MyHandlerAdapter를 상속받아 각 버전에 맞는 ControllerHandlerAdapter를 구현

3. HttpServlet을 상속받는 FrontControllerServlet 구현 (protected service overriding 필요)
   - Map<String, Object> handlerMappingMap : <Uri, Object> 를 가지는 Map
   
   - List<MyHandlerAdapter> handlerAdapters : ControllerHandlerAdapter를 담을 리스트
   
     

