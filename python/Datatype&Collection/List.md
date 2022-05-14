# LIST



### 파이썬 리스트 형식

```python
intList = [1, 2, 3, 4, 5]
strList = ["jsoi", "name", "jeong"]
```



#### 초기화, 선언
``` python
list1 = list() # []
list = [1,2,3,4,5]
```



#### 리스트와 연산자

``` python
list = [3] * 3 # [3,3,3]
list = [1,2,3]+[4,5,6] # [1,2,3,4,5,6]
```



#### 값 하나 읽어오기

```python
a = [0,1,2,3]
b = [0,1,2,[0,1]] # 이렇게 리스트 안에 리스트를 넣을 수도 있다!
a[index] # index번째의 값
a[-1] # 마지막 요소값
b[3] # 3번째 요소인 [0,1]
b[3,0] # [0,1] 중 첫 번째 원소인 0
```



#### Slicing

```python
a = [0,1,2,3,4,5]
b = a[0:2] # 0포함 ~ 2 직전까지 슬라이싱
c = a[2:] # 2번째 인덱스부터 마지막 인덱스까지 슬라이싱
```




#### 추가
```python
list.append(x)
# list의 마지막에 x 추가
```



#### 값 삭제

```python
list.remove(x)
# 첫 번째로 나오는 x를 삭제_값으로 삭제
```



#### 인덱스로 삭제

```python
del list[index]
# index번째의 요소 삭제
del a[2:]
# 슬라이싱 기법을 이용해 삭제
```



#### 추가

```python
list.insert(a,b)
# a번째에 b요소를 추가
```



#### 마지막 요소 삭제 & 반환

```python
list.pop()
# 맨 마지막 요소를 삭제하고 리턴
```



#### 개수 세기

```python
list.count(a)
# a가 몇 번 나오는지 리턴
```



#### 리스트 확장

```python
list.extend([a,b]) # list += [a,b] 와 동일
# list에 다른 리스트를 추가
```

