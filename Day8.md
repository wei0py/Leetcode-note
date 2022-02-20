## Day 8
### Leetcode 155. Min Stack (follow up
### Leetcode 716 Max Stack)
### Leetcode 232. Implement Queue using Stacks
### Leetcode 150. Evaluate Reverse Polish Notation
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
