Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

```
Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

```python
class Solution:
    def removeDuplicates(self, nums):
        # init a pointer and set to 1 as non duplication idx
        non_dup_idx = 0 
        # iterate through the list and compare value current idx with non_dup_idx
        # if they are not equal then swap, and increment non_dup_idx by 1 
        for idx in range(len(nums)):
            if nums[idx] != nums[non_dup_idx]:
                non_dup_idx += 1
                nums[non_dup_idx] = nums[idx]
        return non_dup_idx + 1
```


```
1.
nums =  [0, 0, 1, 1, 2, 2]
non_dup_idx = 0 
idx = 0
nums[idx] = nums[0] = 0
nums[non_dup_idx] = nums[0] = 0 
they are equal, move idx to next
2.
nums =  [0, 0, 1, 1, 2, 2]
non_dup_idx = 0 
idx = 1 
nums[idx] = nums[0] = 0
nums[non_dup_idx] = nums[1] = 0 
they are equal, move idx to next
3. 
nums =  [0, 0, 1, 1, 2, 2]
non_dup_idx = 0 
idx = 2 
nums[idx] = nums[2] = 1
nums[non_dup_idx] = nums[0] = 0 
increment non_dup_idx to point to next non_dup_idx
they are not equal, assign nums[2] to non_dup_idx
4.
nums =  [0, 1, 0, 1, 2, 2]
non_dup_idx = 1 
idx = 3 
nums[idx] = nums[3] = 1 
nums[non_dup_idx] = nums[1] = 1
they are  equal, move to next idx
5. 
nums =  [0, 1, 0, 1, 2, 2]
non_dup_idx = 1 
idx = 4 
nums[idx] = nums[4] = 2
nums[non_dup_idx] = nums[1] = 1
they are not equal, then move idx right next to current non_dup_idx 
non_dup_idx += 1
nums[non_dup_idx] = nums[2] = nums[4]
6.
nums =  [0, 1, 2, 1, 0, 2]
non_dup_idx = 2 
idx = 5 
nums[idx] = nums[5] = 2
nums[non_dup_idx] = nums[2] = 2
they are equal, skip and reach the end.
```