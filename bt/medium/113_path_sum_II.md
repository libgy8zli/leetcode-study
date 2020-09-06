Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.
```
Example:

Given the below binary tree and sum = 22,
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1

Return:
[
   [5,4,11,2],
   [5,8,4,5]
]
```

We can take a similar DFS approach, and pass down the sum after subtracting the current node value 
down along with a list contains the values of current path, if the total in this list equal to 
target path, we will append this list to final one. 

```python
class Solution:
    def pathSum(self, root, sum):
        if not root:
            return None
        # init empty list to hold path whose total equal to total
        # and a list with root, sum - root.val and empty list 
        final_list, node_stack = [], [(root, sum-root.val, [root.val])]
        while node_stack:
            curr_node, curr_sum, curr_path = node_stack.pop()
            if curr_sum == 0 and not curr_node.left and not curr_node.right:
                final_list.append(curr_path)
            if curr_node.left: 
                node_stack.append((curr_node.left, curr_sum-curr_node.left.val, curr_path+[curr_node.left.val]))
            if curr_node.right: 
                node_stack.append((curr_node.right, curr_sum-curr_node.right.val, curr_path+[curr_node.right.val]))
        return final_list
            









```