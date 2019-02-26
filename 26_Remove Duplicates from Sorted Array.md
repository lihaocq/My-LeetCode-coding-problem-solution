## Key points

1. use **two pointers method**, this problem is not important as long as you understand Problem 15: 3 Sum.

## Code:

```python 3
class Solution:
    def removeDuplicates(self, nums):
        len_nums = len(nums)
        if len_nums<=1:
            return len_nums
        i = 0
        j = 0

        while j < len_nums-1:

            while (nums[j] == nums[i] and j < (len(nums)-1)):
                j += 1
                
            if nums[j] != nums[i]:
                nums[i+1] = nums[j]
                i += 1

        return i+1

```