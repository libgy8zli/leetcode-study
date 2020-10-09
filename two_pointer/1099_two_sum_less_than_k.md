Given an array A of integers and integer K, return the maximum S such that there exists i < j with A[i] + A[j] = S and S < K. If no i, j exist satisfying this equation, return -1.


```
Example 1:

Input: A = [34,23,1,24,75,33,54,8], K = 60
Output: 58
Explanation: 
We can use 34 and 24 to sum 58 which is less than 60.
Example 2:

Input: A = [10,20,30], K = 15
Output: -1
Explanation: 
In this case it's not possible to get a pair sum less that 15.
 

Note:

1 <= A.length <= 100
1 <= A[i] <= 1000
1 <= K <= 2000
```


```python
class Solution:
    def twoSumLessThanK(self, nums, K):
        # similar to sorted array two sum
        nums.sort()
        left, right = 0, len(nums) - 1
        max_sum = float('-inf')
        while left < right: 
            curr_sum = nums[left] + nums[right]
            if curr_sum < K: 
                max_sum = max(max_sum, curr_sum)
                left += 1
            else:
                right -= 1
        return max(max_sum, -1)


```