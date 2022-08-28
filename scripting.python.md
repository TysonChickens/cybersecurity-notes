---
id: zgnlnwhkc5699kp1myzjann
title: Python
desc: ''
updated: 1653180236036
created: 1653180229128
---

# Python Basics

- [ ] Understand what the benefits are of using Python.

- [ ] Describe the basic syntax of Python.
- [ ] Describe Python data structures.
- [ ] Describe the basic syntax of conditions and branching.

- [ ] Understand functions and methods of Python scripting.
- [ ] Describe Python Libraries.
---

## Benefits of Using Python

Worldwide, Python is the most popular language, Python gew the most in the last 5 years (19.4%) and Java lost the most (-7.2%).

1. Open Source
2. Easy to learn and implement
3. Portable
4. High Level
5. Can be used for almost anything in cybersecurity
6. Extensive libraries

## Getting Started with Python

- Variables
- `>>>`
- PEP8
- .py

### Data Types

#### Data Structures

![Data](https://miro.medium.com/max/3576/1*QfI8H_8HplGa1v9IrrWjBA.png)

### Conditions and Branching

#### If-Else

To trigger a command, given a certain condition, we can use `if`, `elif`, `else` statements:

![if-else-statement](https://cdn.educba.com/academy/wp-content/uploads/2019/09/If-Else-Statement-in-Python.png)

- `if` establishing the first condition.
- `elif` is used when many conditions are possible.
- `else` will execute its command if none of the `if` and `elif` conditions were met.

#### For Loops

![for-loop](https://cdn.techbeamers.com/wp-content/uploads/2018/08/Python-For-Loop-Flowchart.png)

- Loops allow to iterate a task.
- For loops allow to execute a block of statements multiple times.

``` python
for element in sequence:
    block of statements
```

#### While Loops

![while-loop](https://files.realpython.com/media/t.899f357dd948.png)

- For loops execute a statement a set number of times.
- While loops run only if a condition is met.

``` python
while condition:
    block of statements
```

``` python
i = 0
while (L[i] >= 0):
    print(L[i])
    i = i+1
```

#### Functions & Methods

A function is a named sequence of statements that performs a desired operation.

- Python has many built-in functions:
  - type(4) &rarr; int
  - len([1,2,3]) &rarr; 3
  - sum([1,2,3]) &rarr; 1+2+3=6
  - float(6) &rarr; 6.0
  - print("Hello World") &rarr; 'Hello World'

Define own function with:

``` python
def function_name(input_parameters)
    body of function
    return output
```

- Functions allow to write own chain of commands, simplifying the readability.
- Reusable, define once... Use many times.

A method is a function that "belongs to" an object.

- Methods are a set of procedures for interacting with the data in an object.
- Methods are similar to functions, but there are some differences.

### Libraries

#### Scientific Computing:

- Pandas (data structure & tools)
- NumPy (arrays & matrices)
- SciPy (integrals, solving differential equations, optimization)

#### Visualization:

- Matplotlib (most popular for plots & graphs)
- Seaborn (heat maps, time series & violin plots)

#### Algorithmic

- Scikit-learn (tools for statistical modeling: regression, classification, clustering...)
- StatsModels (explore data, estimate statistical models, and perform statistical tests)