Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

```
Example 1:

Input: [3,2,1,5,6,4] and k = 2
Output: 5
Example 2:

Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
```

#### Approach one using min_heap 

```python
from heapq import heappush, heappop
class Solution:
    def findKthLargest(self, nums, k):
        if not nums:
            return nums
        min_heap = []
        # we push each number into the min_heap 
        for num in nums:
            heappush(min_heap, num)
        # and min_heap always put the smallest in the current heap on top 
        # so whenever the length of min_heap greater than k we pop out the current smallest number
            if len(min_heap) > k:
                heappop(min_heap)
        # when every number iterate through, and the smallest number always pop out whenever length 
        # of min_heap bigger than k. 
        return min_heap[0]
```

```
nums = [3, 2, 1, 5, 6, 4]
k = 2
1. when first time reach length 2:
[2, 3]
2. next number is 1. 
[1, 2, 3], because length greater than 2, so pop out smallest one: 1, min_heap = [2, 3]
3. next number is 5.
[2, 3, 5],  because length greater than 2, so pop out smallest one 2, min_heap [3, 5] 
4. next number is 6
[3, 5, 6],  because length greater than 2, so pop out smallest one 3, min_heap [5, 6] 
4. next number is 4 
[4, 5, 6],  because length greater than 2, so pop out smallest one 4, min_heap [5, 6] 

and kth largest is min_heap[0] = 5
```

#### Approach two using quick_select 
```python
class Solution:
    def findKthLargest(self, nums, k):
        return self.quick_select(nums, 0, len(nums), k-1)
    def quick_select(self, nums, start, end, k):
        if start == end:
            return nums[start]
        left, right = start, end 
        pivot = nums[start+(end-start)//2]
        while left <= right:
            # because we find the kth largest, we will sort it in decending order
            while left <= right and nums[left] > pivot:
                left += 1
            while left <= right and nums[right] < pivot:
                right -= 1
            # if left is still less than or equal to right
            # swap left and right
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        # then we will recursive check
        # if k is smaller than right, we can just look the left side 
        if k <= right:
            self.quick_select(nums, start, right, k)
        if k >= left:
            self.quick_select(nums, left, end, k)
        return nums[k]
        
                

```