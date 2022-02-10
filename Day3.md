### Day 3
## Median of Two Sorted Arrays. 
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.  
The overall run time complexity should be O(log (m+n)).
1. using the method on CS61B, merge two sorted arrays. But here, we only merge half part of the array.
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int len1 = nums1.length;
        int len2 = nums2.length;
        int[] C = new int[(len1 + len2)/2 +1];
        int L1 = 0;
        int L2 = 0;
        while(L1+L2 < C.length) {
            if (L2 >= len2 || (L1 < len1 && nums1[L1] < nums2[L2]) ) {
                C[L1+L2] = nums1[L1];
                L1 += 1;
            } else {
                C[L1+L2] = nums2[L2];
                L2 += 1;
            }
        }
        if ((len1 + len2) % 2 == 0) {
            return (C[C.length - 1] + C[C.length - 2]) / 2.0;
        } else {
            return C[C.length - 1];
        }
    }
}
```
