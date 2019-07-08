# Using Python as a Calculator.

### Numbers
An *int* is an integer number ( ex: 2,4, 20)
A *float* A Float is a number with a remainder with a decimal (example: 1.1, 2.5, 20.2)

Division (/) will always return a float. To do a *floor division* and get an integer result (discarding any fractional result) you can use the *//* operator. To calculate the remainder you can use the *%*

```
17/3 # Classic division returns a float
5.666667
>>>
>>> 17//3 # Floor division returns the number without the fractional part.
5
>>> 17 % 3 # The % operator returns the remainder of the division In this case 17-15  
2
>>> 5 * 3 + 2 # result * divisor + remainder
17
```

You can also calculate powers by using the `**` operator

```
>>> 5**2 #5 squared
25
>>> 2 ** 9 # 2 to the power of 9
512

```

The `=` sign is used  to signed a variable. Afterwards, no result is displayed before the next interactive prompt:

```
>>> width = 20
>>> height = 5 * 9
>>> width * height
900
```

If the variable is not defined, or not assigned, trying to use it will give you an error.
```
>>> n
File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined
```

Python fully supports different mixed operands.
Example :

```
>>>4 * 3.75 - 1
14.0
```

In interactive mode, the last printed expression is assigned the variable `_`

```
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round (_, 2)
113.06

```
This variable should be treated as read-only by the user. Don’t explicitly assign a value to it — you would create an independent local variable with the same name masking the built-in variable with its magic behavior.

### Strings

Besides numbers, Pyhton can also manipulate strings, which can be expressed in several ways. They can be enclosed in single quotes  `'..'` or doulbe quote `".."` with the same result. `\` can be used to escape quotes

```
>>> 'spam eggs' # Single quotes
'spam eggs'
>>> 'doesn\'t' # Use \ to escape the single quite
"doesn't"
>>> "doesn't" # or just use doulbe quote
"doesn't"
>>> ''"Yes," they said'
'"Yes," they said'
>>> "\"Yes,\" they said."
'"Yes,"they said.'
```

The `print()` function produces a more readable output, by omitting the enclosing quotes and by printing escape and special characters:

```
>>> '"Isn\''t," they said.'
'"Isn\'t," they said.'
>>> print('"Isn\'t," they said.')
"Isn't," they said.
>>>s= 'First line. \n Second Line.' # \n means newline
>>> s  # without print(), \n is included in the output
'First line.\nSecond line.'
>>> pint(s) # with pint(), \n produces a new line

```

If you don't want characters to be prefaced by `\` interpreted as a special character, you can use raw strings by adding a `r` before the first quote:

```
>>> print('C:\some\name') # here \n means new line!
C:\some
ame
>>> print(r'C:\some\name') # note the r before the quote
C:\some\name
```

Strings literals can span multiple lines. One way is using triple quote `"""..."""` or `'''...'''`.

Example:
```
>>> print("""\
... Usage:      [OPTIONS]
...     -h              Display this usage message
...     -H hostname     Hostname to connect to
... """)

Usage:  [OPTIONS]
        -h              Display this usage message
        -H hostname     Hostname to connect to

```

Strings can be concatenated (glued together) with the `+` operator and replaced with the (`*`):

```
>>> # 3 times 'un', followed by 'ium'
>>> 3* 'un' + 'ium'
'unununium'
```

Two or more `string literals` (Ex: The ones enclosed between quotes) next to each other are automatically concatenated.

```
>>> 'Py' 'thon''sucks'
Pythonsucks
```

This feature is particularly useful when you want to break long strings:

```
>>> text = ('Put several strings within parentheses'
...            'to have them joined together.')
>>> text
'Put several strings within parentheses to have them join together'
```

This will only work with literals though, not variables or expressions

```
>>> prefix = 'Py'
>>> prefix 'thon'  # can't concatenate a variable and a string literal
  File "<stdin>", line 1
    prefix 'thon'
                ^
SyntaxError: invalid syntax
>>> ('un' * 3) 'ium'
  File "<stdin>", line 1
    ('un' * 3) 'ium'
                   ^
SyntaxError: invalid syntax
```

If you want to concatenate variables or a variable and a literal, use the `+`

```
prefix = 'Py'
prefix + 'thon'
'Python'

```

Strings can be indexed (subscripted) with the first character having index 0. There is no separate character type; a character is simple a string of size one:

```
>>> word = 'Python'
>>> word[0] # char in position 0
'P'
>>> word[5] # char in position 5
'n'
```

Indexes may also have negative numbers, to start counting from the right:

```
>>> word[-1] # Last character
'n'
>>> word [-2] # Second to last char
'o'
>>> word[-6]
'p'
```

Note that since -0 is the same as 0, negative indexes start from -1.
```
>>> word[-0]
'P'
>>> word[0]
'P'

