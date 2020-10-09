Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

```
Example 1:

Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Example 2:

Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
 

Note:

1 <= A.length <= 10000
-10000 <= A[i] <= 10000
A is sorted in non-decreasing order.
```
since this array is already sorted, and we have negative value on the
left side, so the left side square may be greater than the right side one 
we will start 3 pointers, left, right and one to track which index should 
hold the current highest number


```python
class Solution:
    def sortedSquares(self, A):
        if not A:
            return A
        output = [0 for _ in range(len(A))]
        left, right, max_num_idx = 0, len(A) - 1, len(A) - 1
        while left <= right:
            left_square = A[left] * A[left]
            right_square = A[right] * A[right]
            # if left is bigger, assign left_square to 
            # current max num index, meanwhile increment 
            # left by 1
            if left_square > right_square:
                output[max_num_idx] = left_square
                left += 1 
            else:
                output[max_num_idx] = right_square
                right -= 1
            max_num_idx -= 1
        return output


```

