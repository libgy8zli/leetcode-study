Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

```
Example 1:

Input: [1,2,3]

       1
      / \
     2   3

Output: 6
Example 2:

Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

Similary to question 543 diameter of tree, we can use a similar approach to do a DFS from bottom up 

```python
class Solution:
    def __init__(self):
        self.max_sum = float("-inf")
    def maxPathSum(self, root):
        pass
    def bottom_up_recursive(self, root):
        # base case 
        if not root:
            return 0
        # the max path sum of current node, would be the 
        # the left node max path sum + right node max path sum + curr_node.val
        # but we need to compare left and right node max path sum with 0 
        # if one of them (or both) is smaller than 0 , we will exclude it 
        left_node_sum = max(self.bottom_up_recursive(root.left),0)
        right_node_sum = max(self.bottom_up_recursive(root.right), 0)
        curr_max_sum = left_node_sum + right_node_sum + root.val
        # compare with tree overall
        self.max_sum = max(self.max_sum, curr_max_sum)
        return max(left_node_sum, right_node_sum) + root.val


```

