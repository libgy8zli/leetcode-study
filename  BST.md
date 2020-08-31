##BST 

Binary search tree is a binary tree where each node contains a key and an optional associated value.
It allows particularly fast lookup, addition, and removal of items. And each node is arranged
following these properties:

    1. The left subtree of a particular node always contain keys with value less
    than the value of the node.
    2. The right subtree of a particular node always contain keys with value greater
    than the value of the node. 
    3. The left and right subtrees are also binary search tree. 
    
BST node:
```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

####pre-order traversal will visit node in this order: **root-left-right**.

Recursive approach:
```python
def preorder(root):
    result = []
    if root:
        result.append(root.val)
        result += preorder(root.left)
        result += preorder(root.righ)
    return result
```

Iterative approach:
```python
def preorder(root):
    result = []
    node_stack = [(root, False)]
    while node_stack:
        curr_node, visited = node_stack.pop()
        if curr_node:
            if visited:
                result.append(curr_node.val)
            else:
                node_stack.append((root, True))
                node_stack.append((root.left, False))
                node_stack.append((root.right, False))
    return result 
```

####in-order traversal will visit node in this order: **left-root-right**.

Recursive approach:
```python
def inorder(root):
    result = []
    if root:
        result = inorder(root.left)
        result.append(root.val)
        result += inorder(root.right)
    return result 
```
Iterative approach:
```python
def inorder(root):
    result = []
    node_stack = [(root, False)] # use a stack keep the node in LIFO order. 
    while node_stack:
        curr_node, visited = node_stack.pop()
        if curr_node:
            if visited:
                result.append(curr_node.val)
            else:
                node_stack.append((curr_node.right, False))
                node_stack.append((curr_node, True))
                node_stack.append((curr_node.left, False))
    return result
```

####post-order traversal will visit node in this order: **left-right-root**.

Recursive approach:
```python
def postorder(root):
    result = []
    if root:
        result += postorder(root.left)
        result += postorder(root.right)
        result.append(root)
    return result 
```

Iterative approach:
```python
def postorder(root):
    result = []
    node_stack = [(root, False)]
    while node_stack:
        curr_node, visited = node_stack.pop()
        if curr_node:
            if visited:
                result.append(curr_node.val)
            else:
                node_stack.append((root, True))
                node_stack.append((root.right, False))
                node_stack.append((root.left, False))
    return result
```