Given an array A of 0s and 1s, we may change up to K values from 0 to 1.

Return the length of the longest (contiguous) subarray that contains only 1s. 

```
Example 1:

Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation: 
[1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
Example 2:

Input: A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
Output: 10
Explanation: 
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
 

Note:

1 <= A.length <= 20000
0 <= K <= A.length
A[i] is 0 or 1 
```

This is almost identical question with question 404. instead of letters, 
we only have 1 or 0 

```python 
class Solution:
    def longestOnes(self, A, K):
        if not A:
            return 0
        start, max_len, max_repeat = 0, 0, 0
        freq_dict = {1:0, 0:0}
        for end in range(len(A)):
            freq_dict[A[end]] += 1
            max_repeat = max(max_repeat, freq_dict[1])
            if end-start+1 > max_repeat + k:
                freq_dict[A[start]] -= 1
                start += 1
            max_len = max(max_len, end-start+1)
        return max_len
```

We can simplify the appove approach,  since there are only 1 and 0
in the dictionary,  which means any time the count of 0 is greater
than k, that means the current window is bigger than max_repeat + k
max_repeat in this case, will be the count of 1 in current window 

```python 
class Solution:
    def longestOnes(self, A, K):
        if not A:
            return 0
        start, max_len= 0, 0
        freq_dict = {1:0, 0:0}
        for end in range(len(A)):
            freq_dict[A[end]] += 1
            if freq_dict[0] > K:
                freq_dict[A[start]] -= 1
                start += 1
            max_len = max(max_len, end-start+1)
        return max_len
```