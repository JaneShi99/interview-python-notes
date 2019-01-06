### Chapter 11- Searching

### Binary Search

- over sorted array
- Time complexity is O(log n)

```python
def bsearch(t,A):
    L, U = 0,len(A)-1
    while L<=U:
        M = L + (U - L)/2 #instead of (L + U)/2 prevent overflow
        if A[M] < t:
            L = M + 1
        elif A[M] = t:
            return M
        else:
            U = M - 1
    return -1
```



### Note that there are many more searching problems that requires more in-depth thinking

### The library binary search functions

```python
#suppose we are given as input an array of students, sorted by descending GOA, ties brokenon name
Student = collections.namedtuple('Student',('name','grade_point_average'))

def comp_gpa(student):
    return(-student.grade_point_average,student.name)
#negative because higher GPA comes first
def search_student(students,target,comp_gpa):
    i = bisect.bisect_left([comp_gpa(s) for s in students], comp_gpa(target))
    return 0<= i<len(students) and students[i] == target
```



- Reference:

https://docs.python.org/3/library/bisect.html

- Note that the bisect_left library function returns the index to the first occurence or the appropriate index that points to the rightmost item smaller or equal to the data point

### Searching libraries functions

- the bisect module provides binary search for sorted list
- `bisect.bisect_left(a,x)` returns the first element not less than a targeted value
- `bisect.bisect_right(b,x)` returns the first element that is greater than a targeted value



### Practice question

- write a method that takes a sorted array, a key, and returns the index of first occurence of the key in the array, and - 1 if it is not in the array
- note that the naive approach is to use binary search, locate the occurence of item and keep going left. But this is worst case O(n) consider the case that all of the items are equal and we are searching for that item
- the following method still preserves a O(log n) time complexity. the idea is, that once we find the item, we record it, and look at the subarray that is currently to its left.

```python
def search_first_of_k(A,k):
    left,right,result = 0,len(A) - 1, -1
    while left<= rigt:
        mid = (left + right)//2
        #note that // is the floor division sign
        if A[mid] > k:
            right = mid - 1
        elif A[mid] = k:
            result = mid
            right = mid - 1
        else: #A[mid] > k
            left = mid + 1
   return result
```









