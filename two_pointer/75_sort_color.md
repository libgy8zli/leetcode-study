Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

```
Example 1:

Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Example 2:

Input: nums = [2,0,1]
Output: [0,1,2]
Example 3:

Input: nums = [0]
Output: [0]
Example 4:

Input: nums = [1]
Output: [1]
```

##### Approach 1 one-pass 
since the list only contain 3 numbers(0, 1, 2), we can init 3 pointers, left=curr=0 and right=len(nums)-1,  
and use curr to compare the left and right, and move them accordingly, if values at curr and left 
are 0, we increment both pointers by 1, if curr 


```python
class Solution:
    def sortColor(self, nums):
        if not nums:
            return nums
        left, mid, right = 0, 0, len(nums) - 1
        while mid <= right:
            # when mid point to 0, we need to swap mid and left
            if nums[mid] == 0:
                nums[mid], nums[left] = nums[left], nums[mid]
            # when mid point to 1, no need to swap, but increment mid by 1
            elif nums[mid] == 1:
                mid += 1
            else:
            # when mid point to 2, swap mid and right, decrement right by 1 
                nums[right], nums[mid] = nums[mid], nums[right]
                right -= 1
        return nums 
```
```
nums = [0, 1, 0, 2, 0, 1, 2]
step 1:
init left = mid = 0 , right = len(nums) - 1 = 6 

1. when nums[mid] = 0 
nums = [0, 1, 0, 2, 0, 1, 2]
we swap left and mid, and increment left and mid by 1
left = mid = 1 
2. nums[mid] = nums[1] = 1
nums = [0, 1, 0, 2, 0, 1, 2]
we increment mid by 1 
left = 1
mid = 2
right = 6
3. nums[mid] = nums[2]  =  0 
nums[left] = nums[1] = 1 
need to swap left and mid 
nums = [0, 0, 1, 2, 0, 1, 2]
left = 2 
mid = 3
right = 6
4. nums[mid] = nums[3] = 2 
need to swap mid with right 
nums = [0, 0, 1, 2, 0, 1, 2]
left = 2
mid = 3 
right = 5
5. nums[mid] = nums[3] = 2
need to wap mid with right 
nums = [0, 0, 1, 1, 0, 2, 2]
left = 2
mid = 3 
right = 4
6. nums[mid] = nums[3] = 1 
no swap, but increment mid by 1
left = 2
mid = 4
right = 4
7. nums[mid] = nums[4] = 0
need to swap left and mid
nums = [0, 0, 0, 1, 1, 2, 2]
left = 3 
mid = 5 
right = 4
8, mid > right, so stop while loop 
and nums is sorted correctly.
```


#### quicksort approach 

```python
class Solution:
    def sortColor(self, nums):
        if not nums:
            return nums 
                
        self.quick_sort(nums, 0, len(nums)-1)
        return nums

    def quick_sort(self, nums, start, end):
        if start >= end:
            return None 
        left, right = start, end 
        pivot = nums[start+(end-start)//2]
        while left <= right:
            while left <= right and nums[right] > pivot:
                right -= 1
            while left <= right and nums[left] < pivot:
                left += 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        self.quick_sort(nums, start, right)
        self.quick_sort(nums, left, end)

```


