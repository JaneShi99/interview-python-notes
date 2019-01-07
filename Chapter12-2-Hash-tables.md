### Chapter 12 Hash tables for python

- Inserts, deletes, and looksup run O(1) time on average. (low amortized cost although rehashing is expensive)

- Idea is to store keys in an array

- We want a good hash function that spread the keys out in order to minimize the collision 

- Hash functions have one requirement: same keys have same hash codes, make them as non-invertible as possible. i.e. try to make it injective

- Try to make the hash function efficient to compute



  ### Example hash function for strings

   ```python
  def string_hash(s,modulus):
      MULT = 997
      return functools.reduce(lambda v, c: (v * MULT + ord (c)) % modulus, s, 0)
   ```

- hash function should examine all the chars in string

- give a large range of values, and should not let one character affect the result. i.e. if our hash function is to cast chars to integer, and to multiply them, having a single 0 would result in all 0. So that's generally not a good hash function

- we want a rolling hash function, i.e. if the first char is deleted and another char is added to the end of the string, we can compute the new hashcode in O(1) time

- functools.reduce example:

  - `reduce(lambda x, y: x+y, [1, 2, 3, 4,5])` calculates `((((1+2)+3)+4)+5)`

  - the accumulator start at 0, v is the accumulator variable. 

  - reduce takes in three params, first argument is function, second argument is a iterator, the third thing is accumulator. Note that a string is an iterable.

  - `lambda v, c: (v * MULT + ord (c)) % modulus` is the iterable, s is the string(iterable), and 0 is the initial accumulator value

  - equivalent to the following function

  - ```python
    def helper(acc, curr):
         return (acc * MULT + ord(c)) % modulus
    acc = 0
    for val in s:
        helper(acc, val)
    ```

    - functions reduce implementation is similar to:

  ```python
  def reduce(function, iterable, initializer=None):
      it = iter(iterable)
      if initializer is None:
          value = next(it)
      else:
          value = initializer
      for element in it:
          value = function(value, element)
      return value
  ```


- more notes about functools.reduce are written in the notes page

### Example applicaion of hash tables

- solving anagrams: given a list of words, and then your task is to group the words that are the anagrams of one another

- ```python
  def find_anagrams(dictionary):
      sorted_string_to_anagrams = collections.defaultdict(list)
      for s in dictionary:
          sorted_string_to_anagrams[''.join(sorted(s))].append(s)
  	return[
              group for group in sorted_string_to_anagrams.values() if len(group) >=2
          ]
  
  ```

### Designing a hash table class

- reference for python hash function
- https://www.programiz.com/python-programming/methods/built-in/hash
- frozenset is an unmutable set

### Hash table libraries

- There are multiple hash table-based data structures common in python: set, dict, collections.defaultdict, and collections.Counter
- The difference is that set stores only keys, while other three store key-value pairs.
- collections.counter is used for counting the number of occurrences of keys.
- example for collections.counter 

```python
c = collections.Counter(a=3,b=1)
d = collections.Counter(a=1,b=2)
#add two counters together: 
#c[x] + d[x], collections.Counter({'a':4,'b':3})
c + d
#subtract two counters together
#collections.Counter({'a' = 2})
c - d
#intersection: min(c[x],d[x]), 
#collections.Counter({'a':1,'b':1})
c & d
#union: max(c[x],d[x]),
#collections.Counter({'a':3,'b':2})
c | d
```

- Operation for set:
  - `s.add(42), s.remove(42),s.discard(123), x in s, s <=t (i.e. subset), and s - t (elements in s not in t)`
  - to iterate over kvps, use items(), to iterate over values, use values()



### Exercise 12.2

- write a program that takes text for an anonymous letter and text for a magazine, determine if it is possible to write the anonymous letter using the magazine. 
- the anonymous lettter can be written using the magazine, if for each charater in the anon. letter the number of times it appears in the anon. letter is no more than the number of times of that letter appearing in magazine.
- idea: count the number of distinct characters appearing in the letter
- idea: iterate through letter once, and store character counts in a hash table (key: chars and val: number of times it appear)
- then we 'undo' the has function while passing through the magazine: i.e. reduce the count of that letter by 1 if that letter appear in the hash table. Now, as soon as the hash table is empty we know we're done

```python
def is_letter_constructible_from_magazine(letter_text, magazine_text):
    #this below code automatically sets up the counter hash table
    # ready for the letters
    char_freq_for_letter = collections.Counter(letter_text)
    #now pass thru magazine
    for c in magazine_text:
        if c in char_freq_for_letter:
            char_freq_for_letter[c] -=1
            if char_freq_for_letter[c] == 0:
                del char_freq_for_letter[c]
                if not char_freq_for_letter:
                    return True
    return not char_fre_for_letter
```

- worst cast runtime is O(m+n)
- hash table has 256 entry if characters are coded in ASCII