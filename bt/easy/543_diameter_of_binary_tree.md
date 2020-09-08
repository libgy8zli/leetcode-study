Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

```
Example:
Given a binary tree
          1
         / \
        2   3
       / \     
      4   5    
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.
```


Using a recursive DFS approach from bottom up. We will traverse from bottom up, and compare the diameter 
of each node with max diameter of the tree.

```python
class Solution:
    
     def __init__(self):
        # init an attribute to store tree diameter
        self.diameter = float("-inf")

     def diameterOfBinaryTree(self, root):
        pass
    
    def node_diameter(self, root):
        # base case, if root is None
        # return 0 
        if not root:
            return 0 
        # then get current node left node height
        left_node_height = self.node_diameter(root.left)
        # similarly get the right node height
        right_node_height = self.node_diameter(root.right)
        # diameter of current node would be the combine of left and right node height
        diameter = left_node_height + right_node_height
        # then compare to current Tree diamter 
        self.diameter = max(self.diameter, diameter) 
        # for each node height would be the max between left node and right node plus 1 
        return max(left_node_height, right_node_height) + 1



```