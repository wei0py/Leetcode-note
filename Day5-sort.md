### Day5
## Quick sort and merge sort
## 148. Sort List
1. Using merge sort, first separate the list into 2 from medium (this can be done using slow = slow.next and fast = fast.next.next). Then sort the two list using recursive and then using merge to merge this two list.
2. Using quick sort.

## 56. Merge Intervals



## 27. Remove elements
1. python 
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
