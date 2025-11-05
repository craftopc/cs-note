[Discussion 1 | CS 61A Fall 2025](https://cs61a.org/disc/disc01/)
# Q1: Race
```python
def race(x, y):
    """The tortoise always walks x feet per minute, while the hare repeatedly
    runs y feet per minute for 5 minutes, then rests for 5 minutes. Return how
    many minutes pass until the tortoise first catches up to the hare.

    >>> race(5, 7)  # After 7 minutes, both have gone 35 steps
    7
    >>> race(2, 4) # After 10 minutes, both have gone 20 steps
    10
    """
    assert y > x and y <= 2 * x, 'the hare must be fast but not too fast'
    tortoise, hare, minutes = 0, 0, 0
    while minutes == 0 or tortoise - hare:
        tortoise += x
        if minutes % 10 < 5:
            hare += y
        minutes += 1
    return minutes
```

> Find positive integers x and y (with y larger than x but not larger than 2 * x) for which either:
> - race(x, y) returns the wrong value or
> - race(x, y) runs forever


The core issue is in the `while` loop's condition. It's possible for the tortoise to "jump over" the hare's position without ever being at the same distance.

This happens when the hare is resting. For example, if the hare is at 20 meters and the tortoise is at 19 meters with a speed of 2 m/min, the tortoise's next position will be 21 meters. It completely misses the 20-meter mark, causing an infinite loop, not an error value.

The input pair `(x=3, y=4)` triggers this scenario. After the first 5 minutes, the hare has covered `4 * 5 = 20` meters and rests. The tortoise's distance goes from 18m (at minute 6) to 21m (at minute 7), skipping 20 entirely.

# Q2: Fizzbuzz
```python
def fizzbuzz(n):
    """
    >>> result = fizzbuzz(16)
    1
    2
    fizz
    4
    buzz
    fizz
    7
    8
    fizz
    buzz
    11
    fizz
    13
    14
    fizzbuzz
    16
    >>> print(result)
    None
    """
    "*** YOUR CODE HERE ***"
    for i in range(1, n + 1):
        if i % 3 == 0 and i % 5 == 0:
            print('fizzbuzz')
            continue
        if i % 3 == 0:
            print('fizz')
            continue
        if i % 5 == 0:
            print('buzz')
            continue
        print(i)
```

# Q3: Is Prime?
```python
from math import sqrt

def is_prime(n):
    """
    >>> is_prime(10)
    False
    >>> is_prime(7)
    True
    >>> is_prime(1) # one is not a prime number!!
    False
    """
    "*** YOUR CODE HERE ***"
    if n < 2:
        return False
    for i in range(2, int(sqrt(n))):
        if n % i == 0:
            return False
    return True
```

> Description Time: Come up with a one sentence description of the process you implemented to solve is prime that you think someone could understand without looking at your code. Try not to just read your code, but instead describe the process it carries out.

**Check if the number can be evenly divided by any integer in the range from 2 to its square root.**

# Q4: Unique Digits
```python
def unique_digits(n):
    """Return the number of unique digits in positive integer n.

    >>> unique_digits(8675309) # All are unique
    7
    >>> unique_digits(13173131) # 1, 3, and 7
    3
    >>> unique_digits(101) # 0 and 1
    2
    """
    "*** YOUR CODE HERE ***"
    count = 0
    for i in range(10):
        if has_digit(n, i):
            count += 1
    
    return count

def has_digit(n, k):
    """Returns whether k is a digit in n.

    >>> has_digit(10, 1)
    True
    >>> has_digit(12, 7)
    False
    """
    assert k >= 0 and k < 10
    "*** YOUR CODE HERE ***"
    while n > 0:
        if n % 10 == k:
            return True
        n //= 10
        
    return False
```

# Q5: Bottles
> 1. What determines how many different frames appear in an environment diagram?

d) The number of times user-defined functions are called when running the code

> 2. What happens to the return value of pass_it(bottles)?

a) It is used as the new value of remaining in the global frame

> 3. What effect does the line bottles = 98 have on the global frame?

c) It has no effect on the global frame.

# Q6: Double Trouble

# Q7: Repeating
```python
def repeating(t, n):
    """Return whether t digits repeat to form positive integer n.

    >>> repeating(1, 6161)
    False
    >>> repeating(2, 6161)  # repeats 61 (2 digits)
    True
    >>> repeating(3, 6161)
    False
    >>> repeating(4, 6161)  # repeats 6161 (4 digits)
    True
    >>> repeating(5, 6161)  # there are only 4 digits
    False
    """
    if pow(10, t-1) > n:  # make sure n has at least t digits
        return False
    end = n % pow(10, t)
    rest = n
    while rest:
        if rest % pow(10, t) != end:
           return False
        rest = rest // pow(10, t)
    return True
```

> The iterative process needed to implement this function is to check that the last t digits of the rest match the last t digits of n, then remove the last t digits of rest.