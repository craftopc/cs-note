# [Names, Assignment, and User-Defined Functions](https://www.youtube.com/watch?v=zYC7tKfKPtM&list=PL6BsET-8jgYULSxiV2garZ0FxbnXR08MP&index=2)
> What is the value of the final expression in this sequence?
> ```python
> f = min
> f = max
> g, h = min, max
> max = g
> max(f(2, g(h(1,5), 3)), 4)
> ```

Before exec `max(f(2, g(h(1,5), 3)), 4)`
- f <- max
- g <- min
- h <- max
- max <- min

So, this expression equal `min(max(2, min(max(1,5), 3)), 4)`
Result is 3

# [Environment Diagrams](https://www.youtube.com/watch?v=gyk0Qutui1s&list=PL6BsET-8jgYULSxiV2garZ0FxbnXR08MP&index=4)
Use this website to understand code step by step
[Python Tutor code visualizer: Visualize code in Python, JavaScript, C, C++, and Java](https://pythontutor.com/render.html#mode=edit)

![[Pasted image 20251104175725.png]]

Click "Visualize Execution" to observe your code step by step

![[Pasted image 20251104175944.png]]


# [Defining Functions](https://www.youtube.com/watch?v=j3uTRrPBrKk&list=PL6BsET-8jgYULSxiV2garZ0FxbnXR08MP&index=4)
Grammar:
>```python
>def <name>(<format parameters>):
>	return <return expression>
>```

Every expression is evaluated in the context of an environment
>```python
>from operator import mul
>def square(square):
>	return mul(square,square)
>square(-2)
>```

![[Pasted image 20251104181206.png]]

In "square" frame square is value -2 without `function square(square)`

The name is first searched for in the local frame. If it cannot be found, Python will continue searching in higher frames, such as the global frame, which is the highest scope.

# [Print and None](https://www.youtube.com/watch?v=jNYc5Gdwo3c&list=PL6BsET-8jgYULSxiV2garZ0FxbnXR08MP&index=5)
Explain why the result is this?
```python
>>> print(print(1), print(2))
1
2
None None
```

Some function no side effect, e.g.
```python
def add(a, b):
	return a + b
```
It only return a add b

But some function has some side effect, e.g.
```python
def my_print(s):
	print(s)
```

In first example, function return value type is maybe int/float/string. The type is decided by expression.
In second example, function don't return any. So for Python, this function return `None` this type.

# [Miscellaneous Python Features](https://www.youtube.com/watch?v=gDsdcF1bpBs&list=PL6BsET-8jgYULSxiV2garZ0FxbnXR08MP&index=6)
Use this struct can quickly write tests, which called doctests.
```python
def foo(x):
	"""A random function.
	
	>>> foo(4)
	4
	>>> foo(5)
	5
	"""
```

use command `python -m doctest file.py` to use it. e.g.
```cmd
PS E:\Data\Downloads\Compressed\lab01\lab01\my> python -m doctest .\file.py
**********************************************************************
File "E:\Data\Downloads\Compressed\lab01\lab01\my\file.py", line 4, in file.foo
Failed example:
    foo(4)
Expected:
    4
Got nothing
**********************************************************************
File "E:\Data\Downloads\Compressed\lab01\lab01\my\file.py", line 6, in file.foo
Failed example:
    foo(5)
Expected:
    5
Got nothing
**********************************************************************
1 item had failures:
   2 of   2 in file.foo
***Test Failed*** 2 failures.
PS E:\Data\Downloads\Compressed\lab01\lab01\my>
```
use `-v` option can output more information

doctest pass
```cmd
PS E:\Data\Downloads\Compressed\lab01\lab01\my> python -m doctest .\file.py
PS E:\Data\Downloads\Compressed\lab01\lab01\my>
```
