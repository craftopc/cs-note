# [Iteration Example](https://www.youtube.com/watch?v=pveIuZT0GJE&list=PL6BsET-8jgYXvcnnEX7x2_USaYug9xZFv&index=1)
> Q: Is this alternative definition of fib the same or different from the original fib?

origin:
```python
def fib(n):
    """Compute the nth Fibonacci number, for N >= 1."""
    pred, curr = 0, 1
    k = 1
    while k < n:
        pred, curr = curr, pred + curr
        k = k + 1
    return curr
```

alternative definition:
```python
def fib_(n):
    """Compute the nth Fibonacci number, for N >= 1."""
    pred, curr = 1, 0
    k = 0
    while k < n:
        pred, curr = curr, pred + curr
        k = k + 1
    return curr
```

Fibonacci sequence:
```text
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...]
```

In first section, calc number range is $[1, n)$ n - 1 times, first item is number 1.
In second section, calc number range is $[0, n)$ n times, first item is number 0, the pred number is defined for get a correct returns only at first run.

Better method is `fib_` function.

# [Control](https://www.youtube.com/watch?v=FwYgFFL52H4&list=PL6BsET-8jgYXvcnnEX7x2_USaYug9xZFv&index=2)
Special example:

control statements
```python
def real_sqrt(x):
	"""Return the real part of the sqare root of x."""
	if x >= 0:
		return sqrt(x)
	else:
		return 0
```

Use function to rewrite it
```python
def if_(c, t, f):
	if c:
		return t
	else:
		return f
		
def real_sqrt(x):
	"""Return the real part of the sqare root of x."""
	return if_(x >= 0, sqrt(x), 0)
```

First section will exec correctly
Second section can report errors, like this:
```python
PS E:\Temp> python -i .\ex.py
>>> real_sqrt(2)
1.4142135623730951
>>> real_sqrt(-1)
Traceback (most recent call last):
  File "<python-input-1>", line 1, in <module>
    real_sqrt(-1)
    ~~~~~~~~~^^^^
  File "E:\Temp\ex.py", line 11, in real_sqrt
    return if_(x >= 0, sqrt(x), 0)
                       ~~~~^^^
ValueError: expected a nonnegative input, got -1.0
>>>
```

Because call expression will evaluate all arguments, such as `sqrt(x)`.

# [Control Expressions](https://www.youtube.com/watch?v=DDcYvnqUCNA&list=PL6BsET-8jgYXvcnnEX7x2_USaYug9xZFv&index=3)
Short-circuit
```python
def has_big_sqrt(x):
	return x > 0 and sqrt(x) > 10
	
def reasonable(n):
	return n == 0 or 1/n != 0
```

for `and` , while left expression is false, program can't exec right expression
for `or`, while left expression is true, program can't exec right expression

# [Higher-Order Functions](https://www.youtube.com/watch?v=UlXvz-34Me0&list=PL6BsET-8jgYXvcnnEX7x2_USaYug9xZFv&index=4)
> A function that takes a function as an argument value or returns a function as a return value

## Use constant to pass special expression
```python
"""Gerneralization."""

from math import pi, sqrt

def area(r, shape_constant):
	assert r > 0
	return r * r * shape_constant
	
def area_square(r):
	return area(r, 1)
	
def area_circle(r):
	return area(r, pi)

def area_hexagon(r):
	return area(r, 3 * sqrt(3) / 2)
```

## Pass function as arguments && Functions as general methods
```python
"""Gerneralization."""

def identity(k):
	return k
	
def cube(k):
	return pow(k, 3)
	
def pi_term(K):
	return 9 / mul(4 * k - 3, 4 * k -1)

def summation(n, term):
	"""Sum the first N terms of a sequence.
	
	>>> summation(5, cube)
	225
	"""
	total, k = 0, 1
	while k <= n:
		total, k = total + term(k), k + 1
	return total
	
def sum_naturals(n):
	"""Sum the first N natural numbers.
	
	>>> sum_naturals(5)
	15
	"""
	return summation(n, identity)

def sum_cubes(n):
	"""Sum the first N cubes of natural numbers.
	
	>>> sum_cubes(5)
	225
	"""
	return summation(n, cube)
```

Maybe we should make a test to improve our understand
[1.6 Higher-Order Functions#functions-as-general-methods](https://www.composingprograms.com/pages/16-higher-order-functions.html#functions-as-general-methods)
Achieve an iterative improvement algorithm, it begins with a 'guess' of a solution, to `update` function to improve that guess, and applies a `close` function to check if 'guess' is close enough the correct value.
```python
def improve(update, close, guess=1):
	while not close(guess):
		guess = update(guess)
	return guess
```
This is general expression we now use it to evaluate "phi"

We need to design two main function. These used the well-known properties of the golden ratio.
update
```python
def golden_update(guess):
	return 1 / guess + 1
```
close
```python
def square_close_to_successor(guess):
	return approx_eq(guess * guess, guess + 1)

def approx_eq(x, y, tolerance = 1e-15):
	return abs(x - y) < tolerance
```

exec it
```python
>>> improve(golden_update, square_close_to_successor)
1.6180339887498951
```
As always, we can write a test for it
```python
from math import sqrt
phi = 1/2 + sqrt(5) / 2
def improve_test():
	approx_phi = improve(golden_update, square_close_to_successor)
	assert approx_eq(phi, approx_phi)
```

## Nested Definitions && Functions as returned values && Currying
> We can use higher-order functions to convert a function that takes multiple arguments into a chain of functions that each take a single argument. More specifically, given a function f(x, y), we can define a function g such that g(x)(y) is equivalent to f(x, y). Here, g is a higher-order function that takes in a single argument x and returns another function that takes in a single argument y. This transformation is called _currying_.

```python
"""Gerneralization."""

def make_adder(n):
	"""Return a function that takes one arguments K and return K + N.
	
	>>> add_three = make_adder(3)
	>>> add_three(4)
	>>> 7
	"""
	def adder(k):
		return k + n
	return adder
```

We can call function as this
```python
make_addr(1)(2)
```
`make_addr(1)` will be evaluated as a function which make argument n plus 1.
This expression equals
```python
f = make_addr(1)
f(2)
```
Check type of `f`
```python
>>> f
<function make_adder at 0x000001C1DB635FE0>
```

