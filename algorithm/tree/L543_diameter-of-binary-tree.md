## Diameter of Binary Tree

#### 문제

이진 트리가 주어졌을 때, 두 노드 간 가장 긴  경로의 길이를 출력하라

----

합도, 리프 노드까지의 거리도 재귀적으로 찾아야 한다.

재귀에서 가장 중요한 종료 조건 : 현재 노드가 None일때 리프노드를 출력하기 위해 -1을 반환한다

-1을 반환하는 것은 다른 문제를 풀 때도 많이 사용되는 것 같다.

```python
def diameterOfBinaryTree(self, root):
    self.ans = 0

    def height(p):
        if not p: return -1 #리프 노드일 경우 -1 반환
        left, right = height(p.left), height(p.right)
        self.ans = max(self.ans, 2 + left + right)
        return 1 + max(left, right)

    height(root)
    return self.ans
```



