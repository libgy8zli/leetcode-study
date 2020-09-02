Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

```
For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```
Since we need to traverse all the nodes of each level before go to next level, we will use a BFS 
technique to solve the problem. 

Recursive approach

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    result = None
    def levelOrder(self, root):
        if not root:
            return []
        if not self.result:
            self.result = []
        self.append_node(root, 0)
        return self.result
    
    def append_node(self, node, depth):
        # check the length of result
        # if length of result is 0, we are at root 
        # then we append a empty list
        # if there are two nodes at same level, only 
        # append empty list one time, when second node check
        # the condition, the len(result) = curr_depth + 1
        if len(self.result) == depth:
            self.result.append([])
        # append  node or node at same level
        self.result[depth].append(node.val)
        
        # increment depth by 1 if any child exist 
        if node.left:
            self.append_node(node.left, depth+1)
        if node.right:
            self.append_node(node.right, depth+1)
        return None
```

Iterative approach 
```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right 

class Solution:
    def levelOrder(self, root):
        # if root is None return empty list
        if not root:
            return []
        
        # initial a queue to help track from top down
        result, node_queue = [], [root]
        while node_queue:
            # for each level iteration, init a empty list to store 
            # value of all the node at each level
            level_result = []
            # at each iteration, we get the size of level
            for _ in range(len(node_queue)):
                # deque each node 
                curr_node = node_queue.pop(0)
                # and append to level result list
                level_result.append(curr_node.val)
                # then append left node to node_queue if exist
                if curr_node.left:
                    node_queue.append(curr_node.left)
                if curr_node.right:
                    node_queue.append(curr_node.right)
            # at the end of each level, append level result to final result
            result.append(level_result)
        return result
```