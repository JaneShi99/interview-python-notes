### 5.12: sample offline data

Task: implement an algo that takes input as array, of distinct element and size, return a subset of the given size. All subsets should be equally likely. 

Idea: generate a random number within given indices, and then remove it, and keep doing so for another k-1 times.

 However, the catch is to do this task in a way that we can use the number random generator. The most efficiet way to do so is to generate a random number, and 'swap' it to the very back so that we 're done with choosing that piece



```python

def random_sampling(k,A):
  	# k is a value where k <= len(A)
    # return a subset of size k in A
    
    for i in range(k):
      #for each i, A[0:i] is the chosen subset
      rand = random.randint(i, len(A)-1)
      #this swaps it to the beginning
      A[rand], A[i] = A[i], A[rand]
     return A[:k]


```

