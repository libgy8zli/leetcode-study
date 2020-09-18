First solution - Array 

The first solution is to use an array to store children nodes. 

For instance, if we store strings which only contains letter a to z, we can 
declare an array whose size is 26 in each node to store its children nodes. ANd
for a specific character c, we an use c- 'a' as the index to find the corresponding
child node in the array.  It is really fast to visit a child node. it is comparatively easy
to visit a specific child since we can easily transfer a character to an index in 
most cases. But not all children nodes are needed. So there might be some 
waste of space.



Second solution - Map
The second solution is to use a hashmap to store children nodes. we can declare a 
hashmap in each node. The key of the hashmap are characters and the value is the 
corresponding child node. It is even easier to visit a specific child directly by corresponding character.
But it might be a little slower than using an array. However, it saves some space since 
we only store the children nodes we need. it s more flexible because we are not limited 
by a fixed length and fixed range. 

We mentioned how to represent the children nodes in Trie node, besides, we might need some other 
values. For example, as we know, each Trie node represents a string but not all the strings 
represented by Trie nodes are meaningful. If we only want to store words in a Trie, we might 
declare a boolean in each node as a flag to indicate if the string representedy b
this node si a word or not. 


