Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

```
Example 1:
    3
   / \
  9  20
    /  \
   15   7

Return True

Example 2:
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4

Return False
```

Since the definition of balanced search tree is the difference of left and right subtrees of every node
is no more than 1, we will find the depth of the tree, and compare left and right tree height. 

Recursive approach:
```python
class Solution:
    def tree_height(self, root):
        if not root:
            return 0
        return max(self.tree_height(root.left), self.tree_height(root.right)) + 1

    def isBalanced(self, root):
        if not root:
            return True
        if abs(self.tree_height(root.left)-self.tree_height(root.right)) > 1:
            return False
        return self.isBalanced(root.left) and self.isBalanced((root.right))
```

