# Flow Control

### if statements
Perhaps the most well-known statement type is the if statement.

Example:
```
>>> x = int(input("Please enter an integer: "))
Please enter an integer: 100
>>> if x < 0:
      x = 0 # notice the indent
      print ('Negative changed to zero')
  elif x == 0:
      print('Zero')
  elif x == 1:
      print('Single')
  else:
      print('More')
```

There can be zero or more `elif` parts and the `else` part is also optional. The keyword elif stands for else if and is useful to avoid excessive indentation. An if .... elfif ... elif sequence for the `switch` or `case` statements found in other languages.

Notice how we had to indent for each statement.

### for statements
The `for` statement in Pyhton differs from C. Rather than always iteraing over an arithmetic progression of numbers, or giving the user the ability to define both the iteration step and halting condition, Python's `for` statement iterates over the items of any sequence ( a list or a string), in the order that they appear in the sequence. For example:

```
>>> # Measure some strings:
... words = ["cat", "window", "defenestrate"]
>>> for w in words:
...     print(w, len(w))
...
cat 3
window 6
defenestrate 12

```



### The range() function

If you do need to iterate over a sequence of numbers, the built-in function `range()` comes in handy. It generates arithmetic progressions:

The `range()` function returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and ends at a specified number.

Syntax:

`range(start, stop, step)`

Parameter Values

```
Parameter	Description
start	Optional. An integer number specifying at which position to start. Default is 0
stop	Optional. An integer number specifying at which position to end.
step	Optional. An integer number specifying the incrementation. Default is 1

```

```
>>> for i in range(10):
...     print(i)
...
0
1
2
3
4
5
6
7
8
9

```

The given end point is never part of the generated sequence; range(10) generates 10 values, the legal indexes for items of a sequence of length 10. It is possible to let the range start at another number, or to specify a different increment (even negative; sometimes this is called the 'step'):


```
>>> for i in range(5,10):
...     print(i)
...
5
6
7
8
9
```

```
>>> for i in range(0,10,3):
...     print(i)
...
0
3
6
9

```
So in the last example the range is from 0-10, with increments of 3. Thus 0, 3, 6, 9


To iterate over the indexes of a sequence, you can combine `range()` and `len()` :


```
>>> a = [ "Mary", "Had", "a", "little", "lamb"]
>>> for i in range(len(a)):
...     print(i,a[i])
...
0 Mary
1 Had
2 a
3 little
4 lamb


```

In most cases it is convenient to just use the `enumerate()` function/

A strange thing happens if you just print a range:

```
>>> print(range(10))
range(0, 10)

```

In many ways the object returned by `range()` behaves as if it is a list, but in fact isn't. It is an object which returns the successive items of the desired sequence when you iterate over it, but it doesn't really make the list thus saving space.

We csay such an object is repeatable, that is, suuitable as a target for funcitons and constructs that expect something from which they can obtain succesive items until the supply is exhausted. We have see that the `for` statement is an iterator. The function `list()` is another; as it creates a list from iterables:

```
>>> list(range(5))
[0, 1, 2, 3, 4]
```

### break and continue statements, and else clasuses on loops

The `break` statement, like in C, breaks out the innermost enclosing `for` or `while` loop.


Loop statements may have an `else` clause; it is executed when the loop terminates through exhaustion of the list (with `for`) or when the condition becomes false (with while), but not when the loop is terminated by a `break` statement.  
Example:

```
>>> for n in range(2,10):
...     for x in range(2,n):
...             if n % x == 0:
...                     print(n, 'equals', x, '*', n//x)
...                     break
...     else:
...             # loop fell through wihtout finding a factor
...             print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
>>>
```
When used with a loop, the else clause has more in common with the else clause of a try statement than it does that of if statements: a try statement’s else clause runs when no exception occurs, and a loop’s else clause runs when no break occurs.

The `continue` statement, also borrowed from C, continues with the next iteration of the loop:

```
>>> for num in range(2,10):
...     if num % 2 == 0:
...             print("Found an even number",num)
...             continue
...     print("Found a number",num)
...
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9

```

### pass statements


The `pass` statement does nothing. It can be used when a statement is require syntactially but the program requires no action:

```
while True:
  pass # Busy-wait for keyboard interrupt (Ctrl+C)

```
This is more commnly used for breaking minimal classes:

```
class MyEmptyClass:
  pass
```

Another place `pass` can be used is as a place-holder for a function or condiational body when you are working on a new code, allowing you to keep thinking at a more abstract level. The pass is silently ignored:

```
def initlog(*args):
  pass # REMEMBER TO IMPLEMENT THIS
```

### defining functions


The keyword `def` introduces a function definition. It must be followed by the function name and the parenthesized list of formal parameters. The statements that form the body of the function start at the next line, and must be indented.

The first statement of the function body can optionally be a string literal; this string literal is the function's documentation string, or docstring. There are tools which use docstrings to automatically produce online or printed documentation, or to let the user interactively browse through code; it's good practice to include docstring in code hat your write, so you make a habit of it.

