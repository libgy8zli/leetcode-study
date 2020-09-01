Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

 - The left subtree of a node contains only nodes with keys less than the node's key.
 - The right subtree of a node contains only nodes with keys greater than the node's key.
 - Both the left and right subtrees must also be binary search trees.
 
```
Example 1:
    2
   / \
  1   3
Input: [1, 2, 3]
Output: True

Example 2:
    5
   / \
  1   4
     / \
    3   6 
Input: [5, 1, 3, None, None, 3, 6]
Output: False
Explanation: The root node's value is 5 but its right child's value is 4.
```

Basic idea:

when traverse the tree, we need to make sure every node is with a upper and lower range.  
for a node which is the left child of its parent, it should smaller than the parent node, 
and need to pass down the parent value, so none of the nodes in the right subtree is greater
than the parent node. 

similarly , the node which is the right child of its parent, it should be greater than the 
parent node, and also need to pass down the parent value, and make sure none of the nodes
in the left subtree is smaller than the parent node.


Ia. Recursive approach:
```python
class Solution:
    def isValidBst(self, root):
        return self.isValidBstHelper(root, float("-inf"), float("inf"))    
    def isValidBstHelper(self, root, lower, upper):
        if not root:
            return True
        if root.val <= lower or root.val >= upper:
            return False 
        return self.isValidBstHelper(root.left, lower, root.val) and self.isValidBstHelper(root.right, root.val, upper)
```
II. Iterative approach:
    
    1. DFS
    we will use a stack to keep track the node in a LIFO order, and each record in the stack will contain current node, 
    and the lower and upper limits. 
```python
class Solution:
    def isValidBst(self, root):
        if not root:
            return True
        node_stack = [(root, float('-inf'), float('inf'))]
        while node_stack:
            curr_node, lower, upper = node_stack.pop()
            if curr_node.val <= lower or curr_node.val >= upper:
                return False
            
            if curr_node.left:
                node_stack.append((curr_node.left, lower, curr_node.val)) 

            if curr_node.right:
                node_stack.append((curr_node.right, curr_node.val, upper)) 
        return True
```
    2. BFS    
    we will use a queue to keep track the node in a FIFO order, and each record in the stack will contain current node, 
    and the lower and upper limits. 
```python
class Solution:
    def isValidBst(self, root):
        if not root:
            return True
        node_queue = [(root, float('-inf'), float('inf'))]
        while node_queue:
            curr_node, lower, upper = node_stack.pop()
            if curr_node.val <= lower or curr_node.val >= upper:
                return False
            
            if curr_node.left:
                node_queue.append((curr_node.left, lower, curr_node.val)) 

            if curr_node.right:
                node_queue.append((curr_node.right, curr_node.val, upper)) 
        return True
```

III. Inorder traversal

We will do a inorder traversal, if it is a BST, then every node should ordered in ascending order
during inorder traversal

```python
class Solution:
    def isValidBst(self, root):
        if not root:
            return True
        node_stack = [(root, False)]
        prev_val = float('-inf') 
        while node_stack:
            curr_node, visited = node_stack.pop()
            if curr_node:
                if visited:
                    if curr_node.val <= prev_val:
                        return False
                    else:
                        prev_val = curr_node.val
                else:
                    node_stack.append((root.right, False))
                    node_stack.append((root, True))
                    node_stack.append((root.left, False))
        return True
``` 
    