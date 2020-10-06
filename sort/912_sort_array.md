Given an array of integers nums, sort the array in ascending order.

```
Example 1:

Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Example 2:

Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
 

Constraints:

1 <= nums.length <= 50000
-50000 <= nums[i] <= 50000
```


##### Merge sort

1. Divide by finding the mid point m between start and end of an array.
2. Conquer by recursively sorting the subarrays created by the divide step 
3. Combine by merging two sorted subarrays back into single sorted one. 

for merge sort the time complexity is O(NlogN),  the worst and average complexity is O(NlogN)
and the space complexity is O(n), need a temp array to hold sorted value

```python
class Solution:
    def sortArray(self, nums):
        # base case if nums 
        if len(nums) <= 1:
            return nums
        # get the middle point
        pivot = len(nums) // 2
        # divide list into two
        left_list = self.sortArray(nums[:pivot])
        right_list = self.sortArray(nums[pivot:])
        return self.merge_sort(left_list, right_list)

    def merge_sort(self, left_list, right_list):
        # init pointers for both left and right lists
        left_idx, right_idx = 0, 0 
        # init empty list to hold sorted values
        sorted_list = []
        # iterate through both list and compare the value
        # if value of current left pointer at left list is less, then 
        # append this value to the sorted list, and increment 
        # left pointer by 1, otherwise do the same thing for 
        # right list
        while left_idx < len(left_list) and right_idx < len(right_list):
            if left_list[left_idx] < right_list[right_idx]:
                sorted_list.append(left_list[left_idx])
                left_idx += 1
            else:
                sorted_list.append(right_list[right_idx])
                right_idx += 1
        # there could be left-over if one list reach end first, so 
        # we will append the left-over to sorted_list 
        # when slice in python list out of range, it will return empty list 
        sorted_list += left_list[left_idx:]
        sorted_list += right_list[right_idx:]
        return sorted_list
```


#### Quick sort 

Like merge sort, quick sort is also a divde and conquer algorithm,  but unlike merge sort,  quick sort will do 
the sort in divide step, and in the opposite, merge sort hardly does anything in divide step.  

1. Divide by choosing a pivot number (normally start with middle), and then put all the numbers less  than or equal 
pivot to the left, and all the numbers greater than pivot to the right 
2. Conquer by recursively sorting the subarrays on the left side and right side.
3. Combine by doing nothing, once every subarray is recursively sorted,  we get the sorted list 


```python

class Solution 
    def sortArray(self, nums):
        if not nums:
            return nums
        self.quick_sort(nums, 0, len(nums)-1)
        return nums

    def quick_sort(self, nums, start, end):
        # check if start is less than end  
        if start >= end:
            return None
        
        # init left and right pointers 
        left, right = start, end
        # get pivot point 
        pivot_idx = start + (end-start) // 2
        pivot = nums[pivot_idx]
        while left <= right:
            # compare right side numbers to pivot if already 
            # greater than the pivot, move right pointer to right 
            while left <= right and nums[right] > pivot:
                right -= 1
            # compare left side numbers to pivot if already 
            # less than  the pivot, move left pointer to left
            while left <= right and nums[right] < pivot:
                left += 1
            # then we swap left and right
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        # once the while stop, left will be greater than right, so 
        # we will sort from the start to right, and left to end
        self.quick_sort(nums, start, right)
        self.quick_sort(nums, left, end)


```


