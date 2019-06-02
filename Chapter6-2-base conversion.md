### Chapter 6-2: Base conversion



- Write a program where:

  - input is a string, an integer $b_1$, an integer $b_2$, where the string is orignally represented in $b_1$ we want to change it so that it is represented in $b_2$
  - Assume that $ 2\leq b_1, b_2, \leq 16$ , $a$ for 10, $b$ for 11, and that $f$ for 15

- Idea: can convert to base 10 then convert to the other value by division.

- solution is implemented using recursion

- ```
  string.hexdigits
  ```

  The string `'0123456789abcdefABCDEF'`.

- `string.ascii_letters`

  The concatenation of the [`ascii_lowercase`](https://docs.python.org/3.1/library/string.html#string.ascii_lowercase) and [`ascii_uppercase`](https://docs.python.org/3.1/library/string.html#string.ascii_uppercase) constants described below. This value is not locale-dependent.

- `string.ascii_lowercase`

  The lowercase letters `'abcdefghijklmnopqrstuvwxyz'`. This value is not locale-dependent and will not change.

- `string.``ascii_uppercase`

  The uppercase letters `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`. This value is not locale-dependent and will not change.

- `string.digits`

  The string `'0123456789'`.

- `string.hexdigits`

  The string `'0123456789abcdefABCDEF'`.

- `string.octdigits`

  The string `'01234567'`.

- `string.punctuation`

  String of ASCII characters which are considered punctuation characters in the `C` locale.

- `string.printable`

  String of ASCII characters which are considered printable. This is a combination of [`digits`](https://docs.python.org/3.1/library/string.html#string.digits), [`ascii_letters`](https://docs.python.org/3.1/library/string.html#string.ascii_letters), [`punctuation`](https://docs.python.org/3.1/library/string.html#string.punctuation), and [`whitespace`](https://docs.python.org/3.1/library/string.html#string.whitespace).

- `string.whitespace`

  A string containing all ASCII characters that are considered whitespace. This includes the characters space, tab, linefeed, return, formfeed, and vertical tab.

comes from https://docs.python.org/3.1/library/string.html



These basically gives you a string with desired needed letters

```python
def convert_base(num_as_string, b1,b2):
  def construct_from_base(num_as_int,base):
  	if num_as_int == 0:
      return '0'
    else:
      costruct_from_base(num_as_int // base, base) + string.hexdigit[num_as_int % base].upper()
  
  is_negative = num_as_string[0]== '-'
  num_as_int = functools.reduce(lambda x, c: x*b1+string.hexdigits.index(c.lower()), num_as_string[is_negative:], 0)
  
  return ('-' if is_negative else '') + ('0' if num_as_int==0 else construct_from_base(num_as_int, b2))

```

