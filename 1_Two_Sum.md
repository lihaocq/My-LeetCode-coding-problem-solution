# Problem 1 &nbsp; &nbsp; Two Sum
### Problem Statement:
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target. You may assume that each input would have exactly **one** solution, and you may not use the same element twice.
##### Example
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
### Notes:
There are three ways to solve this problem:
###### 1. Brute Force: 
loop through the input list. And for each element, it loops all the rest elements after this element. So the time complexity is O(n^2).
space complexity is O(1)

The run time of the following code is -- 3872 ms.
``` python 3
#python3

import copy


class Solution:
    def twoSum(self, nums, target):

        length_nums = len(nums)
        for i in range(length_nums):
            counterpart = target - nums[i]
            for j in range(i+1,length_nums):
                if  nums[j] == counterpart:
                    return [i, j]
```
##### 2. sorted list ()
It is easier to solve this problem after sorting the input list. Use two pointers (head pointer and end pointer to narrow down the possible range of target elements. Moving the head pointer forward and the end pointer backward, finally the target elements would be found if they exist.

The run time of the following code is -- 68 ms.
``` python 3
#python3
import copy

class Solution:
    
    def twoSum(self, nums, target):

        length_nums = len(nums)
        # generate a list which has sorted list and the index of orignial list
        sorted_list = sorted(enumerate(nums),key=lambda x:x[1])
        
        pointer_head = 0
        pointer_end = length_nums-1
        
        while pointer_end > pointer_head: 

            temp = sorted_list[pointer_head][1]+sorted_list[pointer_end][1]
            if temp ==target:
                return [sorted_list[pointer_head][0],sorted_list[pointer_end][0]]
            elif temp > target:
                pointer_end -= 1
            elif temp< target:
                pointer_head += 1
```
