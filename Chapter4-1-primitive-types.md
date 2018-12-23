### Chapter 4 Primitive Types

### 1. Primitive types

```python
def count_bits(x):
    """
    this counts the number of bits that are needed to represent the integer x
    """
    num_bits = 0
    while x:
        num_bits += x & 1
        x >>= 1
    return num_bits
```



- |, &, ^ means bitwise or, bitwise and, bitwise xor respectively
- ">>" means the shift operator. 
  - a = 60
  - then c = a >> 2;
  - print (c) returns 0000 1111, since a's binary representation is 0011 1100, and after 2 shifts to the right it would become 0000 1111
- the line `num_bits += x&1` 
- integers in pyhon3 has unbounded size
- negatve numbers- treated as their 2's complement value
- numeric methods in python include:
  - `abs(x), math.ceil(x),math.floor(x),min(x,y),pow(x,y),math.sqrt`
  - conversions include: `str(42),int('42'),float('3.14')` etc
- computing the parity of a binary word

### The brute force algorithm for counting parity

```python
def parity(x):
    """
    THE BRUTE FORCE ALGORITHM
    this computes the parity of a binary word, where the parity is defined as the number of 1s in its
    binary expansion modulo 2
    """
    answer = 0
    while x:
        answer ^= x & 1
        x >>= 1
    return answer


```

- This goes through the number digit wise, so O(n) time

- answer ^= x & 1, where ^ is the xor which is the same as addition mod 2

### More elegant ways

```python
def parity1(x):
    """
    THE ALGORITHM THAT CUTS DOWN IN CHUNKS
    this uses the trick that drops non-zero bits one at a time
    """
    result = 0
    while x:
        result ^= 1
        x &= x - 1 # it drops the lowest non-zero bit from x, a.k.a it accumulates 1 mod 2 whenever encounters nonzero bit
       
    return result
```



- Trick: x & (x-1) gives you x with its lowest (lowest non-zero) bit erased
- Trick: x & ~(x-1) isolates lowest bit that is 1 in x, ~ is bitwise complement
- so you keep on doing the x & x - 1 loop and xor (the digits)

### Introducing caching

- idea is to create a look up table: 
  - <0,1,1,0> corresponds to ((00),(10),(01),(11))
  - then just keep on using this table and creating new strings but in reduced size
- Bit mask in python
  - bit masking just "extracts" the value at exact positions in the binary word

```python
def parity2(x):
    """
    this uses a bitmask that just extracts the wanted digits and does operation accordingly
    each pair of bits in the string of length 8
    """
    MASK_SIZE = 16
    BIT_MASK = 0xFFFF
    return(PRECOMPUTED_PARITY [x >> (3 * MASK_SIEZZ)] ^ 
           PRECOMPUTED_PARITY [(x >> (2 * MASK_SIZE)) & BIT_MASK] ^ 
           PRECOMPUTED_PARITY [(x >> MASK_SIZE) & BIT_MASK] ^ 
           PRECOMPUTED_PARITY [x & BIT_MASK])
```



- This algorithm uses time O(n/L)
  - let n be the word size, and let L be the width of the word that we cache the results
  - there are n/L terms, and say each term takes O(1) time, so this algorithm takes up time O(n/L)

### Using the convenient XOR

- take advantage of the fact that CPU's word level XOR processes multiple bits at a time
- keep doing the "folding-like" method where you XOR the first n/2 bits and the last n/2 bits
- so we have the following solution

```python

def parity3(x):
    """
    this method just does bitwise xor for the binary words's first half and second half
    """
   x ^= x >> 32
   x ^= x >> 16
   x ^= x >> 8
   x ^= x >> 4
   x ^= x >> 2
   x ^= x >> 1

   return x & 0x1
```



