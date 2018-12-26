### Chapter 9 Binary Trees

- A binary tree is either empty, or a root node r with a left binary tree and a right binary tree
- Occur very commonly in binary tree searches

### Prototype of a binary tree

```Python
class BinaryTreeNode:
    def __init__(self, data=None,left=None,right=None):
        self.data = data
        self.left = left
        self.right = right
```



### Basic properties of a binary tree

- search path is the unique path that leads from the root to a particular node
- a full binary tree is a tree where every node other than the leaf has two children
- a perfect binary tree is a full binary tree and all the leafs are same depth, each parent has two children. It has 2^(h+1)-1 nodes and 2^h of them are leafs
- a perfect/complete bin tree has height floor(log n)
- key words: depth, height,  ancestor, descendant, leaf, etc
- you have pre-order, post-order and in-order traversals **(implementation is trivial)**



### Tips for binary trees

- use recursive algorithms
- consider left and right skewed trees wheenver doing complexity analysis because they are outliers
- dont make the mistake of treating a node that has single child as leaf!



### 9.1 Test if binary tree is height balanced

- a binary tree is height balanced if for each node, | height(left)-height(right) | <=1
- write a program to check whether binary tree is height balanced
- **Idea 1** brute force: compute height for each node then do a recursive compare O(n) time and O(n) space
- **Idea 2** observe that all we need to know for a subtree is 1. whether it is height balanced 2. whats its height

```python
def is_balanced_binary_tree(tree):
    BalancedStatusWithHeight = collections.namedtuple('BalancedStatusWithHeight', ('balanced','height'))    
    #first value tells you whether it is balanced
    #second value tells you its height
    #this is the return type that gives you a structure to work with, where it contains useful information for
    #both return and for the numeric check

    #you expect BalancedStatusWithHeight return type for all of 
    #the returns in the helper recursive fuction and eventually
    #you return the field of the tree in that function
    def check_balanced(tree):
        if not (tree):
            return BalancedStatusWithHeight(True, -1) #base case for a null node
        left_result = check_balanced(tree.left)
        if not left_result.balanced:
            return BalancedStatusWithHeight(False,0)

        right_result = check_balanced(tree.right)
        if not right_result.balanced:
            return BalancedStatusWithHeight(False,0)

        is_balanced = abs(left_result.height - right_result.height) <= 1
        height = max(left_result.height,right_result.height) + 1
        return BalancedStatusWithHeight(is_balanced,height)
    return check_balanced(tree).balanced
```

- note that post-order traversal is used to maximize efficiency

### Exercise 9.1

- write a program that returns the size of largest complete subtree
- design an algorithm that takes in a tree and integer k and check whether the tree is k-balanced

### Writing functions

- it is helpful to define a helper struct and a helper function within a bigger function
- for functions that requires recursion, you can define 
  -  a struct (namedtuple) that will hold useful info for each layer of recursion
  - a helper function that only returns that specific struct
  - then eventually you use that helper function on your input, and extract the needed field from the return struct