Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

```
Examples 1:
Input: [3,9,20,null,null,15,7]

   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7 

Output:

[
  [9],
  [3,15],
  [20],
  [7]
]

Examples 2:

Input: [3,9,8,4,0,1,7]

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7 

Output:

[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]

Examples 3:

Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5)

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

Output:

[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]

```


Intuition: 
```
Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5)

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2
we can start with BFS approach and use dictionary track the column index, and set root column 
index as 0,  if we move to the left, column index decrement by 1, if we move to the right 
column index increment by 1

3: 0 
9: column_index(3) - 1 = 0 - 1 = -1   # left
4: column_index(9) - 1 =  -1 - 1 = -2 # left
0: column_index(9) + 1 =  -1 + 1 = 0  # right
5: column_index(0) - 1 =   0 - 1 = -1 # left
2: column_index(0) + 1 =   0 + 1 = 1  # right
8: column_index(3) + 1 = 0 + 1 = 1    # right
1: column_index(8) - 1 = 1 - 1 = 0    # left
7: column_index(8) + 1 = 1 + 1 = 2    # right


{
  -2: [4],
  -1: [9, 5], 
   0: [3, 0, 1],
   1: [8, 2],
   2: [7]
}
```

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def verticalOrder(self, root):
        # root is None, return empty list
        if not root:
            return []
        # init a dictionary to track column index and element
        # can use collections.defaultdict(list) 
        col_dict = {} 
        # use a queue to track node and column index, 
        # start with root with column index 0
        # if move to left, decrement by 1
        # if move to right, increment by 1
        node_queue = [(root, 0)]
        while node_queue:
            curr_node, curr_col_idx = node_queue.pop(0)
            # append to the list in the dictionary with key == curr_col_idx
            col_dict[curr_col_idx] = col_dict.get(curr_col_idx, []) + [curr_node.val]
            # if left child, col index decrement by 1, and append to queue
            if curr_node.left:
                node_queue.append((curr_node.left, curr_col_idx-1))
            if curr_node.right:
                node_queue.append((curr_node.right, curr_col_idx+1))
        # only return the values in the dictionary, but sort by key
        return [v for _, v in sorted(col_dict.items(), key=lambda item:item[0])]
            
```

