# HashTable

#### **해시 함수**

임의 크기 데이터를 고정 크기 값으로 매핑하는데 사용하는 함수

 성능이 좋은 해시 함수란?

- 충돌이 적은 해시 함수
- 쉽고 빠른 연산
- 해시 테이블에 고루 퍼져 있어야 한다

#### 로드 팩터 

테이블에 저장된 데이터 개수 n을 버킷의 개수 k로 나눈 것 - *공실률*

load factor = n/k

로드 팩터가 증가하면 해시 테이블 성능은 감소한다



#### 해시 함수

키 : 우리가 넣어야 할 값

해시 : 키를 해시 함수로 재구성한 것

가장 간단한 연산 : h(x) = x mod m

2의 제곱에 가깝지 않은 소수를 정하는 것이 좋다



#### 해시 테이블

1. 해시 값을 계산한다(ex : mod 연산)

2. 해시 값을 이용해 배열의 인덱스를 구한다

3. 같은 인덱스가 있다면 연결 리스트를 이어준다



#### 오픈 어드레싱

해싱 값에 다른 값이 이미 할당되어 있을 때(충돌)

빈 공간을 찾기 위해 타겟으로 선형 탐사를 진행한다 

- 단점 : 특정 공간에 값들이 뭉쳐진다(Clustering)



#### 개별 체이닝

해싱 값이 다른 값이 할당되었을 때(충돌) 해당 인덱스에 연결 리스트로 연결한다



#### 파이썬의 해싱 방법 : 오픈 어드레싱 

Dictionary에 HashTable(Open Addressing)을 사용한다

이유

- 체이닝 시 메모리 할당 오버헤드가 높다

- 오픈 어드레싱의 선형 탐사 방식은 체이닝에 비해 성능이 더 좋지만, 80%가 찰 경우 성능 저하가 뚜렷하다
  - 그래서 오픈 어드레싱 방식을 채택하고, 로드 펙터를 적게 잡는다

![image](https://user-images.githubusercontent.com/17975647/168940269-05e2b5f0-9b0a-4059-a652-52123b885e50.png)



### 구현

