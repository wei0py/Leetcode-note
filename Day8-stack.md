## Day 8 Stack

Stack in Python:
- A stack is a linear data structure that stores items in a Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) manner. In stack, a new element is added at one end and an element is removed from that end only. The insert and delete operations are often called push and pop.
- There are various ways from which a stack can be implemented in Python. 1. list 2. Collections.deque 3. queue.LifoQueue
- Python stack can be implemented using the deque class from the collections module. Deque is preferred over the list in the cases where we need quicker append and pop operations from both the ends of the container, as deque provides an O(1) time complexity for append and pop operations as compared to list which provides O(n) time complexity. 

### Leetcode 155. Min Stack (follow up
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
