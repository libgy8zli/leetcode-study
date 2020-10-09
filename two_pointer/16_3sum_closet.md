Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

 
```
Example 1:

Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
 

Constraints:

3 <= nums.length <= 10^3
-10^3 <= nums[i] <= 10^3
-10^4 <= target <= 10^4
```

we can take a similar approach to 3SUM, sort the array first, and start from beginning idx
and  create left and right pointer as idx + 1 and len(nums) - 1 , then compare these 
3 numbers sum with target, and create a variable to track the absolute smallest difference. 
if target - 3sum > 0, which means 3sum is smaller , then move left pointer to right, 
otherwise meaning 3sum is bigger , then move right to left to get closer

```python
class Solution:
    def threeSumClosest(self, nums, target):
        if not nums:
            return nums
        # start with first element til third to last
        nums.sort()
        min_diff = float('inf')
        for idx in range(len(nums)-2):
            left, right = idx + 1, len(nums) - 1
            while left < right:
                curr_sum = nums[idx] + nums[left] + nums[right]
                curr_diff = target - curr_sum
                if curr_diff == 0:
                    return target 
                if abs(curr_diff) < abs(min_diff):
                    min_diff = curr_diff
                # if curr_diff greater than 0, which means curr_sum is smaller, move left 
                # to right to bring them closer 
                if curr_diff > 0:
                    left += 1
                else:
                    right -= 1
        return target - min_diff
```
