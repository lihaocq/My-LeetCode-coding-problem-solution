## Key points

Readme: This problem is not very different with Problem 15 : 3 Sum. Problem 15 is more important. If you understand Problem 15, then just ignore this problem.

1. Use the method: **Two Pointer**

   First, sort the list and put one pointer at head and another one at the tail.

   Second, if sum is smaller than reference, increase head pointer. If sum is larger than reference, decrease tail pointer.

   

## Code:

```python 3
class Solution:
    def threeSumClosest(self, nums, target):
        len_nums = len(nums)
        best_value_abs = 10000000
        result = 0

        nums.sort()

        p1 = 0
        for p1 in range(0, len_nums-2):
            p2 = p1+1
            p3 = len_nums-1

            while p2 < p3:

                value = nums[p1]+nums[p2]+nums[p3]
                value_abs = abs(target-value)

                if value_abs < best_value_abs:

                    result = value
                    best_value_abs = value_abs

                if value > target:
                    p3 -= 1
                elif value < target:
                    p2 += 1
                else:
                    return value

        return result


```