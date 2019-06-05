### Test for cyclicity

- write a program that takes a LL, and return null if there does not exist a cycle, and the node at the start of the cycle if there exist a cycle.
- is space is not an issue we can use a hash table to store the nodes. 

- this would require O(n) space
- a dumb brute force approach can achieve the in no additional space by doing a double loop i.e. fix a  node and have another one running down. this is O(n^2) time!

- the actual idea to solve this problem: use a slow iterator (who move down by 1 at a time ) and a fast iterator(who move down by 2 at a time )

- the list has a cycle iff two iterators meet. 
- to detect where the cycle exactly is, find start of the cycle by calculating the length of C. Then compute cycle lens and then subtract.