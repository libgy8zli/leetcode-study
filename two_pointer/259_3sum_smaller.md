Given an array of n integers nums and an integer target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.

Follow up: Could you solve it in O(n2) runtime?

```
Example 1:

Input: nums = [-2,0,1,3], target = 2
Output: 2
Explanation: Because there are two triplets which sums are less than 2:
[-2,0,1]
[-2,0,3]
Example 2:

Input: nums = [], target = 0
Output: 0
Example 3:

Input: nums = [0], target = 0
Output: 0
 

Constraints:

n == nums.length
0 <= n <= 300
-100 <= nums[i] <= 100
-100 <= target <= 100
```

```python
class Solution:
     def threeSumSmaller(self, nums, target):
        nums.sort()
        triple_count = 0
        for idx in range(len(nums)-2):
            left, right = idx + 1, len(nums) - 1
            while left < right:
                curr_sum = nums[idx] + nums[left] + nums[right]
                if curr_sum < target:
                    #if curr_sum is smaller than target, that means all the two number between 
                    # right and left , plus nums[idx] is less than target
                    triple_count += right - left 
                    left += 1
                else:
                    right -= 1
        return triple_count


```
