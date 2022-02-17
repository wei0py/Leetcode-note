### Day7

##  Leetcode 225. Implement Stack using Queues
```python
class Stack:
    def __init__(self):
        self._queue = collections.deque()

    def push(self, x):
        q = self._queue
        q.append(x)
        for _ in range(len(q) - 1):
            q.append(q.popleft())
        
    def pop(self):
        return self._queue.popleft()

    def top(self):
        return self._queue[0]
    
    def empty(self):
        return not len(self._queue)
```
## Leetcode 346. Moving Average from Data Stream
## Leetcode 281. Zigzag Iterator
## Leetcode 1429. First Unique Number
## Leetcode 54. Spiral Matrix
```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        if len(matrix) == 0: return res
        
        row_begin = col_begin = 0
        row_end = len(matrix) - 1 
        col_end = len(matrix[0]) - 1
        
        while (row_begin <= row_end and col_begin <= col_end):
            res += [matrix[row_begin][col] for col in range(col_begin, col_end + 1)]
            row_begin += 1
            res += [matrix[row][col_end] for row in range(row_begin, row_end + 1)]
            col_end -= 1
            
            if (row_begin <= row_end):
                res += [matrix[row_end][col] for col in range(col_end, col_begin - 1, -1)]
                row_end -= 1
                
            if (col_begin <= col_end):
                res += [matrix[row][col_begin] for row in range(row_end, row_begin - 1, -1)]
                col_begin += 1
        
        return res
```

## Leetcode 362. Design Hit Counter
