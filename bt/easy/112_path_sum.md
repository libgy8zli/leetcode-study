Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.
```
Example:

Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

Iterative DFS approach 
1. Start with DFS with the root of the tree, and target_sum - root.val to pass down 
2. if current node is a leaf, and the target sum passed down from top equal to 0
    which means we find a path.
   if current node is not a leaf,  pass down target sum with child values substracted. 
   and enter into stack.    
   
(change node_stack.pop() to node_stack.pop(0), this is a iterative BFS approach)
   
````python
class Solution:
    def HasPathSum(self, root, sum):
        # early stop if root is None
        if not root:
            return None
        # init stack 
        node_stack = [(root, sum-root.val)]
        while node_stack:
            curr_node, curr_sum = node_stack.pop()
            if curr_sum == 0 and not curr_node.left and not curr_node.right:
                return True
            if curr_node.left:
                node_stack.append((curr_node.left, curr_sum - curr_node.left.val))
            if curr_node.right:
                node_stack.append((curr_node.right, curr_sum - curr_node.right.val))
        return None
````

Similarly, we can have a recursive approach 
```python
class Solution:
    def HasPathSum(self, root, sum):
        if not root:
            return None
        if root.val == sum and not root.left and not root.right:
            return True
        return self.HasPathSum(root.left, sum - root.val) or self.HasPathSum(root.right, sum - root.val)




```