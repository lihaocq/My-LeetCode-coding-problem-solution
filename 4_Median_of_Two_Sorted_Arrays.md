
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
