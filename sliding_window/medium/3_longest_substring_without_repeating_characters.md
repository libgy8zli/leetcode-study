Given a string s, find the length of the longest substring without repeating characters.

```
Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
Example 4:

Input: s = ""
Output: 0
 

Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.

``` 
The basic idea here is to have a hashmap (python dictionary) to store the index of 
every element in the string, whenever we see a repeating character, we shrink the window 
and move start pointer to the right next element of the repeating character

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        # if string is empty, return 0
        if not s:
            return 0
        # init an empty dictionary 
        start, max_len, index_map = 0, 0, {}
        for end in range(len(s)):
            if s[end] in index_map:
                # if we encounter one repeating character, we move 
                # start pointer to the one right next to repeating character
                # if the start is already ahead of current repeating character
                # we will keep it
                start = max(start, s[end]+1)
            # update max_len 
            max_len = max(max_len, end-start+1)
            # update the character index
            index_map[s[end]] = end
        return max_len
        




```
