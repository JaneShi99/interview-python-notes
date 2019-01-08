### Chapter 15: Recursion in Python

- Two key points to implement recursion: find the base cases, which are solved directly, and then ensuring the process of bigger cases converging to base cases

### Divisino algorithm

```python
def gcd(x,y):
    return x if y == 0 else gcd(y, x % y)
```



### Tips for recursion

- it's suitable for problems when the input is expressed recursively
- good for search, enumeration, divide-and-conquer
- when you have a deeply nested iteration loops, you might want to consider using recursion instead
- removing recursion -> mimics call stack with the stack data structure
- tail recursive recursion can be just reduced to a while loop
- if recursive funcion calls the save argument more than once, cache the result (DP)



### Exercise 15.1 Towers of hanoi

