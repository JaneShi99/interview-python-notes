### String problems in python

- the following code checks whether a string s is palindromic 

```python
def is_palindromic(s):
    # s[~i] for i in [0,len(s)-1] is s[-(i + 1)]
    return all (s[i] == s[~i] for i in range(len(s) //2))
```



### String libraries

- key operators:

  - s[3], len(s), s + s, s[2:4] , where other list variants apply as well

  - s in t

  - s.strip()

  - 

    - ```python
      string.strip([chars])
      ```

  - strip() returns a copy of the string that strips the leading and trailing characters with the following rule:

    - when the combination of characters in the chars argument no longer matches the character of string from the left, it stops removing leading characters in the string
    - when the combination of characters in the chars argument no longer match the characters of strings from the right it stops removing trailing characters in the string

  - s.startwith(prefix), and s.endwith(suffix)

  - split at character

  - foratting for printing

  - S.toLower()

  - join substrings

  - note that strings are immutable, so the operations that are applied to the strings returns the string as a copy

  - 

### 6.1 Converting between strings and integer

```python
def int_to_string(x):
    is_negative = False
    if x < x:
        x, is_negative = -x, True

    s = []
    while True:
        s.append(chr(ord('0') + x % 10)) #converting the x by adding its number to 0's char representation
        x //= 10
        if x == 0:
            break
    return ('-' if is_negative else '') + ''.join(reversed(s))

def string_to_int(s):
    return functools.reduce(
            lambda running_sum, c: running_sum * 10 + string.digits.index(c), 
            s[s[0] == '-':], 0 * (-1 if s[0] == '-' else 1)
```

- notes:
- https://www.w3schools.com/python/python_lambda.asp
- https://docs.python.org/2/library/functools.html