# Math for Programming

This wiki lists out some math concepts that are beyond trivial in case I need to access them in future development projects.

## Numbers

### Last Digit

```python

a = 12345

last_digit = a % 10 # answer is 5

```

### Loop Digits

```python

a = 12345

while a > 0:
    last_digit = a % 10
    a = a // 10 # make sure you are doing integer division so you don't end up with decimals


```

### Even and Odd

```python

number = 5

if number % 2 == 0:
    is_even = True

if number % 2 == 1:
    is_odd = True

```

## Geometry

### Trigonometry

Knowledge of trigonometry is helpful in designing output. Let us take the example of a unit circle

Definitions for SOH-CAH-TOA:

- SOH: Sin(x) = Opposite / Hypotenuse
- CAH: Cos(x) = Adjacent / Hypotenuse
- TOA: Tan(x) = Opposite / Adjacent

```python

import math

# thanks to the unit circle definition, the cos is equivalent to the x coordinate, whereas the sin represents the y

for i in range(0, 2 * math.pi, 0.001):
    circle_coord = (math.cos(i), math.sin(i))

```