You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:


````
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
````

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

 

Follow up:

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.


```python
class Solution:
    def connect(self, root):
        if not root:
            return None
        # init and node queue
        node_queue = [root]
        while node_queue:
            # get the current queue length
            curr_len = len(node_queue)
            # for each level init a prev node 
            prev_node = None
            for _ in range(curr_len):
                # dequeue the node
                node = node_queue.pop(0)
                # if prev_node is not None, assign the current node as next 
                # for prev_node
                if prev_node:
                    prev_node.next = node
                # set current node as prev for next iteration
                prev_node = node
                # append left first, then right if exists
                if node.left:
                    node_queue.append(node.left)
                if node.right:
                    node_queue.append(node.right)
        return root
```