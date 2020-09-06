Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.
```
Example 1:
Input:nums = [1,1,1], k = 2
Output: 2
```

Constraints:

- The length of the array is in range [1, 20,000].
- The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

Note: sliding window technique is not good here, because the array contains both positive and negative numbers.

if all positive numbers:
````python
class Solution:
    def subarray_sum(self, nums, k):
        if not nums:
            return 0
        start, sum_count, curr_sum = 0, 0, 0
        for end in range(len(nums)):
            curr_sum += nums[end]
            while curr_sum >= k: 
                if curr_sum == k:
                    sum_count += 1
                curr_sum -= nums[start]
                start += 1
        return sum_count
````

Prefix sum is a sum of the curent value with all previous elements starting from the begining of the structure

It could be defined for 1D arrays (sum the current value with all the previous integers)

| input array | x0 | x1    | x2       | x3          | x4             |
|-------------|----|-------|----------|-------------|----------------|
| prefix sum  | x0 | x0+x1 | x0+x1+x2 | x0+x1+x2+x3 | x0+x1+x2+x3+x4 |


If the cumulative sum (represented by sum[i] for sum up to i<sup>th</sup> index) between two indices, say i 
and j is at a difference of k,  sum[j] - sum[i] = k, then the sum of elements lying between indices i
and j is k. 

Based on this idea, we use a hashmap which is used to store the cumulative sum was seen so far
the intuition  is we're recording earlier cumulative sums  so that when we encounter the latest cum_sum 
that is k away from an earlier cum_sum, we know to increment count.We record a "number of times" for earlier values,
ensuring we capture all extended up-and-down sequences where elements cancel.
```
for example
array = [0, 0, 0] 
target = 0

at index 0 
count = 1  
prefix_sum = {0:1}
subarray equals to target:
[0]


at index 1 
cum_sum = 0 
count = count + 1 = 1 + 1 = 2
and 
count = count + prefix_sum[0] = 2 + 1 = 3
subarries equals to target:
[0] # 0 at index 0
[0] # 0 at index 1
[0, 0] # both 0 at index 0 and 1

prefix_sum = {0:2}

at index 2 
cum_sum = 0 
count = count + 1 = 3 + 1 = 4
and 
count = count + rpefix_sun[0] = 4 + 2 = 6
subarries equal to target:
[0]  # index at 0
[0]  # index at 1 
[0] # index at 2 
[0, 0] # index at 0 and 1 
[0, 0] # index at 1 and 2  
[0, 0, 0] # index at 0, 1, 2 


```

```
array = [3, 4, 7, 2, -3, 1, 4, 2]
target_sum = 7

prefix_sum_count = {} 

at index 0:
ele_list = [3]
prefix_sum_count = {3:1}
current_prefix_sum - target_sum = 3 - 7 = -4 
-4 is not in current hash_map:
count = 0 

at index 1:
ele_list = [3, 4]
prefix_sum_count = {3:1, 7:1}
current_prefix_sum - target_sum = 7 - 7 = 0 
count = 1

at index 2:
ele_list = [3, 4, 7]
prefix_sum_count = {3:1, 7:1, 14:1}
current_prefix_sum - targe_sum = 14 - 7 = 7
and 7 is in the current hash_map
count = count + prefix_sum_count[7] = 1 + 1 = 2

at index 3:
ele_list = [3, 4, 7, 2]
prefix_sum_count = {3:1, 7:1, 14:1, 16:1}
current_prefix_sum - target_sum = 16 - 7 = 9
and 9 is not in the current hash_map
count = 2

at index 4:
ele_list = [3, 4, 7, 2, -3]
prefix_sum_count = {3:1, 7:1, 14:1, 16:1, 13:1}
current_prefix_sum - target_sum = 13 - 7 = 6
6 is not in the current hash_map
count = 2

at index 5:
ele_list = [3, 4, 7, 2, -3, 1]
prefix_sum_count = {3:1, 7:1, 14:2, 16:1, 13:1}
current_prefix_sum - target_sum = 14 - 7 = 7
7 is in the current hash_map, so sum of elements between index 2 and current index [7, 2, -3, 1]
also equal to target sum
count = count + prefix_sum_count[7] = 2 + 1 = 3

at index 6:
ele_list = [3, 4, 7, 2, -3, 1, 4]
prefix_sum_count = {3:1, 7:1, 14:2, 16:1, 13:1, 18:1}
current_prefix_sum - target_sum = 18 - 7 = 11
11 is not in current hash_map
count = 3

at index 7 
ele_list = [3, 4, 7, 2, -3, 1, 4, 2]
prefix_sum_count = {3:1, 7:1, 14:2, 16:1, 13:1, 18:1, 20:1}
current_prefix_sum - target_sum = 20 - 7 = 13
13 is in the current hash map , so sum of elements between index 5 and current_index [1, 4, 2]
also equal to 7
count = count + prefix_sum[13] = 3 + 1 = 4
```

````python
class Solution:
    def subarraySum(self, nums, k):
        if not nums:
            return 0 
        # init a hash map 
        prefix_sum = {}
        cum_sum , total_count = 0, 0
        for num in nums:
            cum_sum += num
            # inrement total count if cum_sum equals target
            if cum_sum == k:
                total_count += 1
            # we record the number of one earlier cum_sum that is k away from the current one 
            # so we can capture all the up and down extended 
            total_count += prefix_sum.get(cum_sum-k, 0)
            # then put current cum_sum in the map, if it is not already in
            prefix_sum[cum_sum] = prefix_sum.get(cum_sum, 0) + 1
        return total_count    
````
