Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

```
Example:
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

Iterative approach with BFS,  we will search each level, and only append the last 
node at each level to final result:

```python
class Solution:
    def rightSideView(self, root):
        if not root:
            return []
        #inital empty list, and a queue with root
        result, node_queue = [], [root]     
        while node_queue:
            # get current level length
            curr_level_len = len(node_queue)
            for i in range(curr_level_len):
                # for all the node in current level
                # pop them out from front (dequeue)
                curr_node = node_queue.pop(0)
                # if it is the last element in the level append
                # to final result
                if i == curr_level_len - 1:
                    result.append(curr_node.val)
                # append left , right to queue (enqueue) if not None
                if curr_node.left:
                    node_queue.append(curr_node.left)
                if curr_node.right:
                    node_queue.append(curr_node.right)
        return result
```

Iterative approach with DFS

```python
class Solution:
    def rightSideView(self, root):
        if not root:
            return []
        # init empty list for final result
        # and stack to traverse in a LIFO order
        result, node_stack = [], [(root, 0)]
        while node_stack:
            curr_node, level = node_stack.pop()
            # if the level is equal to the length of final result
            # which means we need to append the node, if there 
            # is a left node at same level, the final result length 
            # is already increased by 1 for the same level right node
            # so the length of final node will be 1 greater then left node depth
            if level == len(result):
                result.append(curr_node.val)
            # enter the left node first:
            # and increment level by 1 
            # and have right node out first for next iteration
            if curr_node.left:
                node_stack.append((curr_node.left, level+1))
            if curr_node.right:
                node_stack.append((curr_node.right, level+1))
        return result
```

similar to the iterative DFS approach,  recursive approach:
```python
class Solution:
    def rightSideView(self, root):
        if not root:
            return []
        
        right_side_view = []
        def helper(node, depth):
            if depth == len(right_side_view):
                right_side_view.append(node.val)
                
            
            if node.right:
                helper(node.right, depth+1)
                
            if node.left:
                helper(node.left, depth+1)
            
        helper(root, 0)
        return right_side_view


```