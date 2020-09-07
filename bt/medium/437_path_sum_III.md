You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.
```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11

```

Similar to question 560, we can use prefix sum approach for this one 

There are two situations we need to consider:
1. The tree path with the target sum starts from the root,  then if cum_sum == target_sum,
then increment the count by 1
2. The tree path with the target sum with somewhere downwards, that means we should add the counts 
of cum_sum - target_sum has been seen,  because cum_sum - (cum_sum-target_sum) = target_sum.  the 
reason we add the count is to capture all the extended up or down sequences where elements cancel.

Note: once the current subtree processed, need to remove current cum_sum from the hash map,  just 
in case the parallel subtree continue on this cum_sum 


```python
class Solution:
    def pathSum(self, root, sum: int):
        if not root:
            return None
        # init a dicitonary to store the counts of prefix sum has been seen so far
        prefix_sum = {} 
        path_count, node_stack = 0, [(root, root.val, False)]
        while node_stack:
            curr_node, cum_sum, visited = node_stack.pop()
            # if already visited, need to remove the cum_sum from 
            # hash map
            if visited:
                prefix_sum[cum_sum] -= 1
                continue 
            # if not vistied:
            # check if cum_sum equals sum for situation 1
            if cum_sum == sum:
                path_count += 1
            # also increment path_count by the count of cum_sum-sum for situation 2
            path_count += prefix_sum.get(cum_sum-sum, 0)
            # finally increment the count of current cum_sum
            prefix_sum[cum_sum] = prefix_sum.get(cum_sum, 0) + 1
            # append cum_sum back with visited = True 
            node_stack.append((None, cum_sum, True))
            # pass down cum sum to each left and right node if exists
            if curr_node.left:
                node_stack.append((curr_node.left, curr_node.left.val + cum_sum, False))
            if curr_node.right:
                node_stack.append((curr_node.right, curr_node.right.val + cum_sum, False))
        return path_count
```

```
every node_stack and prefix_sum for example
[1, -2, -3]
-1 

# iteration-0 initial node_stack with just root
# inital prefix_sum {}
[(<__main__.TreeNode object at 0x7f6354066710>, 1, False)]
{}
--------

# iteration-1, append both left and right child to node_stack. update prefix_sum
# left child cum_sum 1 - 2 = -1
# right child cum_sum 1 - 3 = -2
[(None, 1, True), (<__main__.TreeNode object at 0x7f6354066990>, -1, False), (<__main__.TreeNode object at 0x7f6354066950>, -2, False)]
{1: 1}
--------
# iteration-2 
# pop out right node, and update prefix sum, since it is processed, append (None, -2, True) back
# to remove -2 for next iteration 
[(None, 1, True), (<__main__.TreeNode object at 0x7f6354066990>, -1, False), (None, -2, True)]
{1: 1, -2: 1}
--------
# iteration-3
# remove right node cum_sum 
[(None, 1, True), (<__main__.TreeNode object at 0x7f6354066990>, -1, False)]
{1: 1, -2: 0}
--------
# iteration-4 
# process left child ,by update prefix_sum
[(None, 1, True), (None, -1, True)]
{1: 1, -2: 0, -1: 1}
--------
[(None, 1, True)]
{1: 1, -2: 0, -1: 0}
--------




```