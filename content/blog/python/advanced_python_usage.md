+++
author = "Bowen She"
categories = ["python"]
tags = ["python"]
date = "2019-01-02"
description = "We are gonna discuss some advanced topics beyond common usage in string, list, tree in python. See what we've got here.."
featured = "space.JPEG"
featuredalt = "quiz time"
featuredpath = "/img"
linktitle = ""
title = "Advanced Topics in Python"
type = "post"
+++

# Iterators and Generators in Python

## The iteration protocol
```
class myIterator:
    def __init__(self):
        pass

    def __iter__(self):
        return self

    def __next__(self):
```

The protocol to create an Iterator contains two main parts: ```__iter__``` and ```__next__```. The ```__iter__``` returns the object we want to iterate over and the ```__next__``` mehtod is automatically on eahc iteration and that returns the value for the current iteration. *Notice: Python 2 use ```next``` and Python 3 use ```__next__()```*

## Generators
Generators in Python is another way of creating iterable objects and are usually used when you need to create iterable objects quickly, without the need of creating a class and adopting the iteration protocol. **To create a generator, you just need to define a function and then use ```yield``` keyword instead of return**.

TO create a fibonacci number stream generator, someone can write like this:

```python
def fibonacci():
  a, b = 0, 1

  while True:
    yield a
    a, b = b, a + b
```
If you want to add an end stop for the sequence generator, you can write like this:

```python
def fibonacci(max):
  a, b = 0, 1
  i = 0

  while i < max:
    yield a
    a, b = b, a + b
```

Then to test your generator to create a limit length sequence try this:

```Python
if __name__ == __main__():
    f = fibonacci(100)
    for i in f:
        print(i)
```

Please note that the iterator and the generator is "One-off consumed". We can't use them anymore once it reaches the end because in Python they can't be rewound. If you want to use it again, you have to declare a new generator instead.

# Play with iterable objects
Iterable objects give you a lot of possibility. If you want to create a list from previous generator, you can simply do:
```
my_fibonacci_list = list(fibonacci(100))
```
Another way of creating a list from an iterable objects is by using ***list comprehension*** that allow you to create a list in a very natural way, specifying also which elements to choose for the list.
```
fibonacci_odd_list = [i for i in fibonacci(100) if i % 2 == 1]
```
----

# Map and Reduce




great resources

https://www.quora.com/What-are-the-advanced-topics-in-python

https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-851-advanced-data-structures-spring-2012/lecture-videos/
