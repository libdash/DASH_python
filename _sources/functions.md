---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(functions)=
```{raw} jupyter
<div id="qe-notebook-header" align="right" style="text-align:right;">
        <a href="https://quantecon.org/" title="quantecon.org">
                <img style="width:250px;display:inline;" width="250px" src="https://assets.quantecon.org/img/qe-menubar-logo.svg" alt="QuantEcon">
        </a>
</div>
```

# Functions

```{index} single: Python; User-defined functions
```

## Overview

Functions are an extremely useful construct provided by almost all programming.

We have already met several functions, such as

* the `sqrt()` function from NumPy and
* the built-in `print()` function

In this lecture we'll 

1. treat functions systematically and cover syntax and use-cases, and
2. learn to do is build our own user-defined functions.

We will use the following imports.

```{code-cell} ipython
import numpy as np
import matplotlib.pyplot as plt
```

## Function Basics

A function is a named section of a program that implements a specific task.

Many functions exist already and we can use them as is.

First we review these functions and then discuss how we can build our own.

### Built-In Functions

Python has a number of **built-in** functions that are available without `import`.

We have already met some

```{code-cell} python3
max(19, 20)
```

```{code-cell} python3
print('foobar')
```

```{code-cell} python3
str(22)
```

```{code-cell} python3
type(22)
```

The full list of Python built-ins is [here](https://docs.python.org/library/functions.html).


### Third Party Functions

If the built-in functions don't cover what we need, we either need to import
functions or create our own.

Examples of importing and using functions were given in the {doc}`previous lecture <python_by_example>`

Here's another one, which tests whether a given year is a leap year:

```{code-cell} python3
import calendar
calendar.isleap(2024)
```

## Defining Functions

In many instances it's useful to be able to define our own functions.

Let's start by discussing how it's done.

### Basic Syntax

Here's a very simple Python function, that implements the mathematical function $f(x) = 2 x + 1$

```{code-cell} python3
def f(x):
    return 2 * x + 1
```

Now that we've defined this function, let's *call* it and check whether it does what we expect:

```{code-cell} python3
f(1)   
```

```{code-cell} python3
f(10)
```

Here's a longer function, that computes the absolute value of a given number.

(Such a function already exists as a built-in, but let's write our own for the
exercise.)

```{code-cell} python3
def new_abs_function(x):
    if x < 0:
        abs_value = -x
    else:
        abs_value = x
    return abs_value
```

Let's review the syntax here.

* `def` is a Python keyword used to start function definitions.
* `def new_abs_function(x):` indicates that the function is called `new_abs_function` and that it has a single argument `x`.
* The indented code is a code block called the *function body*.
* The `return` keyword indicates that `abs_value` is the object that should be returned to the calling code.

This whole function definition is read by the Python interpreter and stored in memory.

Let's call it to check that it works:

```{code-cell} python3
print(new_abs_function(3))
print(new_abs_function(-3))
```


Note that a function can have arbitrarily many `return` statements (including zero).

Execution of the function terminates when the first return is hit, allowing
code like the following example

```{code-cell} python3
def f(x):
    if x < 0:
        return 'negative'
    return 'nonnegative'
```

(Writing functions with multiple return statements is typically discouraged, as
it can make logic hard to follow.)

Functions without a return statement automatically return the special Python object `None`.

(pos_args)=
### Keyword Arguments

```{index} single: Python; keyword arguments
```

Keyword arguments are passed to functions using the parameter names explicitly. This allows you to pass arguments in any order. Here’s an example:

```{code-cell} python3
def greet(name, age):
    print(f"Hello, my name is {name} and I am {age} years old.")

# Using keyword arguments
greet(age=30, name='Alice')
```

In this user-defined function call to greet function, notice that the arguments are passed in `name=argument` syntax.

This is called  *keyword arguments*, with age and name being the keywords.

Keyword arguments are particularly useful when a function has a lot of arguments, in which case it's hard to remember the right order.

You can adopt keyword arguments in user-defined functions with no difficulty.

Non-keyword arguments are called *positional arguments*, since their meaning
is determined by order.

### The Flexibility of Python Functions

As we discussed in the {ref}`previous lecture <python_by_example>`, Python functions are very flexible.

In particular

* Any number of functions can be defined in a given file.
* Functions can be (and often are) defined inside other functions.
* Any object can be passed to a function as an argument, including other functions.
* A function can return any kind of object, including functions.

We will give examples of how straightforward it is to pass a function to
a function in the following sections.

### One-Line Functions: `lambda`

```{index} single: Python; lambda functions
```

The `lambda` keyword is used to create simple functions on one line.

For example, the definitions

```{code-cell} python3
def f(x):
    return x**3
```

and

```{code-cell} python3
f = lambda x: x**3
```

are entirely equivalent.

To see why `lambda` is useful, suppose that we want to calculate $\int_0^2 x^3 dx$ (and have forgotten our high-school calculus).

The SciPy library has a function called `quad` that will do this calculation for us.

The syntax of the `quad` function is `quad(f, a, b)` where `f` is a function and `a` and `b` are numbers.

To create the function $f(x) = x^3$ we can use `lambda` as follows

```{code-cell} python3
from scipy.integrate import quad

quad(lambda x: x**3, 0, 2)
```

Here the function created by `lambda` is said to be *anonymous* because it was never given a name.


### Why Write Functions?

User-defined functions are important for improving the clarity of your code by

* separating different strands of logic
* facilitating code reuse

(Writing the same thing twice is [almost always a bad idea](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself))

