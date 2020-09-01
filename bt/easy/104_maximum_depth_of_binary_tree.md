Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

```
Example:

Given binary tree [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
Return 3
```

Recursive
```python
class Solution:
    def tree_height(self, root):
        # base case, if the node is None return 0
        if not root:
            return 0
        return max(self.tree_height(root.left), self.tree_height(root.right)) + 1
```

The intuition is to traverse the tree and record the maximum depth during the traverse:
```
    1
   / \
  2   7
 / \
3   4
   / \
  5   6


height(1) = 1 + max(height(2), height(7))
height(2) = 1 + max(height(3), height(4))
height(7) = 1 + max(0, 0)  # it is a leaf
height(3) = 1 + max(0, 0)  # it is a leaf 
height(4) = 1 + max(height(5), height(6))
height(5) = 1 + max(0, 0)
height(6) = 1 + max(0, 0)
               ||
              \  /
               \/

Going bottom-up:

height(4) = 1 + max(1, 1) = 2
height(2) = 1 + max(1, 2) = 3 
height(1) = 1 + max(3, 1) = 4
```

Iterative with BFS:
```python
class Solution:
    def maxDepth(self, root):
        if not root:
            return 0 
        node_queue = [(root, 1)]     
        max_depth = float("-inf")
        while node_queue:
            curr_node, depth = node_queue.pop()                                      
            max_depth = max(max_depth, depth)
            if curr_node.left:
                node_queue.append((curr_node.left, depth+1))
            if curr_node.right:
                node_queue.append((curr_node.right, depth+1))
        return max_depth
```