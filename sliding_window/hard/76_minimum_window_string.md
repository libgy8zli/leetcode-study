Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

```
Example:

Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
Note:

If there is no such window in S that covers all characters in T, return the empty string "".
If there is such window, you are guaranteed that there will always be only one unique minimum window in S.
```


```python
class Solution:
    def minWindow(self, s, t):
        # early stop for empty s
        if not s:
            return ""
        # since we need to find a substring contain all the characters in t
        # we can init a freq count dictionary for t, whenever we 
        # find a match character in s, we will decrease the freq of this 
        # character by 1, when the frequency of this character become 0
        # that means we find all occurrences of current character.
        # then we can increase a variable called matched by 1
        # when matched equals to the len of frequency, means we find 
        # all the characters of t in current substring
        start, matched, output_str, freq_dict = 0, 0, "", {} 
        for c in t:
            freq_dict[c] = freq_dict.get(c,0) + 1
        # can replace above loop, with Counter in collections
        # freq_dict = collections.Counter(t)
        
        # iterate s
        for end in range(len(s)):
            # if we find a match, decrease freq by 1
            if s[end] in freq_dict:
                freq_dict[s[end]] -= 1
                # when freq == 0, increase matched by 1
                if freq_dict[s[end]] == 0:
                    matched += 1
            # once matched equals to len(freq_dict) 
            # means we find all characters, then start 
            # to shrink the window from left
            while matched == len(freq_dict):
                # update output_str first, if current substring 
                # is shorter 
                if not output_str:
                    output_str = s[start:end+1]
                else:
                    if len(output_str) > len(s[start:end+1]):
                        output_str = s[start:end+1]
                # shrink the window
                if s[start] in freq_dict:
                    # if s[start] freq is 0 
                    # decrease matched by 1 first
                    if freq_dict[s[start]] == 0:
                        matched -= 1
                    # increase the freq by 1
                    freq_dict[s[start]] += 1
                # move start to right 
                start += 1
        return output_str
                
            


```