```

In addition to indexing *slicing* is also supported. While indexing is used to obtain individual characters, slicing allows you to obtain substring:

```
>>> word[0:2] # Chars from position 0(included) to 2(excluded)
'Py'
>>> word[2:5] # charcaters from position 2 (included) to 5 (excluded)
'tho'
>>> word[-6:-1]
'Pytho'
```

Note how the start is always included, and the end always excluded. This makes sure that `s[:i] + s[i:]` is always equal to `s`:

```
>>> word[:2] + word[2:]
'Python'
>>> word[:4] + word[4:]
'Python'
```

Slice indexes have useful defaults; an omitted first index defaults to zero, an omitted second index defaults to the size of the string being sliced.


```
>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'
```

Attempt to index something that is too large will result in an error

```
word[50] # the word only has 6 characters
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

However if you use a range for slicing it will work:
```
>>> word[4:50]
'on'
>>> word[50:]
''
```

Python strings cannot be changed as they are immutable. Therefore assigning to  an indexed position in the string results in an error.

```
>> word[0] = 'J'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

If you need a different string, you should create a new one:
```
>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
Pypy
```

There is a built in function `len()` which returns the lenght of a string:

```
>>> s='supercalifragilisticexpialidocious'
>>> len(s)
34
```

### Lists

Python knows a number of compound data types, used to group together other values. The most versatile is the list, which can be written as a list of comma-separated values (items) between square brackets. Lists might contain items of different types, but usually the items all have the same type.

```
>>> squares = [1, 4, 0, 16, 25]
>>> squares
[1, 4, 0, 16, 25]
```

Like strings, lists can also be indexed and sliced :
```
>>> squares[0]  # indexing returns the item
1
>>> squares[-1]
25
>>> squares[-3:]  # slicing returns a new list
[9, 16, 25]
```

All slicing operations return a new list containing the requested elements. This means that  the following slice returns a new (shallow) copy of the list

```
>>> squares[:]
[1, 4, 0, 16, 25]
```

Lists also support operations like concatenation- Meaning you can add to the list:

```
>>> squares + [20,30,40,50]
[1, 4, 0, 16, 25, 20, 30, 40, 50]
```

Unlike strings, which are immutable, lists are a mutable type, i.e. it is possible to change their content:

```
>>> cubes = [1,8,27,65,125]
>>> cubes
[1, 8, 27, 65, 125]
>>> cubes[3] = 64
>>> cubes
[1, 8, 27, 64, 125]
```

You can also add new items at the end of hte list by using the `append()` method.

```
>>> cubes.append(216)
>>> cubes.append(7**3)
>>> cubes
[1, 8, 27, 64, 125, 216, 343]
```

Assignment to slices is also possible, and this can even change the size of the list or clear it entirely.

```
>>> letts =['a','b','c','d','e','f','g']
>>> letts
['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> #replace some values
... letts[2:5] = ['C','D','E']
>>> letts
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now lets remove them
... letts[2:5]=[]
>>> letts
['a', 'b', 'f', 'g']
>>> #You can clear the entire list by replacing all the elements with something empty
... letts[:]=[]
>>> letts
[]
```

The built in function `len()` also applies to lists - counts the length of list:
```
>>> letts =['a','b','c','d','e','f','g']
>>> len(letts)
7
```

It is possible to nest lists (create lists containing other lists), for example:


```
>>> a= ['a','b','c']
>>> n=[1,2,3]
>>> x=[a,n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[1]
[1, 2, 3]
>>> x[0][1]
'b'
>>> x[0:2]
[['a', 'b', 'c'], [1, 2, 3]]
```

 ### The first steps toward programming
 We can create something that is a bit more complicated

 ```
 >>> a,b = 0, 1
 >>> while a < 10:
 ...     print(a)
 ...     a,b = b, a+b
 ...
 0
 1
 1
 2
 3
 5
 8

 ```
 Note that print(a) is indented - you must indent!
 The first line contains a multiple assignment: the variables a and b simultaneously get the new values 0 and 1. On the last line this is used again, demonstrating that the expressions on the right-hand side are all evaluated first before any of the assignments take place. The right-hand side expressions are evaluated from the left to the right.

The while loop executes as long as the condition (here: a < 10) remains true. In Python, like in C, any non-zero integer value is true; zero is false. The condition may also be a string or list value, in fact any sequence; anything with a non-zero length is true, empty sequences are false. The test used in the example is a simple comparison. The standard comparison operators are written the same as in C: < (less than), > (greater than), == (equal to), <= (less than or equal to), >= (greater than or equal to) and != (not equal to).

The body of the loop is indented: indentation is Python’s way of grouping statements. At the interactive prompt, you have to type a tab or space(s) for each indented line. In practice you will prepare more complicated input for Python with a text editor; all decent text editors have an auto-indent facility. When a compound statement is entered interactively, it must be followed by a blank line to indicate completion (since the parser cannot guess when you have typed the last line). Note that each line within a basic block must be indented by the same amount.

The print() function writes the value of the argument(s) it is given. It differs from just writing the expression you want to write (as we did earlier in the calculator examples) in the way it handles multiple arguments, floating point quantities, and strings. Strings are printed without quotes, and a space is inserted between items, so you can format things nicely, like this

```
>>> i=256*256
>>> print('The vaule of i is', i)
The vaule of i is 65536

```
The keyword argument end can be used to avoid the newline after the output, or end the output with a different string:

```
>>> a,b= 0,1
>>> while a < 1000:
...     print (a, end=',')
...     a,b = b, a+b
...
0,1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,
```
