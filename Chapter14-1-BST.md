### Chapter 14-1 BSTs in Python

### Notes: 

- BST are a very robust data structure. If used effectively, it is the data structure that can be used to solve almost all data structure problems
- Why? They can efficiently:
  - look for min/max
  - add/delete key
  - enumerate keys in a specific range, sorted
  - look for successor or predeccesor of search key
- red-black trees are an example of height balanced BSTs. They are commonly used for library functions
- avoid putting mutables in BSTs, or else you would have to update the BST as you update the object
- The following is the BST prototype

```python
class BSTNode:
    def __init__(seld,data=None,left=None,right=None):
        self.data, self.left, self.right = data,left,right
```

- check if key present, has a O(height) runtime

```python
def search_bst(tree,key):
    return (tree
           if not tree or tree.data == key else search_bst(tree.left,key)
if key < tree.data else search_bst(tree.right,key)
```

### !!! COME BACK TO THIS PIECE OF CODE LATER BECAUSE I DONT QUITE GET IT

### Tips / Binary Tree libraries

- notes that python does not come with a built-in BST library

- use `sortedcontainers` module for binary tree 
- example: `t=bintrees.RBTree([(5,'A'),(2,'B'),(9,'J')])` 
- functions: insert(e), discard(e), min_item(), max_item(), min_key(),max_key(),pop_min(),pop_max()



### Exercisde 14.1

- given a binary tree, check whether it satisfy the property of a binary search tree.
- If we approach this problem with looking at a BST's definition, we would for each node, make sure it's greater than or equal to max from left and less than or equal to min from the right. This could take a long time(worse case O(n^2))
- a smarter approach is to look at the bound constraints from top down, achieving O(n) efficiency. i.e. keep on refining the range of the possible key value for each node. Updating the lower and upper bounds, make the bounds as tight as possible to provide the range of values

```python
def is_bt_bst(tree):
    QueueEntry = collections.namedtuple('QueueEntry',('node','lower','upper'))
    bfs_queue = collections.deque([QueueEntry(tree,float('-inf'),float('inf'))])
    
    while bfs_queue:
        front = bfs_queue.popleft()
        if front.node:
            if not front.lower<=front.node.data<=front.upper:
                return False
            bfs_queue =+[
                QueueEntry(front.node.left,front.lower,front.node.data),
                queueEntry(front.node.right,front.node.data,front.upper)
            ]
    return True
```













