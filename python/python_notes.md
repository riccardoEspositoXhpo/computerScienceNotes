# Python Wiki

## Basics

### Code Basics

- Python code is executed line by line, no need to define a main function
- variable types do not have to be specified, they are inferred
- lines do not need endings
- colon is used for conditions, loops
- indentation is used to infer code blocks, instead of {}

```python

# user input
answer = input("Input name.")

# user output - string concatenation, only works if answer is string
print("hello, " + answer)

# user output 2 - works with any variable type
print(f"hello, {answer}")

```

## Loops and Conditions

```python

x = y = 0

if x < y:
    # x lower than y
elif x > y:
    # x larger than y
else:
    # x equal to y

i = 0:

if x in ['yes','no']:
    # do stuff

while i < 3:
    # do stuff
    i += 1

# infinite loop
while(True):
    # do stuff

# two for loops

for j in [0,1,2]:
    # do stuff

for k in range(3):
    # do stuff

```

## Data Types

- bool
- str (string)
- int
- float
- range - range of values, typically used in loops
- list - array, dynamic length (size). Mutable
- tuple - stores values in this form (x,y,...). Immutable
- dict - stores keys and values { "name" : "Beily", "number": 1}
- set - collection of values without duplicates

### Functions and main execution

- For safety, as the codebase expands, you may want to explicitly call out which functions you want to run. Code could look something like this:

```python

def main():
    barf(3)

def barf(n):
    for i in range(3):
        print("barf")

# this is one option to run only explicit functions
main()

# assuming your file is called main.py and your function is main
if __name__ == '__main__'
    main()

```

### Print Function 

```python

# print automatically puts a newline at the end of the print, you can override
print("hello", end = '') 

```

### User input

```python

from sys import argv

if len(argv) == 2:
    # do stuff
    print(argv[1])

```

### Files

```python

import csv

with open("file.csv","a") as file:
    writer = csv.writer(file)
    writer.writerow(["hello","world"])

    # read data into a python dict
    reader = csv.Dictreader(file)

    # looping file rows
    for row in reader:

        title = row["hello"]


```

## Advanced Topics


### Lambda Function

```python

titles = new Dict()

# the sorted function accepts a custom sorting algo
# the lambda function is a nemeless function, you just specify input/output
# in this case we are sorting, in reverse order, based on the value and not the key of the dict
sorted(title, key=lambda title: titles[title]), reverse = True)

```

### Sqlite

- Use sqlite3 library here instead of cs50

## Libraries and functions

```python

# list of libraries I have used

# image processing library
from PIL import Image, ImageFilter

# system lib - argv is for user input
from sys import argv

# file processing
import csv


```

## Tips and Tricks

```python

# sort array
sorted(array)



```