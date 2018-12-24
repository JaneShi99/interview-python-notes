### Arrays in python

- retrieving and updating array elements take O(1) time
- resizing is infrequent, so for dynamic arrays insertion and updating is still considered O(1) time
- time complexity of deleting the element at index i from an array of length n is  O(n-i), same with adding new element
- trick: take advantage that you can work effficiently on both ends
- Example:
  - given array, with no additional space granted, reorder its entries so even entries appear first
  - solution: having three subarrays from left to right in the order: even, unclassified, odd
  - then using swap while iterating through the array
- solution given by:

```python
def even_odd(A):
    """
    type A: list[int]
    rtype: list[int]
    """
    
    next_even, next_odd = 0, len(A - 1) #this sets the values respectively
    while next_even< next_odd:
        if A[next_even] % 2 == 0:
           next_even+=1
        else:
           A[next_even], A[next_odd] = A[next_odd], A[next_even] #this swaps values
        	next_odd -= 1
```

- this gives time complexity O(n)

- tips:

  - brutes force ways often take O(n) extra space but more tricky ways can take O(1) extra space
  - fill it from the back so you dont have to shift if you were to insert from front
  - overwriting array instead of deleting
  - you should code with subarrays
  - beware of off-by-1
  - when using 2D aaray use parallel logic

- Array libraries:

  - array in python are list type

  - instantiating array

    - [3,5,7,11]
    - [1] + [0] * 10
    - list(range(100))

  - basic operators

    - len(A)
    - A.append(20)
    - A.remove(20)
    - A.insert(2,200)

  - instantiating a 2D array

    - [ [ 2, 3, 4]  , [3, 4] , [6,7, 8, 9] ]
    -   a in A : return whether a is in A

    - 
    - shallow vs deep copy
    - shalow copy: copy.copy(x)
    - deep copy: copy.deepcopy(x)

  - min(A) max(A)

  - slicing 

    - of the form A[i ; j ; k]. Example:
    - A = [1,6,3,4,5,2,7]
    - A[2:4] returns [3,4]
    - A[2:] returns [3,4,5,2,7]
    - A[:4] returns [1,6,3,4]
    - A[:-1] returns [1,6,3,4,5,2]
    - A[-3:] returns [5,2,7]
    - A[-3:-1] returns [5,2]
    - A[1:5:2] returns [6,4]
    - A[5:1:-2] returns [2,4]
    - A[::-1]returns [7,2,5,4,3,6,1]
    - B= A[:] returns a shallow copy
    - A[k:] + A[:k] rotates array a by k elements

  - list comprehension

    - good way to create lists
    - it consists of an input sequence, an iterator over the input sequence, logic condition over the iterator(optional) and expression that yields the elements of derived list
    - examples:
    - [x **2 for x in range (6)]
    - [x **2 for x in range (6) if x % 2 == 0]

  - list comprehension supports multiple layer looping

    - if A = [1,3,5] and B = ['a', 'b'] then 
    - [(x,y) for x in A for y in B] creates (x,y) for all six elements
    - iterating thru 2D array
    - if a = [ [ 1, 2, 3] , [ 4 , 5 ,6 ] ]  then  [ [ x ** 2 for x in row] for row in M] yields [ [ 1, 4, 9 ], [16, 25, 36 ]]



  ### Dutch national flag partitioning problem

  - the problem: you are given an array and pivot. Your task is to re-order the array in a way that the elements less than the pivot stays to the left of pivot and elements to the right to pivot stays to the right
  - trivial with O(n) time but with O(n) additional space. 
  - one way is to: go through the array and keep on swapping them to the right place
  - this below method has O(n) time and O(1) space

  ```python
  def dutch_glag_partition(pivot_index, A):
      pivot = A[pivor_index]
      #first pass: gourp elements smaller than pivot value
      smaller = 0
      for i in range(len(A)):
          if A[i] < pivot:
              A[i], A[smaller] = A[smaller], A[i]
              smaller += 1
      #second pass: group elements larger than pivot value
      larger = len(A) - 1
      for i in reversed(range(len(A))):
          if A[i] < pivot:
              break
          elif A[i] > pivot:
              A[i], A[larger] = A[larger], A[i]
              larger -= 1
  ```

  - this method is complex as it keeps tracks of a previously define index
  - the larger and smaller index keeps track of the element that is currently "out of place" closes to the edge, so that when you encounter a smaller / larger element, it is ready to be swapped

### Solution to the partition problem that only requires one pass

- Although it is faster, it uses a trickier implementation
- we maintain four subarrays: bottom, middle, unclassified, top. Where bottom, middle, and top means elements that are greater than, equal to, and smaller than the pivot, respectively.
- suppose A = <-3, 0, -1,1,1,?,?,?,4,2> where pivot is 1 and the ? are unclassified
- if A[5] is less than pivot, you swap it with the first 1, if it is same as pivot, dont touch it. Otherwise you switch it with the last unclassified element. So each pass you do one action, and it would sit in the right subarray
- i.e. each iteration decreases the size of the unclassified subarray by 1

```python
def dutch_flag_partition(pivot_index, A):
    pivot = A[pivot_index]
    #the following invariants
    # bottom group: A[:smaller]
    # middle group: A[smaller:equal]
    # unclassified group: A[equal: larger]
    # top group: A[Larger:]
    smaller, equal, larger = 0, 0, len(A)
    
    # the while loop keeps on going as long as the unclassified array isnt empty
    while equal < larger:
        # A[equal] is the incoming element to be classified
        if A[equal] < pivot:
            A[smaller], A[equal] = A[equal], A[smaller]
            smaller+= 1
            equal +=1
        elif A[equal] == pivot:
            equal += 1
        else: # A[equal] > pivot
            larger -= 1
            A[equal],A[larger] = A[larger],A[euqal]
            
```

