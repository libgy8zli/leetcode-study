Given a node in a binary search tree, find the in-order successor of that node in the BST.

If that node has no in-order successor, return null.

The successor of a node is the node with the smallest key greater than node.val.
You will have direct access to the node but not to the root of the tree. Each node will have a reference to its parent node. Below is the definition for Node:
```python 
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
```

```
Example 1:
    2
  /   \
 1     3
Input: [2, 1, 3] p = 1
Output: 2
Explanation: 1's in-order successor node is 2. Note that both p and the return 
value is of TreeNode type.

Example 2: 
            5
          /   \
        3      6
       / \   
      2   4 
     / 
    1
Input: [5, 3, 6, 2, 4, None, None, 1], p = 6
Output: None
Explanation: There is no inoder successor of the current node, so the answer is None
```
```
Example 1:
    2
  /   \
 1     3
Input: [2, 1, 3] p = 1
Output: 2
Explanation: 1's in-order successor node is 2. Note that both p and the return 
value is of TreeNode type.

Example 2: 
            5
          /   \
        3      6
       / \   
      2   4 
     / 
    1
Input: [5, 3, 6, 2, 4, None, None, 1], p = 6
Output: None
Explanation: There is no inoder successor of the current node, so the answer is None
```
There are two scenarios: 

1. if the node has right node: Since the successor will be the smallest value on the right substree of current node. we can traverse
start with the immediate right node of current node, and keep finding the left node downstream 
2. if the node does not have a right node, we will traverse back to the parent until the current node is 
not parent node's right node.

`````python
class Solution:
    def inorderSuccessor(self, node):
        if node.right:
            node = node.right
            while node.left:
                node = node.left
            return node 
        while node.parent and node == node.parent.right:
            node = node.parent
        return node.parent
`````

Similarly question:
find the predecessor of node:

1. if the node has left node: Since the predecessor will be the biggest value on the left substree of current node. we can traverse
start with the immediate left node of current node, and keep finding the right node downstream 
2. if the node does not have a left node, we will traverse back to the parent until the current node is 
not parent node's left node.

```python
class Solution:
    def inorderpredecessor(self, node):
        if not node:
            return None
        if node.left:
            node = node.left
            while node.right:
                node = node.right
            return node 
        while node.parent and node == node.parent.left:
            node = node.parent
        return node.parent
            

```