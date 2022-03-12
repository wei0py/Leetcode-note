## 二分法（Binary Search）：
基础知识：二分法是用来解法基本模板，时间复杂度logN；常见的二分法题目可以分为两大类，显式与隐式，即是否能从字面上一眼看出二分法的特点：要查找的数据是否可以分为两部分，前半部分为X，后半部分为O.  
显式二分法：  
### Leetcode 34. Find First and Last Position of Element in Sorted Array
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        if len(nums)==0:
            return [-1,-1]
        i = 0
        j = len(nums)-1
        k=len(nums)-1
        while i<j:
            m=int((i+j)/2)
            if nums[m]<target:
                i=m+1
            elif nums[m]> target:
                
                j=m-1
                k=m-1
            else:
                j=m
            #     i=int((i+m)/2)
            #     j=int((j+m)/2)
        
        if nums[j]==target:
            l1=j
            l2=k
        
            while l1<=l2:
                m=int((l1+l2)/2)
                if nums[m]>target:
                    l2=m-1
                else:
                    l1=m+1
            return [j,l2]
                    
        else:
            return [-1,-1]
```
### Leetcode 33. Search in Rotated Sorted Array
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        length = len(nums)
        if length == 0:
            return -1
        if length == 1:
            if nums[0] != target:
                return -1
            else:
                return 0
    
        if nums[0] > nums[length - 1]:
            i, j = 0, length - 1
            while (i < j):
                inter = int((i + j)/2)
                if (nums[inter] > nums[i]):
                    i = inter
                else:
                    j = inter
            if target > nums[length - 1]:
                i1 = 0
                j1 = i + 1
            else: 
                i1 = i + 1
                j1 = length - 1
        else:
            i1 = 0
            j1 = length - 1
        while ( i1 <= j1 ):
            inter1 = int((i1 + j1)/2)
            if (nums[inter1] < target):
                i1 = inter1 + 1
            elif nums[inter1] > target:
                j1 = inter1 - 1
            else:
                return inter1
        return -1


```
### Leetcode 1095. Find in Mountain Array
### Leetcode 162. Find Peak Element
### Leetcode 278. First Bad Version
### Leetcode 74. Search a 2D Matrix
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        len1 = len(matrix)
        if len1 ==0:
            return False
        i, j = 0, len1-1
        
        while(i < j):
            inter = int((i+j)/2) 
            if (target < matrix[inter][0]):
                j = inter
            elif (target > matrix[inter][0] and target < matrix[inter + 1][0]):
                i = inter
                break
            elif target > matrix[inter + 1][0]:
                i = inter + 1
            else:
                return True
        # print(i,j,inter)
        k = i
        i1, j1 = 0, len(matrix[k]) -1 
        while (i1 <= j1):
            inter1 = int((i1+j1)/2)
            if (matrix[k][inter1] < target):
                i1 = inter1 +1
            elif (matrix[k][inter1] > target):
                j1 = inter1 -1
            else:
                return True
        return False
```
### Leetcode 240. Search a 2D Matrix II. 
隐式二分法：  
### Leetcode 69. Sqrt(x)
### Leetcode 540. Single Element in a Sorted Array
### Leetcode 644. Maximum Average Subarray II
### Leetcode 528. Random Pick with Weight
### Leetcode 1300. Sum of Mutated Array Closest to Target
### Leetcode 1060. Missing Element in Sorted Array
### Leetcode 1062. Longest Repeating Substring
### Leetcode 1891. Cutting Ribbons
