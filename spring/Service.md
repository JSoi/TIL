# Service

Service 객체는 비즈니스 로직이 모여있다.

비즈니스 로직을 설명하라면 좀 벙찔 것 같긴 한데, 그래도 두루뭉술하게 서술하자면 유저가 필요로 하는 요구사항을 구현한 것 같다.



> 이미 저장된 회원의 비밀번호를 바꾸고 싶어요!

그래.. 바꿀게

Service : update(ID, 바꾸고자 하는 비밀번호)

Repository : ID를 조회



뜬금없지만 Repository와 Service에 대해 좀..알아보자

Repository와 Service는 인접한 계층이기 떄문에 분리하는 기준이 항상 애매한 것 같다.

Repository에는 DB에 접근하는 모든 코드가 모여있다.

service 패키지는 DB에 접근하는 코드는 repository에 위임하고, 비즈니스 로직과 관련된 모든 코드가 모여있다.

이렇게 구분해두면 비즈니스 로직과 관련된 부분에 문제가 발생했을 때는 service 패키지를 확인하고, DB 접근과 관련된 문제가 발생하면 repository 부분을 확인하게 된다고 한다.



## 참조

비즈니스 로직

https://matthew.kr/%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%8A%94-%EB%B9%84%EC%A6%88%EB%8B%88%EC%8A%A4-%EB%A1%9C%EC%A7%81%EC%9D%84-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%9C%EB%8B%A4/