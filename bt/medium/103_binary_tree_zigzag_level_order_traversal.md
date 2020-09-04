Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

```
For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7

return its zigzag level order traversal as:
[
  [3],
  [20,9],
  [15,7]
]
```

Similar to level order traversal, in additional to LOT,  we need one variable to track 
wether we need to reverse a list of node in one level before append to final list. 

```python
class Solution:
    def zigzagLevelOrder(self, root):
        if not root:
            return None
        # init a queue to track 
        final_list, node_queue = [], [root]
        # init reverse indicator
        reverse = False 
        while node_queue:
            level_result = []
            level_len = len(node_queue)
            for _ in range(level_len):
                curr_node = node_queue.pop(0)
                if not reverse:
                    level_result.append(curr_node.val)
                else:
                    level_result = [curr_node.val] + level_result
                if curr_node.left:
                    node_queue.append(curr_node.left)
                if curr_node.right:
                    node_queue.append(curr_node.right)
            # append level result to final list
            final_list.append(level_result)
            # switch reverse at end of each level
            reverse = not reverse 
        return final_list        
```

DFS iterative approach 
```python
class Solution:
    def zigzagLevelOrder(self, root):
        if not root:
            return None
        # init the final list and node stack with root and root level
        final_list, node_stack = [], [(root, 0)]
        while node_stack:
            curr_node, curr_level = node_stack.pop()
            # if the curr_level equal to length of final_list
            # that means this node is the first one in curr level 
            # ex. final_list = [] len = 0 ,  root level is 0 
            if curr_level == len(final_list):
                final_list.append([curr_node.val])
            else:
                if curr_level % 2 == 0:
                    final_list[curr_level].append(curr_node.val)
                else:
                    final_list[curr_level] = [curr_node.val] + final_list[curr_level]
            # need to append right node first if exist, since this is a LIFO order
            # so the left node will exist first
            # and make sure the reverse or not align with calculation of curr_level % 2 == 0
            if curr_node.right:
                node_stack.append((curr_node.right, curr_level+1))
            if curr_node.left:
                node_stack.append((curr_node.left, curr_level+1))

        return final_list
            
```