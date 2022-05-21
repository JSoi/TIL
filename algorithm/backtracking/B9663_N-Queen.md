# 백준 9663

정말 유명한 백트래킹 대표 문제이다

<https://www.acmicpc.net/problem/9663>

## 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

## 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.



## 입력

```
8
```

## 출력

```
92
```



------

### <필요한 변수>

#### board[행] = 열

일차원 배열을 생성해준다. 이런 체스판이 나오면 좋아라 하고 2차원 배열 생성하는데.. TLE도 그렇고 머리도 꼬인다

#### count

우리가 리턴해야 할 변수! 퀸을 놓는 경우의 수이다

#### visited[열]:cry:

해당 열을 다른 퀸이 방문했는지 체크한다.

이를 통해 반복문의 수행을 줄여 TLE를 방지할 수 있다.



### <코드의 흐름>

무조건 0행부터 시작해야 한다. 모든 퀸이 들어가는 경우의 수는 모든 행, 열이 차 있어야 만족된다



### 소스 코드

```python
# N-Queen
# https://www.acmicpc.net/problem/9663
N = int(input())
board = [-1] * N
count = 0
visited = [False] * N  # 열 방문 여부 저장


def go(row):
    if row >= N:  # 다 끝낸 것 - 정답 중 하나이다
        global count
        count += 1
        return
    # 다음으로 진행 필요
    for col in range(N):
        if visited[col]:
            continue
        board[row] = col
        if is_ok(row):
            visited[col] = True
            go(row + 1)
            visited[col] = False


def is_ok(check_row):  # 해당 행이 유효한지 검사함
    for each_row in range(check_row):
        if board[each_row] == board[check_row] or abs(check_row - each_row) == abs(board[check_row] - board[each_row]):
            return False
    return True


go(0)
print(count)
```



