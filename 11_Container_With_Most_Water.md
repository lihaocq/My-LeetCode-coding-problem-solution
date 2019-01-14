# Problem 11 &nbsp; &nbsp; Container With Most Water
### Problem Statement:
Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

##### Example 1
```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```
##### 1. Brute Force: 
Brute force method can not pass the time limit for this problem.
Time complexity O(n^2).
Space complexity O(1).

``` python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        max_area = 0
        nums= len(height)
        
        for i in range(nums):
            for j in range(i,nums):
                area = (j-i)*min(height[i],height[j])
                if area > max_area:
                    max_area = area
        return max_area
```
##### 2. Two Pointer Approach
This method is from https://leetcode.com/articles/container-with-most-water/

This method is special. However, the key idea is that try to make the time complexity O(n).

space complexity is O(1)

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        max_area = 0
        nums= len(height)
        imin = 0
        imax = nums - 1
        
        while imin < imax:
            area = (imax- imin)*min(height[imin],height[imax])
            if max_area < area :
                max_area = area
            if height[imin] > height[imax]:
                imax -= 1
            else:
                imin += 1
            
        return max_area
```

