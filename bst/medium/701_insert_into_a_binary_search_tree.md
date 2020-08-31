Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

Note that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

```
Example 1:
Given the tree:
        4
      /   \ 
     2     7 
    / \
   1   3
Add the value to insert: 5
        4
      /   \ 
     2     7 
    / \   /
   1   3  5
This tree is also valid:
        5
      /   \ 
     2     7 
    / \   
   1   3
        \
         4
```
Constraints:

  - The number of nodes in the given tree will be between 0 and 10^4.
  - Each node will have a unique integer value from 0 to -10^8, inclusive.
  - -10^8 <= val <= 10^8
  - It's guaranteed that val does not exist in the original BST.
  
Recursive approach

```Python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right 

class Solution:
    def insertIntoBST(self, root, val):
        if not root:
            return TreeNode(val)
        if val > root.val:
            if not root.right:
                root.right = TreeNode(val)
            else:
                self.insertIntoBST(root.right, val)
        elif val < root.val:
            if not root.left:
                root.left = TreeNode(val)
            else:
                self.insertIntoBST((root.left, val))
        return root
```

Iterative approach 
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right 

class Solution:
    def insertIntoBST(self, root, val):
        if not root:
            return TreeNode(val) 
        node = root 
        while node:
            if node.val > val:
                if not node.left:
                    node.left = TreeNode(val)
                    return root
                else:
                    node = node.left
            elif node.val < val:
                if not node.right:
                    node.right = TreeNode(val) 
                    return root
                else:
                    node = node.right
        


```