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






## Advanced Topics


## Libraries and functions

