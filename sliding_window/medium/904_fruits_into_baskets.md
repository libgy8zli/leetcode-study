In a row of trees, the i-th tree produces fruit with type tree[i].

You start at any tree of your choice, then repeatedly perform the following steps:

Add one piece of fruit from this tree to your baskets.  If you cannot, stop.
Move to the next tree to the right of the current tree.  If there is no tree to the right, stop.
Note that you do not have any choice after the initial choice of starting tree: you must perform step 1, then step 2, then back to step 1, then step 2, and so on until you stop.

You have two baskets, and each basket can carry any quantity of fruit, but you want each basket to only carry one type of fruit each.

What is the total amount of fruit you can collect with this procedure?

Identical question: 159

```
Example 1:

Input: [1,2,1]
Output: 3
Explanation: We can collect [1,2,1].
Example 2:

Input: [0,1,2,2]
Output: 3
Explanation: We can collect [1,2,2].
If we started at the first tree, we would only collect [0, 1].
Example 3:

Input: [1,2,3,2,2]
Output: 4
Explanation: We can collect [2,3,2,2].
If we started at the first tree, we would only collect [1, 2].
Example 4:

Input: [3,3,3,1,2,1,1,2,3,3,4]
Output: 5
Explanation: We can collect [1,2,1,1,2].
If we started at the first tree or the eighth tree, we would only collect 4 fruits.

```

Use a python dictionary to track the tree have been seen, and increment the count whenevery 
we see the tree, if the length of the dictionary is greater than 2, which means we see a new 
tree, shrink from beginning until the length of dict equal = 2. then compare with number of 
trees we see previously.  

```python
class Solution:
    def totalFruit(self, tree):
        if not tree:
            return 0 
        start, max_tree, tree_count_dict = 0, 0, {}
        for end in range(len(tree)):
            # increment the tree count in the dictionary if seen
            tree_count_dict[tree[end]] = tree_count_dict.get(tree[end],0) + 1
            # if the number of tree  in dictionary is greater than 2
            # we need to shrink the window by moving start to the right
            # until tree count in map equal to 2
            while len(tree_count_dict) > 2:
                if tree[start] in tree_count_dict:
                    tree_count_dict[tree[start]] -= 1
                    if tree_count_dict[tree[start]] == 0:
                        tree_count_dict.pop(tree[start])  
                start += 1
            # update max_tree
            max_tree = max(max_tree, end-start+1)
        return max_tree
        






```