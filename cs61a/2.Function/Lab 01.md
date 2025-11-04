[Lab 1: Functions | CS 61A Fall 2025](https://cs61a.org/lab/lab01/#required-questions)

# Q1: Return and Print
```cmd
return-and-print > Suite 1 > Case 1
(cases remaining: 1)

What would Python display? If you get stuck, try it out in the Python
interpreter!

>>> def welcome():
...     print('Go')
...     return 'hello'
>>> def cal():
...     print('Bears')
...     return 'world'
>>> welcome()
(line 1)? Go
(line 2)?
-- Not quite. Try again! --

(line 1)? Go
(line 2)? 'hello'
-- OK! --

>>> print(welcome(), cal())
(line 1)? Go
(line 2)? Bears
(line 3)? hello world
-- OK! --
```

# Q2: Debugging Quiz
```cmd
---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 1
(cases remaining: 7)

Q: In the following traceback, what is the most recent function call?
Traceback (most recent call last):
    File "temp.py", line 10, in <module>
      f("hi")
    File "temp.py", line 2, in f
      return g(x + x, x)
    File "temp.py", line 5, in g
      return h(x + y * 5)
    File "temp.py", line 8, in h
      return x + 0
  TypeError: must be str, not int
Choose the number of the correct choice:
0) g(x + x, x)
1) f("hi")
2) h(x + y * 5)
? 2
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 2
(cases remaining: 6)

Q: In the following traceback, what is the cause of this error?
Traceback (most recent call last):
    File "temp.py", line 10, in <module>
      f("hi")
    File "temp.py", line 2, in f
      return g(x + x, x)
    File "temp.py", line 5, in g
      return h(x + y * 5)
    File "temp.py", line 8, in h
      return x + 0
  TypeError: must be str, not int
Choose the number of the correct choice:
0) the code looped infinitely
1) the code attempted to add a string to an integer
2) there was a missing return statement
? 1
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 3
(cases remaining: 5)

Q: How do you write a doctest asserting that square(2) == 4?
Choose the number of the correct choice:
0) def square(x):
       '''
       input: 2
       output: 4
       '''
       return x * x
1) def square(x):
       '''
       doctest: (2, 4)
       '''
       return x * x
2) def square(x):
       '''
       >>> square(2)
       4
       '''
       return x * x
3) def square(x):
       '''
       square(2)
       4
       '''
       return x * x
? 2
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 4
(cases remaining: 4)

Q: When should you use print statements?
Choose the number of the correct choice:
0) For permanant debugging so you can have long term confidence in your code
1) To investigate the values of variables at certain points in your code
2) To ensure that certain conditions are true at certain points in your code
? 1
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 5
(cases remaining: 3)

Q: How do you prevent the ok autograder from interpreting print statements as output?
Choose the number of the correct choice:
0) You don't need to do anything, ok only looks at returned values, not printed values
1) Print with 'DEBUG:' at the front of the outputted line
2) Print with # at the front of the outputted line
? 1
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 6
(cases remaining: 2)

Q: What is the best way to open an interactive terminal to investigate a failing test for question sum_digits in assignment lab01?
Choose the number of the correct choice:
0) python3 ok -q sum_digits -i
1) python3 -i lab01.py
2) python3 ok -q sum_digits --trace
3) python3 ok -q sum_digits
? 0
-- OK! --

---------------------------------------------------------------------
debugging-quiz > Suite 1 > Case 7
(cases remaining: 1)

Q: Which of the following is NOT true?
Choose the number of the correct choice:
0) It is generally bad practice to release code with debugging print statements left in
1) Testing is very important to ensure robust code
2) Code that returns a wrong answer instead of crashing is generally better as it at least works fine
3) Debugging is not a substitute for testing
4) It is generally good practice to release code with assertion statements left in
? 2
-- OK! --
```

# Q3: Pick a Digit
```python
def digit(n, k):

    """Return the k-th digit from the right of n for positive integers n and k.
    
    >>> digit(3579, 2)
    5
    >>> digit(3579, 0)
    9
    >>> digit(3579, 10)
    0
    """

    return (n % pow(10, k + 1) // pow(10, k))
```


# Q4: Middle Number
```python
def middle(a, b, c):
    """Return the number among a, b, and c that is not the smallest or largest.
    Assume a, b, and c are all different numbers.

    >>> middle(3, 5, 4)
    4
    >>> middle(30, 5, 4)
    5
    >>> middle(3, 5, 40)
    5
    >>> middle(3, 5, 40)
    5
    >>> middle(30, 5, 40)
    30
    """
    return a + b + c - max(a, b, c) - min(a, b, c)
```

# Q6: WWPD: What If?
```cmd
---------------------------------------------------------------------
What If? > Suite 1 > Case 1
(cases remaining: 2)

What would Python display? If you get stuck, try it out in the Python
interpreter!

>>> def ab(c, d):
...     if c > 5:
...         print(c)
...     elif c > 7:
...         print(d)
...     print('foo')
>>> ab(10, 20)
(line 1)? 10
(line 2)? foo
-- OK! --

---------------------------------------------------------------------
What If? > Suite 1 > Case 2
(cases remaining: 1)

What would Python display? If you get stuck, try it out in the Python
interpreter!

>>> def bake(cake, make):
...    if cake == 0:
...        cake = cake + 1
...        print(cake)
...    if cake == 1:
...        print(make)
...    else:
...        return cake
...    return make
>>> bake(0, 29)
(line 1)? 1
(line 2)? 29
(line 3)? 29
-- OK! --

>>> bake(1, "mashed potatoes")
(line 1)? mashed potatoes
(line 2)? 'mashed potatoes'
-- OK! --

---------------------------------------------------------------------
```

# Q7: Falling Factorial  Q7
```python
def falling(n, k):
    """Compute the falling factorial of n to depth k.

    >>> falling(6, 3)  # 6 * 5 * 4
    120
    >>> falling(4, 3)  # 4 * 3 * 2
    24
    >>> falling(4, 1)  # 4
    4
    >>> falling(4, 0)
    1
    """
    "*** YOUR CODE HERE ***"
    r = 1
    for i in range(k):
        r *= n - i
    return r
```

# Q8: Divisible By k
```python
def divisible_by_k(n, k):
    """
    >>> a = divisible_by_k(10, 2)  # 2, 4, 6, 8, and 10 are divisible by 2
    2
    4
    6
    8
    10
    >>> a
    5
    >>> b = divisible_by_k(3, 1)  # 1, 2, and 3 are divisible by 1
    1
    2
    3
    >>> b
    3
    >>> c = divisible_by_k(6, 7)  # There are no integers up to 6 that are divisible by 7
    >>> c
    0
    """
    "*** YOUR CODE HERE ***"
    counts = 0
    for i in range(1, n + 1):
        if i % k == 0:
            print(i)
            counts += 1
    return counts
```

# Q9: Sum Digits  Q9
```python
def sum_digits(y):
    """Sum all the digits of y.

    >>> sum_digits(10) # 1 + 0 = 1
    1
    >>> sum_digits(4224) # 4 + 2 + 2 + 4 = 12
    12
    >>> sum_digits(1234567890)
    45
    >>> a = sum_digits(123) # make sure that you are using return rather than print
    >>> a
    6
    """
    "*** YOUR CODE HERE ***"
    total = 0
    while y > 0:
        total += y % 10
        y //= 10
    return total
```

# Q10: Double Eights  Q10
```python
def double_eights(n):
    """Return true if n has two eights in a row.
    >>> double_eights(8)
    False
    >>> double_eights(88)
    True
    >>> double_eights(2882)
    True
    >>> double_eights(880088)
    True
    >>> double_eights(12345)
    False
    >>> double_eights(80808080)
    False
    """
    "*** YOUR CODE HERE ***"
    prev = -1
    while n > 0:
        curr = n % 10
        if curr == 8 and prev == 8:
            return True
        prev = curr
        n //= 10
    return False
```