The execution of a function introduces a new symbol table used for the local variables of the function. More precisely, all variables assignments in a function store the value in the local symbol table whereas variable references first look in the local symbol table, then the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names. Thus, global variable cannot be directly assigned a value within a function (unless named in a global statement), although they may be referenced.

The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called; thus, arguments are passed using call by value (where the value is always an object reference, not the value of the object)  When a function calls another function, a new local symbol table is created for that call.

A function definition introduces the function name in the current symbol table. The value of the function name has a type that is recognized by the interpreter as a user-defined function. This value can be assigned to another name which can then also be used as a function. This serves as a general remaining mechanism:


```
>>> def fib(n):
...     """print a fib up to n."""
...     a, b = 0, 1
...     while a <n:
...             print(a, end=' ')
...             a,b = b, a+b
...     print()
...  # Notice this empty line- it defines end of definition
>>> fib
<function fib at 0x7fec498591e0>
>>> fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

```

So now let's use the definition to in another variable

Example:
```
>>> fib
<function fib at 0x7fec498591e0>
f= fib
f(100)
0 1 1 2 3 5 8 13 21 34 55 89
```

Some may think that it is not a function becasue it returns no value, but it does. If you use the print(), it will print out `None`

Example:


```
>>> fib(0)

>>> print(fib(0))

None

```

It is simple to write a function that returns a list of the numbers of the Fibonacci serries, isntead of printing it.

```
>>> def fib2(n):
...     result = []
...     a, b = 0, 1
...     while a < n:
...             result.append(a)
...             a,b = b, a+b
...     return result
...
>>> f100= fib2(100)
>>> f100
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]

```


### More defining functions


The most useful form is the is the specify a default value for one or more arguments. This creates a function that can be called with fewer arguments than it is defined to allow. For example:

```
def ask_ok (prompt, retries=4, reminder='Please try again!')
  while True:
      ok= input(prompt)
      if ok in ('y', 'ye', 'yes'):
        return True
      if ok in ('n', 'no', 'nop', 'nope'):
        return False
      retries = retries - 1
      if retires < 0:
        raise Valueerror('invalid user response')
      print(remainder)
```
This function can be called in many ways :

- giving only the mandatory arguments: `ask_ok('Do you realy want to quit?')`
- gviing only one of the optional arguments: `ask_ok('OK to overwirte the file?',2)`
- or even giving all arguments: `ask_ok('Ok to overwrite the file?',2,'Come on, only yes or no!')`

The last example introduced the `in` keyword. This tests wheater or not a sequence contains a certain value.

The default values are evaluated at the point of function definition in the defining scope so that means :

```
i = 5
def f(arg=i):
  print(arg)

i=6
f()
```
will print 5  even though i is defined as 6 at the bottom.

The default value is evaluated only once. This makes a difference when the defualt is a object usch as a list or diction or instances of msot classes- Meaning it cna change.

Example:

```
def f(a, L=[]):
    L.append(a)
    return L
>>> print(f(1))
[1]
>>> print(f(2))
[1, 2]
>>> print(f(3))
[1, 2, 3]
>>>

```

If you don't want the default to be shared between subseqent calls, you can write hte funciton like this isntead:

```

>>> def f(a, L=None):
...     if L is None:
...             L = []
...     L.append(a)
...     return L
...
>>> print(f(1))
[1]
>>> print(f(100))
[100]
>>> print(f(3))
[3]

```


### Keyword Arguments


Functions can also be called using keyword aguments of the form `keywordarg=vaule`

Example:

```
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
  print("-- This parrot wouldn't", action, end= '')
  print("if you put", voltage, "volts through it.")
  print("--- Lovely plumage, the", type)
  print(" -- It's", state, "!")

```


This will accept one requirement argument `voltage` and three optional arguments (state, action and type). This function can be called in any of the following ways:

```
>>> parrot(1000)
-- This parrot wouldn't voom if you put 1000 volts through it.
-- Lovely plumage, the Norweign Blue
-- It's a stiff !

>>> parrot(voltage=1000)
-- This parrot wouldn't voom if you put 1000 volts through it.
-- Lovely plumage, the Norweign Blue
-- It's a stiff !

>>> parrot(voltage=1000000, action='VOOOM')
-- This parrot wouldn't VOOOM if you put 1000000 volts through it.
-- Lovely plumage, the Norweign Blue
-- It's a stiff !

>>> parrot('a million', 'bereft of life', 'jump')
-- This parrot wouldn't jump if you put a million volts through it.
-- Lovely plumage, the Norweign Blue
-- It's bereft of life !

>>> parrot('a thousand', state='pushing up the daisises')
-- This parrot wouldn't voom if you put a thousand volts through it.
-- Lovely plumage, the Norweign Blue
-- It's pushing up the daisises !


```


### Intermezzo: Coding Style
