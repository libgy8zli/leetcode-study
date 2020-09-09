Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

```
Example: 

Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

This is a typical sliding window question, with key word 'positive' (meaning same sign of all element)
and 'contiguous'

```python
class Solution:
    def minSubArrayLen(self, s, nums):
        # init start pointer, min_len, and subarray sum 
        start, min_len, sub_sum = 0, float("+inf"), 0
        for end in range(len(nums)):
            # increment subarray sum 
            sub_sum += nums[end]        
            while sub_sum >= s:
                # when sub_sum greater or equal to s
                # update the current min_len with current end and start pointers.
                min_len = min(min_len, end-start+1)
                # then remove the num from the very left from sub_sum
                sub_sum -= nums[start] 
                # and then move start to next level
                start += 1
        return min_len if min_len < float("+inf") else 0
```