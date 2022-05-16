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