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



# An Introductory Example

```{index} single: Python; Introductory Example
```

## Overview

We are now ready to begin learning the Python language.

In this lecture, we will create and analyze small Python programs.

Our goal is to introduce you to fundamental Python syntax and data structures.

More advanced topics will be covered in future lectures.

Make sure you have read the {doc}`lecture <getting_started>` lecture before starting this one.


## The Task: Plotting a Sine Function

Here our goal is to plot Sin(x) where x get the values in the range [0,$2\pi$]

(ourfirstprog)=
Here are a few lines of code that perform the task we set

```{code-cell} ipython
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 2 * np.pi, 1000) # Generate a range of values from 0 to 2π (approximately 6.28)

y = np.sin(x) # Calculate the sine of each value in x

plt.plot(x, y) # Create a plot
plt.show()  # Display the plot
```

Let's break this program down and see how it works.

(import)=
### Imports

The first two lines of the program import functionality from external code
libraries.

The first line imports {doc}`NumPy <numpy>`, a favorite Python package for tasks like

* working with arrays (vectors and matrices)
* common mathematical functions like `cos` and `sqrt`
* generating random numbers
* linear algebra, etc.

After `import numpy as np` we have access to these attributes via the syntax `np.attribute`.

Here's two more examples

```{code-cell} python3
np.sqrt(4)
```

```{code-cell} python3
np.log(4)
```


#### Why So Many Imports?

Python programs typically require multiple import statements.

The reason is that the core language is deliberately kept small, so that it's easy to learn, maintain and improve.

When you want to do something interesting with Python, you almost always need
to import additional functionality.


#### Packages

```{index} single: Python; Packages
```

As stated above, NumPy is a Python package.

Packages are used by developers to organize code they wish to share.

In fact, a **package** is just a directory containing

1. files with Python code --- called **modules** in Python speak
1. possibly some compiled code that can be accessed by Python (e.g., functions compiled from C or FORTRAN code)
1. a file called `__init__.py` that specifies what will be executed when we type `import package_name`

You can check the location of your  `__init__.py` for NumPy in python by running the code:

```{code-block} ipython
:class: no-execute

import numpy as np

print(np.__file__)
```

#### Subpackages

```{index} single: Python; Subpackages
```

Consider the line `x = np.linspace(0, 2 * np.pi, 1000)`.

Here `np` refers to the package NumPy, while `linspace` is a **subpackage** of NumPy.

Subpackages are just packages that are subdirectories of another package. 

For instance, you can find folder `linspace` under the directory of NumPy.

### Importing Names Directly

Recall this code that we saw above

```{code-cell} python3
import numpy as np

np.sqrt(4)
```

Here's another way to access NumPy's square root function

```{code-cell} python3
from numpy import sqrt

sqrt(4)
```

This is also fine.

The advantage is less typing if we use `sqrt` often in our code.

The disadvantage is that, in a long program, these two lines might be
separated by many other lines.

Then it's harder for readers to know where `sqrt` came from, should they wish to.

### Evenly spaced numbers over a specified interval and evaluate output at these generated numbers

Returning to our program that plots Sine function, the remaining lines
after the import statements are

```{code-cell} ipython
x = np.linspace(0, 2 * np.pi, 1000)
y = np.sin(x)
plt.plot(x, y)
plt.show()
```

The first line return 1000 evenly spaced numbers over [0,$2\pi$] interval.

The next line compute the value of Sine function over each of the 1000 numbers in the interval

The next two lines genererate the plot.

