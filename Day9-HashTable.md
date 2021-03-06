# Hashmap/ Hashset题目：
## Leetcode 1. Two Sum
## Leetcode 146. LRU Cache (Python中可以使用OrderedDict来代替)
```python
class LRUCache:

    def __init__(self, capacity: int):
        self.cap = capacity
        self.used = collections.deque()
        self.cache = {}

    def get(self, key: int) -> int:
        if key in self.cache.keys():
            self.used.remove(key)
            self.used.append(key)
            return self.cache[key]
        else:
            return -1
        

    def put(self, key: int, value: int) -> None:
        if key in self.cache.keys():
            self.cache[key] = value
            self.used.remove(key)
            self.used.append(key)
        elif len(self.cache) < self.cap:
            self.cache[key] = value
            self.used.append(key)
        else:
            del self.cache[self.used.popleft()]
            self.cache[key] = value
            self.used.append(key)
```

orderedDict
```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.dict = OrderedDict()

    def get(self, key: int) -> int:
        if key not in self.dict:
            return -1
        self.dict.move_to_end(key)
        return self.dict[key]

    def put(self, key: int, value: int) -> None:
        if key in self.dict:
            self.dict.pop(key)
            
        self.dict[key] = value
        if len(self.dict) > self.cap:
            self.dict.popitem(last=False) 
```
## Leetcode 128. Longest Consecutive Sequence
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums2 = sorted(nums)
        length = len(nums2)
        if (length ==0):
            return 0
        dict1 = set()
        max1 = 1
        i = 0
        while i < length - 1:
            if nums2[i+1] == nums2[i] + 1:
                max1 += 1
                i += 1
            elif nums2[i+1] == nums2[i]:
                i += 1
                continue
            else:
                dict1.add(max1)
                max1 = 1
                i += 1
        dict1.add(max1)
        return max(dict1)
```
## Leetcode 73. Set Matrix Zeroes
```python
class Solution(object):
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        R = len(matrix)
        C = len(matrix[0])
        rows, cols = set(), set()

        # Essentially, we mark the rows and columns that are to be made zero
        for i in range(R):
            for j in range(C):
                if matrix[i][j] == 0:
                    rows.add(i)
                    cols.add(j)

        # Iterate over the array once again and using the rows and cols sets, update the elements
        for i in range(R):
            for j in range(C):
                if i in rows or j in cols:
                    matrix[i][j] = 0
```

## Leetcode 380. Insert Delete GetRandom O(1)
## Leetcode 49. Group Anagrams
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dict1 = {}
        for s in strs:
            sortedword = "".join(sorted(s))
            if sortedword in dict1.keys():
                dict1[sortedword].append(s)
            else:
                dict1[sortedword]= [s]
        return list(dict1.values())
```
## Leetcode 350. Intersection of Two Arrays II
## Leetcode 299. Bulls and Cows
## Leetcode 348 Design Tic-Tac-Toe
