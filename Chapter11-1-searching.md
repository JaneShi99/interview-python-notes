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

