Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.
```
Example 1:
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

Iterative approach, with BFS 
```python
class Solution:
    def averageOfLevels(self, root):
        if not root:
            return 0 
        # init a queue for bfs 
        node_queue = [root]
        level_avg = []
        while node_queue:
            level_len = len(node_queue)
            level_total = 0
            # then iterate through each level to get average and append next level node to queue 
            for _ in range(level_len):
                curr_node = node_queue.pop(0)
                level_total += curr_node.val
                if curr_node.left:
                    node_queue.append(curr_node.left)
                if curr_node.right:
                    node_queue.append(curr_node.right)
            level_avg.append(level_total/level_len)
        return level_avg
```

Recursive approach with DFS

```python
class Solution:
     
    def averageOfLevels(self, root):
        self.level_avg = []
        self.dfs(root, 0)
        return [i[0]/i[1] for i in self.level_avg]


    def dfs(self, root, depth):
        # use a instance attribute list to track the level 
        # if the length of the list is equal to depth, 
        # which means the current node is the first one in the current depth
        # ex. for root, len(self.level_avg) = len([]) = 0, and root depth is 0, so 
        # append root to the list 
        if len(self.level_avg) == depth:
            self.level_avg.append([root.val,1])  # [root.val, 1] for level total, and level node count 
        # if not equal, that means there are already node in the same level visited, we increment
        # level total and, level node count 
        else:
           self.level_avg[depth][0] += root.val
           self.level_avg[depth][1] += 1
        
        # the go down left , right node of curren node if exist
        # and increment depth by 1
        if root.left:
            self.dfs(root.left, depth+1)
        if root.right:
        self.dfs(root.right, depth+1)
        return None


```

