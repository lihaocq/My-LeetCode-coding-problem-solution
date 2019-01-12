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
loop through the input list. And for each element, it loops all the rest elements after this element. 
Time complexity O(n^2). Space complexity O(1).

The run time of the following code is -- 3872 ms.
``` python 3
#python3

import copy


class Solution:
    def twoSum(self, nums, target):

        length_nums = len(nums)
        for i in range(length_nums):  # loop one
            counterpart = target - nums[i]
            for j in range(i+1,length_nums):  # loop two
                if  nums[j] == counterpart:
                    return [i, j]
```
##### 2. Sorted List ()
**It is easier to solve this problem after sorting the input list. Use two pointers (head pointer and end pointer to narrow down the possible range of target elements**. Moving the head pointer forward and the end pointer backward, finally the target elements would be found if they exist.
Time complexity O(n)
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
##### 3. Hash Table -- Two Pass
Looking up time for Hash Table is O(1), if the hash function was chosen carefully. For python, the dictionary is a hash table. Checking if an element is at the list cost time O(n). It should be noted that Dictionary does not allow two keys with the same name.
Time complexity O(n)
The run time of the following code is -- 40 ms.
``` python 3
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hash_table ={}   # generate the hash table
        
        for item_index, item in enumerate(nums):
            hash_table[item]=item_index
        
        for i in range(len(nums)):
            temp = target - nums[i]
            if (temp in hash_table) and hash_table[temp]!=i:
                return [i,hash_table[temp]]
```
##### 4. Hash Table -- one pass
Only one iteration is used in this method. When a new key and its value are put in the hash table, the counterpart of this key is calculated and is checked if it is in the hash table. 
Time complexity O(n)
The run time of the following code is -- 60 ms.
``` Python 3
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hash_table ={}   # generate the hash table
        
        for i in range(len(nums)):
            if (nums[i] not in hash_table):
                hash_table[nums[i]]=i
                
            temp = target - nums[i]
            if (temp in hash_table) and (hash_table[temp] != i):
                return [hash_table[temp],i]
```

