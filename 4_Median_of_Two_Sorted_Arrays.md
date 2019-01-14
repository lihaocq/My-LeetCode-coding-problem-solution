# Problem 4 &nbsp; &nbsp; Median of Two Sorted Arrays

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

### 1. Brute force way: My 1st solution
1) Combine the two lists to a new list. 2) sorted the list with python list.sort(), which sorts the list without generating a new list. 3) get the median of the list.

The complexity is from **sorted()** function. 
Time complexity O(n*log(n)). 
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
### 2. Binary search way
From https://leetcode.com/articles/median-of-two-sorted-arrays/

The overall run time complexity should be O(log (m+n)) means that some thing like Binary Search are supposed to be applied to this problem. 

#### Basic idea for this way

The key for calculating the median is to divide the two lists into two parts, the left part and right part. So the key is to decide i and j, where the two lists should be split. Input lists are A and B, len(A) = m, len(B) = n.

```python 3
             Left   |  Right
A[0], A[1]...A[i-1] | A[i], A[i+1]...A[m]
B[0], B[1]...B[j-1] | B[j], B[j+1]...B[n]
```

**Basic equations** to calculate i and j is that: 

1. i + j = (m+n)//2           It applies for situations that m+n is odd and m+n is even.

2. If m+n is even,
$$
median=\frac{max(Left)+min(Right)}{2}
$$

  If m+n is odd,
$$
  median=min(Right)
$$

**Procedure:** 

```
Loop i from 0 - m
	Calculate j = (m+n)//2 - i      (**Note**: j should be bigger than 0 , so m < n)
	Decide if i is too small or too large by checking:				
		if  A[i-1] > B[j],   decrease i 
		elif B[j-1] > A[i],  increase i
		else: return i		
```
This is just the basic procedure, we could use binary search to make it faster

#### A very important thinking mode

Applying some algorithm is like solving partial differential equation. We should:

-  Find out and apply the control equation. In this case is: 

Calculate j = (m+n)//2 - i ;		if  A[i-1] > B[j],   decrease i ;	if B[j-1] > A[i],  increase i;

- Add some condition which make the control equations could be run smoothly. In this case is: 

j should be bigger than 0 , so m < n.

- Handle the addition conditions  and the boundary conditions (when i = 0, m, or j = 0, m). For this case:

To guarantee m < n, if not, switch A and B.      To handle [i = 0, m, or j = 0, m] cases separately with other cases.

  

#### My code:

Running time 160ms

``` python 3
class Solution:

    def findMedianSortedArrays(self, A, B):

        m = len(A)
        n = len(B)

        ### A should not be longer than B. If it is longer than B, j could be negtive, which is not good.
        if m > n:
            A, B, m, n = B, A, n, m

        imin=0
        imax=m  #because about list A which has m elements, there is m+1 situations in total, from 0 element to m element.

        ### solve the problem that one list is empty.
        if len(A)==0:
            if n%2==0:
                return (B[n//2-1]+B[n//2])/2.0
            elif n%2 ==1:
                return B[n//2]

        ### binary search to find the desired i
        while imin <= imax:
            i = (imax+imin)//2
            j = (m+n)//2-i

            if j>0 and  i < m and B[j-1] > A[i]: # j<0 and i<m is to make sure that B[j-1] and A[i] exist.
                imin = i+1

            elif i>0 and j <n and A[i-1] > B[j]: # i>0 and j<n is to make sure that A[i-1] and B[j] exist.
                imax = i-1

            else:
                
                # if i is perfect.
				
                # play with the edge situation.
                if i==0 : max_left = B[j-1]
                elif j==0: max_left = A[i-1]
                else: max_left = max(B[j-1],A[i-1])

                # play with the edge situation.
                if i==m: min_right = B[j]
                elif j==n: min_right = A[i]
                else: min_right = min(A[i],B[j])
				
                # play with general situation.
                if (m+n)%2 == 0:
                    return (max_left+min_right)/2.0

                if (m+n)%2 == 1:
                    return min_right
```



