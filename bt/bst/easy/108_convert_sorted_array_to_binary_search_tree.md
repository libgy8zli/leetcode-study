Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

```
Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

Because the difference of height of left and right subtree of every node is no more than 1, we can pick
the middle point as root, and then recursively pick the mid point of left half array as current node's left
node, and mid point of right half array as current node's right node.

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right 

class Solution:
    def sortedArrayToBST(self, nums):
        if not nums:
            return None
        mid = (len(nums) - 1 ) // 2
        root = TreeNode(nums[mid])
        root.left = self.sortedArrayToBST(nums[:mid])
        root.right = self.sortedArrayToBST(nums[mid+1:])
        return root


``` 