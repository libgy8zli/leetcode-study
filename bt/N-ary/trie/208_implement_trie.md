Implement a trie with insert, search, and startsWith methods.

```
Example:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
Note:

You may assume that all inputs are consist of lowercase letters a-z.
All inputs are guaranteed to be non-empty strings.
```

1. First Approach using array 
```python
class TrieNode:
    """
    define a TrieNode class with two attributes:
    1. is_word: to indicate if this node represent the end of word
    2. a list with 26 None to hold potential child
    """
    __slots__ = ['is_word', 'children'] 
    def __init__(self):
        self.is_word = False
        self.children = [None] * 26

class Trie:
    
    def __init__(self):
        # root is always Empty node 
        self.root = TrieNode()
    
    def insert(self, word):
        # start with root node
        curr_node = self.root
        # check each letter in word
        for ch in word:
            # get the letter index use unicode code number 
            # difference
            ch_idx = ord(ch) - ord('a')
            # check if this letter is already in current node children list
            # if it is not in the list, put a New TrieNode to ch's index  
            if not curr_node.children[ch_idx]:
                curr_node.children[ch_idx] = TrieNode()
            # then assign this child to current node
            curr_node = curr_node.children[ch_indx]
        # then once iterate all the letters in the word.
        # change last letter's node is_word to True
        curr_node.is_word = True
        return True
    
    def search(self, word):
        # start with root 
        curr_node = self.root
        for ch in word:
            ch_idx = ord(ch) - ord('a')
            if not curr_node.children[ch_idx]:
                return False 
            curr_node = curr_node.children[ch_idx]
        return curr_node.is_word
    
    def startsWith(self, prefix):  
        curr_node = self.root
        for ch in word:
            ch_idx = ord(ch) - ord('a')
            if not curr_node.children[ch_idx]:
                return False 
            curr_node = curr_node.children[ch_idx]
        return True 
```


2. Second approach using Hashmap(python dictionary)

```python
class TrieNode:
    """
    Instead of using list for 26 letters, we use a dictionary
    to hold the children of current node 
    """
    __slots__ = ['is_word', 'children']
    def __init__(self):
        self.is_word = False
        self.children = {}

class Trie:
    
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        
        curr_node = self.root
        for ch in word:
            # get the child node from current node children list if it exists
            # otherwise assign a empty TrieNode for the key of ch in children
            curr_node.children[ch] = curr_node.children.get(ch, TrieNode())
            curr_node = curr_node.children[ch]
        curr_node.is_word = True
    
    def search(self, word):
        curr_node = self.root
        for ch in word:
            curr_node = curr_node.children.get(ch)
            if not curr_node:
                return False
        return curr_node.is_word
             
    def startsWith(self, word):
        curr_node = self.root
        for ch in word:
            curr_node = curr_node.children.get(ch)
            if not curr_node:
                return False
        return True 
        
```
