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
## Leetcode 362. Design Hit Counter
