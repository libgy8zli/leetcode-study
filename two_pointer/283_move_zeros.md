Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

```
Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.
```

Since we need to maintain the order of the origin list, so we need to use two pointers 
which move to the same direction from beginning. very similar to question 26


```python
class Solution:
    def moveZeroes(self, nums):
        zero_idx = 0
        for idx in range(len(nums)):
            # whenever we find one idx with value not 0, swap with value at zero idx 
            # and increment zero_idx by 1
            if nums[idx] != 0:
                nums[idx], nums[zero_idx] = nums[zero_idx], nums[idx]
                zero_idx += 1
        return nums 
```

```
1. 
nums = [0, 1, 0, 3, 12]
zero_idx = 0 
idx = 0 
because nums[idx] = nums[0] = 0 
move to next idx 
2. 
nums = [0, 1, 0, 3, 12]
zero_idx = 0 
idx = 1
nums[idx] = nums[1] = 1
swap value at idx and zero_idx 
nums = [1, 0, 0, 3, 12]
increment zero_idx  by 1
zero_idx = 1
3.
nums = [1, 0, 0, 3, 12]
zero_idx = 1
idx = 2
nums[idx] = nums[2] = 0, skip 
4.
nums = [1, 0, 0, 3, 12]
zero_idx = 1
idx = 3  
nums[idx] = nums[3] = 3
sawp value at idx and zero_idx 
and increment zero_idx by 1
nums = [1, 3, 0, 0, 12] 
5.
nums = [1, 3, 0, 0, 12]
zero_idx = 2 
idx = 4  
nums[idx] = nums[4] = 0, skip
6.
nums = [1, 3, 0, 0, 12]
zero_idx = 2 
idx = 5  
nums[idx] = nums[5] = 12 
swap value at idx and zero_idx
nums = [1, 3, 12, 0, 0]
we reach the end of the list and done.
```
