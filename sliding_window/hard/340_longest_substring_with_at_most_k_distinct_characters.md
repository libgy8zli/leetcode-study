Given a string, find the length of the longest substring T that contains at most k distinct characters.
```
Example 1:

Input: s = "eceba", k = 2
Output: 3
Explanation: T is "ece" which its length is 3.
Example 2:

Input: s = "aa", k = 1
Output: 2
Explanation: T is "aa" which its length is 2.
```
This question is almost identical with question 904, instead of 
keep two distinct letters, this one is to check k distinct 


```python
class Solution:
    def lengthOfLongestSubstringKDistinct(self, s, k):
        if not s:
            return 0 
        # init empty dictionary to keep tracking substring length
        start, max_len, freq_dict = 0, float("-inf"), {}
        for end in range(len(s)):
            # update freq_dict for all the characters have been seen
            freq_dict[s[end]] = freq_dict.get(s[end], 0) + 1
            # when the length of dict is greater than k, shrink the window
            while len(freq_dict) > k: # this is the only difference with question 904
                if s[start] in freq_dict:
                    freq_dict[s[start]] -= 1
                    if freq_dict[s[start]] == 0:
                        freq_dict.pop(s[start])
                # shrink window 
                start += 1
            max_len = max(max_len, end-start+1)
        return max_len
```