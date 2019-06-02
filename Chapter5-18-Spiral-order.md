### Chapter 5-18 Computer the spiral order

- Traverse the array in clockwise, going from outer layer to spiral into inner layer.
- The way I did it was to literally make a copy of the matrix and peel it layer by layer:
  - go 'peel' it, and then remove rows, columns, rows, columns so on and so on
- A uniform way would be to add $n-1$ items from 1st row, $n-1$ items from last column, $n-1$ items (reversed) from first column, $n-1$ items (reversed) from last column, so on and so on. Then, we are left with solving a problem in $(n-2)*(n-2)$ square. Note that this brings uniformity and is clear, because for all sides you are removing an equal number of squares.
- Note that here's a different case for odd `n` because at the end it is just one value left.

