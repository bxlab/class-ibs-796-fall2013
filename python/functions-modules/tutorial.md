---
layout: lesson
root: ../..
title: Flow Control in Python
---

# Functions and Modules

At this point, we've been over the basics of the python language except for the parts that allow you to reuse code you and others have written. Now we will talk about writing functions (sometimes called functions), then we'll talk about modules.

## Functions

Lets say you frequently want to calculate a list of values of power given a list of voltages and a list of currents. You could continually drop the for loop we wrote before into your code, but this approach quickly becomes unwieldy and error prone. The solution is to abstract this  create a function. Here's how.

```python
def calcpower(voltageList, currentList):
  powerList = [] # Initialize an empty list to be filled later.
  indxList = range(len(currentList))

  for indx in indxList:
    power = voltageList[indx] * currentList[indx]
    powerList.append(power)

  return powerList
```

That's it: just a block containing the code we already wrote plus one extra line. The return statement at the end tells python that when the function is done executing, hand back the value of powerList.

You can call this function at any point in the following way:

```python
calcpower(voltageList, currentList)
```

In fact, we've been using functions almost this entire time:

```python
len()
type()
"string!".upper()
```

and so on.

We just looked at one way to construct a function; there are more. Lets say we wanted to write the ugliest function ever that calculates and returns a value raised to a power. (In fact, this function already exists, so writing a new one is a terrible idea). Here's how it would look:

```python
def topower(base,expt):
  product = 1
  for indx in range(expt):
    product = product * base

  return product
```

Seriously though, don't ever use the above code.

What if most of the time we were just squaring a number? We'd want a default value of 2 for the exponent.

```python
def topower(base,expt = 2):
  product = 1
  for indx in range(expt):
    product = product * base

  return product
```

In this case, we are setting the default value to 2. We can change that value when we call the command, but we don't always need to set it to 2.

**Exercise**

Make a function that calculate the GC content of a given DNA sequence. Your function should able to handle sequences of mixed case (see the third test case).

```python
def calculate_gc(x):
    """Calculates the GC content of DNA sequence x.
    x: a string composed only of A's, T's, G's, and C's."""
    ???
```

Test cases:

```python
print round(calculate_gc('ATGC'), ndigits = 2) == 0.50
print round(calculate_gc('AGCGTCGTCAGTCGT'), ndigits = 2) == 0.60
print round(calculate_gc('ATaGtTCaAGcTCgATtGaATaGgTAaCt'), ndigits = 2) == 0.34
```

## Modules

Python has a lot of useful data type and functions built into the language, some of which you have already seen. For a full list, you can type dir(__builtins__). However, there are even more functions stored in modules. 
Modules are a way to package code for reuse at a later time. You can buld your own modules, install others' modules, or use built-in modules provided from python.

Lets do the exponents right. It turns out that python ships with a math module containing exactly that functionality. Here's how you bring it in to your environment.

```python
import math
```

Now we can do exponents, say 3^2

```python
math.pow(3,2)
```

How about 2^4?

```python
math.pow(2,4)
```

Writing a function to create this functionality was a terrible idea because the math module already exists. The math module has other functions like sine, cosine, exp, and so on.

There are other ways to pull from modules into your environment. If you only wanted the sine function, you could import it like so

```python
from math import sin
```

and you'd be able to directly use it without a dot.

```python
sin(3)
```

If you want to pull in everything from the math module, but you're too lazy to type out "math" all the time, you can give the module an alias

```python
import math as mth
```

or whatever you want the alias to be.

One final way to import stuff is to use the asterisk notation. This approach is almost always a terrible idea, so you probably shouldn't do it.

```python
from math import *
```

It is a terrible idea because you dump all of the names of data and functions into your local namespace. If you already have data or functions of the same name, you can end up facing some nasty problems.

## Exercise

Define your own module called dnautils (by creating a file dnautils.py) which contains a function that transcribes DNA into RNA. Specificall, Write a function that mimics transcription. The input argument is a string that contains the letters A, T, G, and C. Create a new string following these rules:

 * Convert A to U
 * Convert T to A
 * Convert G to C
 * Convert C to G

To check your work from the intepreter:

```python
import dnautils
assert( transcribe('ATGC') == 'UACG' )
assert( transcribe('ATGCAGTCAGTGCAGTCAGT') == 'UACGUCAGUCACGUCAGUCA' )
```


======

**Based on materials from Joshua R. Smith and Milad Fatenejad**
