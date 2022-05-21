# Itertools



### Permutation

```python
from itertools import permutations

list = ['A', 'B', 'C']
data = itertools.permutation(list, 2)
```

### Combination

```python
from itertools import combinations

list = ['A', 'B', 'C']
data = itertools.combinations(list, 2)
```

### Permutation with Repetition

```python
from itertools import product

list = ['A', 'B', 'C']
data = itertools.product(sets, repeat = 2) # 2개를 뽑는다
```

### Combination with Repetition

```python
from itertools import combinationswith_replacement

list = ['A', 'B', 'C']
data = itertools.combinations_with_replacement(sets, repeat = 2) # 2개를 뽑는다
```

