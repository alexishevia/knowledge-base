# Python 3 Cheatsheet

## Books and references
- [Dive into Python3](http://www.diveintopython3.net/)
- [The Django Book](https://djangobook.com/)

## Jupyter
The Jupyter Notebook is an open-source web application that allows you to
create and share documents that contain live code, equations, visualizations
and narrative text.
http://jupyter.org/

```
# start the notebook
jupyter notebook
```

jupyter notebook extensions:
https://github.com/ipython-contrib/jupyter_contrib_nbextensions

## Managing Dependencies

### pipenv
Apparently, pipenv is the oficially recommended tool for managing dependencies in Python.
https://docs.pipenv.org/

- initialize your Pipfile
    ```
    # for python2
    pipenv --two

    # for python3
    pipenv --three
    ```

- add a dependency
    ```
    pipenv install <dependency_name>
    pipenv install jupyter
    ```

- install all dependencies for a project
    ```
    pipenv install
    ```

- activate this project's virtualenv, run the following:
    ```
    pipenv shell
    ```

### virtualenvwrapper
virtualenvwrapper was the old way of managing dependencies in Python. You should look into pipenv now.
```
# install
sudo pip install virtualenvwrapper

# create a new env
mkvirtualenv foo -p python2  # python 2
mkvirtualenv foo -p python3  # python 3

# enter virtualenv
workon foo

# exit virtualenv
deactivate

# destroy virtualenv
rmvirtualenv foo
```

## types

```
Value                            | Type  | Mutable?  | Truthy?
--------------------------------------------------------------
1                                | int   | Immutable | True
0                                | int   | Immutable | False
0.1                              | float | Immutable | True
0.0                              | float | Immutable | False
"hello"                          | str   | Immutable | True
""                               | str   | Immutable | False
[1,2,3,3]                        | list  | Mutable   | True
[]                               | list  | Mutable   | False
(1,2,3,3)                        | tuple | Immutable | True
()                               | tuple | Immutable | False
{1,2,3,4}                        | set   | Mutable   | True
{}                               | set   | Mutable   | False
{'hello': 'world', 'foo': 'bar'} | dict  | Mutable   | True
{}                               | dict  | Mutable   | False
```

## comprehensions

### list comprehensions

map
```
>>> a_list = [1,2,3,4]
>>> [elem * 2 for elem in a_list]
[2, 4, 6, 8]
```

filter
```
>>> a_list = [1,2,3,4]
>>> [elem for elem in a_list if elem % 2 == 0]
[2, 4]
```

### dictionary comprehensions
```
>>> a_list = [1,2,3,4]
>>> {elem: elem * 2 for elem in a_list}
{1: 2, 2: 4, 3: 6, 4: 8}
```

```
>>> a_dict = { 'superman': 'Clark Kent', 'batman': 'Bruce Wayne', 'hulk': 'Bruce Banner'}
>>> { key: "Hello " + val for key, val in a_dict.items()}
{'batman': 'Hello Bruce Wayne', 'hulk': 'Hello Bruce Banner', 'superman': 'Hello Clark Kent'}
```

### set comprehensions
```
>>> {x ** 2 for x in {1,2,3}}
{1, 4, 9}
```

### generator functions
the syntax is similar to list comprehensions, but use parens `()` instead of
brackets `[]`. The result is a generator object, which you can pass to
functions like `list()` or `set()`, or you can iterate through it using `next()`
or `for`.
```
>>> a_list = [1,2,3,4]

>>> gen = (x ** 2 for x in a_list)
>>> list(gen)
[1, 4, 9, 16]

>>> gen = (x ** 2 for x in a_list)
>>> next(gen)
1
>>> next(gen)
4

>>> gen = (x ** 2 for x in a_list)
>>> for n in gen:
...   print(n, end=' ')
1 4 9 16
```

## generators

```
def fib(max):
  a, b = 0,1
  while a < max:
    yield a
    a, b = b, a + b

>>> list(fib(1000))
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987]
```

## iterators
A class that implements an `__iter__` method. (must return an object with a
`__next__` method - usually itself)
```
class Fib:
  '''iterator that yields numbers in the Fibonacci sequence'''

  def __init__(self, max):
    self.max = max

  def __iter__(self):
    self.a = 0
    self.b = 1
    return self

  def __next__(self):
    fib = self.a
    if fib > self.max:
      raise StopIteration
    self.a, self.b = self.b, self.a + self.b
    return fib


>>> for n in Fib(1000):
...   print(n, end=' ')
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987


>>> iterator = iter(Fib(1000))
>>> next(iterator)
0
>>> next(iterator)
1
```

## useful constructs

```
# list slicing
>>> a_list = [1,2,3,4]
>>> a_list[0:3]
[1, 2, 3]

# destructuring
>>> (a, b, c) = ['A', 'B', 'C']
>>> a
'A'
>>> b
'B'
>>> c
'C'
```

## debugging

[pdb](https://docs.python.org/3/library/pdb.html) - The Python debugger

```
import pdb; pdb.set_trace()
```
