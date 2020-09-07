Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

Note: A leaf is a node with no children.

```
Example:

Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.

Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

iterative approach
```python
class Solution:
    def sumNumbers(self,root):
        if not root:
            return None
        # init cum sum for all the path and node_stack with root and root.val
        cum_sum , node_stack = 0, [(root, root.val)]
        while node_stack:
            curr_node, curr_num = node_stack.pop()
            # if current node is a left, add the num to cum_sum
            if not curr_node.left and not curr_node.right:
                cum_sum += curr_num
            # if left or right or both exist, add curr_num * 10 to left or right node
            if curr_node.left:
                node_stack.append((curr_node.left, curr_num*10+curr_node.left.val))
            if curr_node.right:
                node_stack.append((curr_node.right, curr_num*10+curr_node.right.val))
        return cum_sum
```

Recursive approach 
```python
class Solution:
    def __init__(self):
        self.cum_sum = 0 
    def sumNumbers(self, root):
        if not root:
            return 0 
        self.recursive_dfs(root, root.val)
        return self.cum_sum
    def recursive_dfs(self, node, curr_num): 
        if not node.left and not node.right: 
            self.sum_sum += curr_num
        if node.left:
            self.recursive_dfs(node.left, curr_num*10+node.left.val)
        if node.right:
            self.recursive_dfs(node.right, curr_num*10+node.right.val)
        return None

```