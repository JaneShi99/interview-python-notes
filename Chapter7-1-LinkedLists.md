### Chapter 7 Linked List

### Linked Lists in python

- it's a data structure that contains a sequence of nodes, where each node contains an object and a reference to the next node.
- first node is called the head
- the last node is he tail, and its next field is null
- list is similar to array, as its data are ordered linearly. Howeverm though, deleting and adding is O(1) time but searching for the element is O(n) time 
- Doubly linked lists works similar, where the first node's prev is null and last node's next is null
- there are ususally two types of problems for linked list, 1. make your own linked list or 2. use the standard list library and solve some problems

### Implementation

```python
class ListNode:
    def __init__(self, data=0, next_node=None):
        self.data = data
        self.next = next_node
        
	def search_list(L,Key):
        while L and L.data!=key:
            L=L.next
        # If the key was not present in the list, L will have become null
        return L
    
    #Insert new_node after node.
    def insert_after(node, new_node):
        new_node.next = node.next
        node.next = new_node
    
    #Delete the node past this one. assume node is NOT a tail
    def delete_after(node):
        onde.next = node.next.next
     
```



### Tips for linked lists

- list problems are ususally simple brute force solution, O(n) space, but existing list nodes can be used to reduce space complexity to O(1)
- focus on writing clean codes for specified problem
- use a dummy head (sentinel), to avoid having to check to empty lists
- it's easy to forget to update next (and prev for doubly linked list) for head and tail
- consider using two iterator

### 7.1 Merge Two sorted list practice problem

```python
def merge_two_sorted_list(L1,L2):
    #creates a placeholder for result
    dummy_head = tail = ListNode()
    
    while L1 and L2:
        if L1.data < L2.data:
            tail.next, L1 = L1, L1.next
        else:
            tail.next, L2 = L2, L2.next
        tail = tail.next
    #Appends the remaining nodes of L1 or L2
    tail.next = L1 or L2
    return dummy_head.next
```























