Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.
```
Example:

Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
Return 2 
```

Iterative with BFS
```python
class Solution:
    def minDepth(self, root):
        if not root:
            return 0
        # initialize a stack with root and depth 1 
        node_queue = [(root, 1)]         
        while node_queue:
            curr_node, depth = node_queue.pop()
            # if reach the first leaf, meaning this is the min depth
            if not curr_node.left and not curr_node.right:
                return depth
            if curr_node.left:
                node_queue.append((curr_node.left, depth+1))
            if curr_node.right:
                node_queue.append((curr_node.right, depth+1))
```