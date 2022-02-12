### Day5
## Quick sort and merge sort
## 148. Sort List
1. Using merge sort, first separate the list into 2 from medium (this can be done using slow = slow.next and fast = fast.next.next). Then sort the two list using recursive and then using merge to merge this two list.
2. Using quick sort.

## 56. Merge Intervals

1. python slow
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        interval2 = sorted(intervals);
        lenI = len(interval2);
        len2 = lenI;
        i = 0
        while(i < len2-1 ):
            if interval2[i][1] >= interval2[i+1][0]:
                interval2[i][1] = max(interval2[i+1][1], interval2[i][1]);
                interval2.pop(i+1);
                len2 -=1
            else:
                i += 1;
        return interval2
```        
2.
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        interval2 = sorted(intervals);
        lenI = len(interval2);
        out=[interval2[0]]
        
        for k in interval2[1:]:
            if k[0] <= out[-1][1]:
                out[-1][1] = max(k[1],out[-1][1])
            else:
                out.append(k)

        return out
```

## 75. Sort Colors
1. slow
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        in1 = nums.count(0)
        in2 = nums.count(1)
        in3 = nums.count(2)
    
        nums[0:in1] =[0 for i in range(in1)]
        nums[in1:(in1+in2)] = [1 for i in range(in2)]
        nums[(in1+in2):] =[2 for i in range(in3)] 


```








## 27. Remove elements
