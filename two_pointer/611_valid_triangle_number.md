Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.
```
Example 1:
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```
Note:

The length of the given array won't exceed 1000.

The integers in the given array are in the range of [0, 1000].

```python

class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        triangle_count = 0
        for first in range(len(nums)-2):
            third = first + 2
            for second in range(first+1, len(nums)-1):
                if nums[first] == 0:
                    continue
                while third < len(nums) and nums[first] + nums[second] > nums[third]:
                    third += 1
                triangle_count += third - second - 1 
        return triangle_count



```
