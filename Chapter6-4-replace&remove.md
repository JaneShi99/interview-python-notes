### Chapter 6.4: replace and remove

- Goal: write a program that takes as input of  array of chars, demove each 'b' and replace each 'a' by two 'd's.
- also given an integer, represented size, which is the number of entries of the array that operation is to be applied to.
- note that the naive implementation would give an runtime of $O(n^2)$ because each insert or delete would have to move all the other values offsite by 1
- and note that it is trivial is we were to have $O(n)$ space
- but the challenge is: how do you do it with $O(n)$ time and $O(1)$ space?
- __Trick to solve this problem__
  - Disect this problem into two parts:
    - the secret is two pointers!
    - how to remove the `b`'s?
      - this part is easy. just traverse through array and skip the bs, append them till the end
    - how to turn the '`a`'s into '`dd`'s?
      - again two pointers. Traverse through the array, find the number of a's. then allocate extra space, and use two pointers to append from the behid.
- This below method takes $O(n)$ extra time and very little space

```python
def replace_and_remove(size,s):
  # forward iteration, remove 'b' and count 'a'
  # next_write is the next available 
  # index we put the non-b in
  next_write, a_count = 0,0
  for i in range(size):
    if s[i] != 'b':
      s[next_write] = s[i]
      next_write +=1
    if s[i] == 'a':
      a_count +=1
  #now we are done making the a count and number of bs
  
  cur_idx = write_idx -1  # up until this one original array 
  												# is full, we obverse 
    							        # this untransformed one
  write_idx = cur_idx + a_count #where to write from
  final_idx = write_idx + 1 #length of the entire array 
  while cur_idx >=0:
    if s[cur_idx] == 'a':
      s[write_idx-1] = 'd'
      s[write_idx] = 'd'
      write_idx -=2
    else:
      s[write_idx] = s[cur_idx]
      write_idx -=1
    cur_idx -=1
  return final_size
```



- Similar problems include:
  - string processing that replaces i by j where i, j in (. , ? !) ('dot', 'comma', 'question mark', 'exclamation mark') respectively. This is similar to earlier example, do a pass to count number of extra slots needed and work form the back
  - an algorithm that merges two sorted arrays of integers, $A$ length $m$ and $B$ length $n$ and the result should be sorted array of length $m+n$. We merge them in A, which has sufficient space
    - [1,3,5,7,x,x,x] and [2,4,6]
    - idea is to work from the back as well. have two pointers