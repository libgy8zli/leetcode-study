Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

The successor of a node p is the node with the smallest key greater than p.val

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

1. Flattening the BST inorder, and return the value right next to p, if p is not at the end 
of flattened list, otherwise return None

```python
class Solution:
    def inorderSuccessor(self, root, p):
        result = []
        p_idx, temp_p_idx = 0, 0
        node_stack = [(root, False)]
        while node_stack:
            curr_node, visited = node_stack.pop()
            if curr_node:
                if visited:
                    if curr_node.val != p.val:
                        temp_p_idx += 1
                    else:
                        p_idx = temp_p_idx
                    result.append(curr_node)
                else:
                    node_stack.append((curr_node.right, False))
                    node_stack.append((curr_node, True))
                    node_stack.append((curr_node.left, False))
        
        if p_idx + 1 > len(result) - 1:
            return None
        else:
            return result[p_idx+1]
```

2. 
    The immediate successor would be the smallest value for all the nodes in the right subtree of the node with 
    value equal to p. We keep traversing down the tree, if p.val smaller than current node, then current node is one
    candidate, then go to the left subtree to see if we can find a smaller one. if p.val greater or equal than current
    node, then the right subtree contains the answer. 
    
```python
class Solution:
    def inorderSuccessor(self, root, p):
        result = None
        while root:
            if p.val < root.val:
                result = root
                root = root.left
            else:
                root = root.right
        return result
```