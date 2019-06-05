### Chapter 7: reverse a single sublet



- goal is to write a program that takes a singly linkedl ist L, two integers $s$ and $f$ as arguments, and then inclusively reverset he order from $s$th node to $f$th node.
- the idea is that we do a single pass. Comibing the identification of sublist with its reversal. and keep counting?
- I am not sure about the verbal explanation. let's see the algoritm

```python
def reverse_sublist(L, start, finish):
  dummy_head = sublist_head = ListNode(0,L)
  
  #we first get to the start of the array first
  #note that our LL index starts at 1
  for _ in range(1,start):
    sublist_head = sublist_head.next
    
  #reverse sublist starting at this index
  sublist_iter = sublist_head.next
  for _ in range(finish - start):
    sublist_iter.next, temp.next, sublist_head.next = \
    (temp.next, sublist_head.next, temp)
   
 	return dummy_head.next
  
```



The complexity is O(f)

it keeps on moving down and down the list. you would have one item, and one temp at a time. each time move down by two and two at a time. 

very smart algorithm. has a tmp s.t.

 tmp.next = sublist head.next

sublist_iter.next = temp.next

sublist.head.next = temp