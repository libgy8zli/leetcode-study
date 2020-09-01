
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

Intuition:

1. if the node is a leaf, we can simply set node = None
2. if the node has a right child. Then the node could be replaced by its successor which is somewhere on the right
subtree.Then could process down recursively to delete the successor. 
3. if the node has left child but no right child.  then this node could be replaced by its predecessor which is somewhere on 
the left subtree, then could process down recursively to delete the predecessor. 

```python
class Solution:
    
    def successor(self, node):
        node = node.right
        while node.left:
            node = node.left
        return node.val

    def predecessor(self, node):
        node = node.left
        while node.right:
            node = node.right
        return node.val

    def deleteNode(self, root, key):
        # edge case, if root is None
        if not root:
            return None
        # if the key is greater than root value, 
        # we will look the right substree 
        if key > root.val:
            root.right = self.deleteNode(root.right, key)
        # similary if the key is less than root value, 
        # we will look the left substree to find the match
        elif key < root.val:
            root.left = self.deleteNode(root.left, key)
        else:
            # if we find the match node there are 3 cases:
            # 1. the node is a leaf, we simply set it to None
            if not root.left and not root.right:
                root = None
            # if the node has a right child, we replace the node
            # with its successor, and then traverse down to delete 
            # the successor 
            elif root.right:
                root.val = self.successor(root)
                # traverse to the right to delete the successor 
                root.right = self.deleteNode(root.right, root.val)            
            # if the node has a left child but no right chiild, we replace
            # the node with its predecessor, and then traverse down 
            # to delete the predecessor
            else:
                root.val = self.predecessor(root)
                root.left = self.deleteNode(root.left, root.val)
       
        return root                 
``` 