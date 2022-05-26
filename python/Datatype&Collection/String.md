# String

```python
String = "abcdefg"
```



#### String replace

한 문자만 바꾸고 싶을 때

```python
str.replace('바꿀 헌 문자','새 문자','바꾸는 횟수')
```

여러 문자를 바꾸고 싶을 때

```python
import re

text = "testnumberone1234567890"
text = re.sub('[0-9]', 'X', text)
print(txt) # testnumberone
```

참고 : <https://wikidocs.net/13>

참고하면서 쓸 때 작성할 계획입니다!