### Chapter 13- Sorting

### Example usingt he sort functionality provided by language's library

- Example: we are given a student class that originally implements compare method by name. By default the array sort library will sort by name. If we want to sort by GPA  we would do have to explicitly specify  how values are compared inside the sort function
- Example:

```python
class Studen(object):
    def __init__(self,name,GPA):
        self.name = name
        self.gpa = gpa
    def __lt__(self,other):
        return self.name < other.name
#initializing the students array
students = [
    Student('A',4,0),
    Student('C',2.0),
    Student('B',3.0),
    Student('D',3.8)
]

#returns a copy of students that is sorted by name
#note that the original students array is unchanged
students_sorted_by_name = sorted(students)

#sort students by GPA
students.sort(key = lambda student:student.GPA)
```

- time complexity for library sorts is O(n log n), most based on quicksort using O(1) extra space

### Tips

- There are usually two types of sorting problems

  - 1. use sorting to make an algorithm problem easier

       in this cse you can use library sort

    2. implement your own sort

       in this case you can use binary trees and heaps for data structure which makes sorting very convenient

### Sorting libraries

- `sort()` sorts a list in place
  - takes two optional arguments: key=None, reverse=False
  - example: to sort by keys: a.sort(key=lambda x: str(x))
- `sorted()` sorts an iterable
  - it returns a new list where the original is unchanged
  - example: b = sorted(a, key = lambda x: str(x))
  - key and reverse works similarly

### 13.1 Exercise

- Task: write a program that takes two sorted arrays as input, and return a new array containing items tat are in both arrays. Input arrays may have duplicates but the resulted array is duplicate-free
- idea: iterate through and comapre the array elements together, this has a runtime of O(m+n)
- idea for writing something iterative:
  - consider all the cases
  - in the while loop, do it one baby step at a time, which makes it very easy for the condition check for the while loop (loop guard)
    - Example: if in one step of the loop, to many processes are updated, then it might have already broken the while guard but it still keeps on going.

```python
def intersection_two_arrays(A,B):
    i,j,intersection = 0,0,[]
    while i < len(A) and j < len(B):
        if A[i] == B[j]:
            if i == 0 or A[i] != A[i-1]:
                #only need to check it once for A, as
                #that suffices to avoid duplicates
               	intersection.append(A[i])
            i,j = i + 1, j + 1
        elif A[i] > B[j]:
            j +=1
        else: #A[i] < B[j]
            i+=1
   return intersection
```





