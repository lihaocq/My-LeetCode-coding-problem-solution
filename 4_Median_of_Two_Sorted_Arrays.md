# Problem 1 &nbsp; &nbsp; Median of Two Sorted Arrays
### Problem Statement:
There are two sorted arrays **nums1** and **nums2** of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
You may assume **nums1** and **nums2** cannot be both empty.
##### Example 1
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```
##### Example 2
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

### Notes:
Two methods are provided for this problem. The second problem provides one way to apply **binary search**. Also it provides **a very important thinking mode** to apply algorithm. 

##### 1. Brute Force: My 1st solution
1) Combine the two lists to a new list. 2) sorted the list with python list.sort(), which sorts the list without generating a new list. 3) get the median of the list.
The complexity is from **sorted()** function. 
Time complexity O(n^2). 
Space complexity O(n).
The run time of the following code is -- 36 ms.
``` python 3
class Solution:
    
    def findMedianSortedArrays(self, nums1, nums2):
        nums = nums1 + nums2
        nums.sort()
        length_total = len(nums)
        
        if length_total%2 == 1:
            return nums[length_total//2]
        if length_total%2 == 0:
             return (nums[length_total//2]+nums[length_total//2-1])/2.0
```
##### 2. Binary Search
https://leetcode.com/articles/median-of-two-sorted-arrays/

The overall run time complexity should be O(log (m+n)) means that some thing like Binary Search are supposed to be applied to this problem.
The overall run time complexity should be O(log (m+n)) means that some thing like Binary Search are supposed to be applied to this problem.

fdafds
fdsafda
fdafda
fdaf
