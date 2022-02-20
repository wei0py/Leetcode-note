## Day 8 Stack

Stack in Python:
- A stack is a linear data structure that stores items in a Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) manner. In stack, a new element is added at one end and an element is removed from that end only. The insert and delete operations are often called push and pop.
- There are various ways from which a stack can be implemented in Python. 1. list 2. Collections.deque 3. queue.LifoQueue
- Python stack can be implemented using the deque class from the collections module. Deque is preferred over the list in the cases where we need quicker append and pop operations from both the ends of the container, as deque provides an O(1) time complexity for append and pop operations as compared to list which provides O(n) time complexity. 

### Leetcode 155. Min Stack (follow up
```python
class MinStack:

    def __init__(self):
        self.stack = collections.deque()
        
    def push(self, val: int) -> None:
        if not self.stack:
            self.min = val
        self.stack.append(val)
        self.min = min(self.min, val)

    def pop(self) -> None:
        self.stack.pop()
        if self.stack:
            self.min = min(self.stack)
        
    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min
```
Another idea, use a tuple to store the min at each time, or use another stack to store the min.
```python
class MinStack(object):

def __init__(self):
    """
    initialize your data structure here.
    """
    self.stack= []

def push(self, x):
    """
    :type x: int
    :rtype: nothing
    """
    if not self.stack:self.stack.append((x,x)) 
    else:
       self.stack.append((x,min(x,self.stack[-1][1])))

def pop(self):
    """
    :rtype: nothing
    """
    if self.stack: self.stack.pop()

def top(self):
    """
    :rtype: int
    """
    if self.stack: return self.stack[-1][0]
    else: return None

def getMin(self):
    """
    :rtype: int
    """
    if self.stack: return self.stack[-1][1]
    else: return None
```
### Leetcode 716 Max Stack)
### Leetcode 232. Implement Queue using Stacks
### Leetcode 150. Evaluate Reverse Polish Notation
Using stack, and when considering the operation, we can deal with them separately, or using eval, or using operator.
```python
import operator
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        ops = {
    '+' : operator.add,
    '-' : operator.sub,
    '*' : operator.mul,
    '/' : operator.truediv,
}
        stack = []
        output = 0
        for i in tokens:
            if i not in ops.keys():
                stack.append(int(i))
            else:
                a = stack.pop()
                b = stack.pop()
                c = int(ops[i](b,a))
                stack.append(c)
        return stack[0]
```
### Leetcode 224. Basic Calculator II (I, II, III, IV)
### Leetcode 20. Valid Parentheses
```python
class Solution:
    # @return a boolean
    def isValid(self, s):
        stack = []
        dict = {"]":"[", "}":"{", ")":"("}
        for char in s:
            if char in dict.values():
                stack.append(char)
            elif char in dict.keys():
                if stack == [] or dict[char] != stack.pop():
                    return False
            else:
                return False
        return stack == []
```

### Leetcode 1472. Design Browser History
### Leetcode 1209. Remove All Adjacent Duplicates in String II
### Leetcode 1249. Minimum Remove to Make Valid Parentheses
### Leetcode 735. Asteroid Collision
