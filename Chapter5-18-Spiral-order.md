### Chapter 5-18 Computer the spiral order

- Traverse the array in clockwise, going from outer layer to spiral into inner layer.
- The way I did it was to literally make a copy of the matrix and peel it layer by layer:
  - go 'peel' it, and then remove rows, columns, rows, columns so on and so on
- A uniform way would be to add $n-1$ items from 1st row, $n-1$ items from last column, $n-1$ items (reversed) from first column, $n-1$ items (reversed) from last column, so on and so on. Then, we are left with solving a problem in $(n-2)*(n-2)$ square. Note that this brings uniformity and is clear, because for all sides you are removing an equal number of squares.
- Note that here's a different case for odd `n` because at the end it is just one value left.

```python
def matrix_spiral(square_matrix):
  #the smarts of this algorithm
  # 1. have n-1 values per side, and each four iterations unwraps an entire layer
  # 2. since each 'move' is like right, down, left, right, instead of writing four different codes (lots of repeats) we just use a direction control that's good
  
  SHIFT = ((0,1),(1,0),(0,-1),(-1,0))
  direction = x = y = 0
  spiral_ordering = []
  for _ in range(len(square_matrix **2)):
    spiral_ordering.append(square_matrix[x][y])
    square_matrix[x][y] = 0 #to reset. Note that we set this value to 0 or any other values not already in the array
    next_x,next_y = x + SHIFT[direction][0], y+ SHIFT[direction][1]
    if (next_x not in range(len(square_matrix)) or next_y not in range(len(square_matrix)), or square_matrix[next_x][next_y] == 0):
      direction = (direction + 1) & 3
      next_x,next_y = x + SHIFT[direction][0], y + SHIFT[direction][1]
      
    x , y = next_x, next_y
  return spiral_ordering
```

