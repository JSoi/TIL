## Sorting

참 많이 쓰는 Sort

하지만 헷갈려서 다시 정리한다



#### Dictionary

키 값을 중심으로 정렬하기





value값

함수로 정렬하기

```python
dic = {'b':2, 'a':1, 'c':3}

def func(x):

	return x[1]

result_func = sorted(dic.items(),key=func)

print(result_func) # {'a' : 1, 'b' : 2, 'c' : 3}
```

// 실행 시 
```python
result = sorted(dic.items(),key=(lambda x:x[1]),reverse=True)
```