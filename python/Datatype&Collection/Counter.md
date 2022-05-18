## Counter

Python에서 빈도수를 저장하는 collection 객체이다!



### 선언 방법
```python
import collections
example = collections.Counter("Don't blame me")
print(list(example.elements())) # 최빈값 3개 반환
```



### 최빈값 꺼내오기

```python
import collections
example = ["jsoi","is","studying","good","good"]
example_counter = collections.Counter(example)
print(example_counter.most_common()) # 요소 전체 반환
print(example_counter.most_common(1)) # 최빈값 1개 반환
print(example_counter.most_common(3)) # 최빈값 3개 반환
```



### 덧셈 연산

```python
ex1 = collections.Counter('hi')
ex2 = collections.Counter('ho')

print(ex1 + ex2) # 출력시 {'h':2, 'i':1,o':1}
```



### 뺄셈 연산
```python
ex1 = collections.Counter('hello')
ex2 = collections.Counter('hell')

print(ex1 - ex2) # 출력시 {'o':1}
```



### 교집합/합집합

```python
ex1 = collections.Counter('ab')
ex2 = collections.Counter('bc')

print(ex1 | ex2) # 출력시 {'a':1, 'b':1, 'c':1}
print(ex1 & ex2) # 출력시 {'b':1}
```