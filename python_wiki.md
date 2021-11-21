# Python Wiki

## General

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

### Loops and Conditions

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

try:
    # try to do something

except: 
    # do something else if you failed

except ValueError:
    # do something in case of specific error

except FileNotFoundError:


```

### Data Types

- bool
- str (string)
- int
- float
- range - range of values, typically used in loops
- list - array, dynamic length (size). Mutable
- tuple - stores values in this form (x,y,...). Immutable
- dict - stores keys and values { "name" : "Beily", "number": 1}
- set - collection of values without duplicates

### Copying Data

```python

#python simplifies a lot, but we must remember that this is still built on top of C.
#this means that we still have a memory address for data, and the value of that address
# copying a variable can have undesired effects, because it could just essentially point two pointers to the same address


import copy

def main():

    # Ensure correct usage
    if len(sys.argv) != 3:

        sys.exit("Usage: python dna.py DATABASE.csv SAMPLE.csv")

    # load the database into a dict
    sequenceCount = []

    with open(sys.argv[1], "r") as database:

        reader = csv.DictReader(database)

        for row in reader:

            sequenceCount.append(row)

    # define an identical dict with no name key
    sequenceCountNoName = copy.deepcopy(sequenceCount)

    for i in range(len(sequenceCountNoName)):

        sequenceCountNoName[i].pop('name')

# The point here is that if you don't deepCopy, this code will pop name from both objects.


```

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

    # please note the if condition remains the same, but the code block to be executed does not need to be "main"
    main()

```

Functions can also take default values.

```python

def sum_stuff(a, b, c = 5):

    return (a + b + c)

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

### Lambda Function

A lambda function is a nameless function that is used to create a function with very few keystrokes. It accepts inputs and returns outputs.

```python

titles = new Dict()

# the sorted function accepts a custom sorting algo
# the lambda function is a nemeless function, you just specify input/output
# in this case we are sorting, in reverse order, based on the value and not the key of the dict
sorted(title, key=lambda title: titles[title]), reverse = True)

# another example of lambda
squares = lambda x : x * x 

# squares(3)
# 9

# the above can equivalently be called with
# (lambda x : x * x)(3)

```


### List Comprehensions

Time and Space efficient ways to create lists in python

```python

fruits = ["apple", "banana", "cherry", "kiwi", "mango"]

# simple list
newlist = [x for x in fruits]

# condition
newlist = [x for x in fruits if "a" in x]

# iterable
newlist = [x for x in range(10)]

# iterable with condition
newlist = [x for x in range(10) if x < 5]

# other manipulations
newlist = [x.upper() for x in fruits]

# modify elements
newlist = ['hello' for x in fruits]

# expressions
newlist = [x if x != "banana" else "orange" for x in fruits]

# n dimensional array of 0 
array = [0 for i in range(n)] for i in range(n)


```

### Loading Configuration Files

```python

# separate sample file config.yml
script_options:
  # Switch between testnet and mainnet
  # Setting this to False will use REAL funds, use at your own risk
  VARIABLE_NAME: True

# python script
import yaml

def configLoader():
    file = './config.yml'

    try:
        with open(file) as file:
            return yaml.load(file, Loader=yaml.FullLoader)
    except FileNotFoundError as fe:
        exit(f'Could not find {file}')

    except Exception as e:
        exit(f'Encountered exception...\n {e}')


parsed_config = configLoader()

VARIABLE_NAME = parsed_config['script_options']['VARIABLE_NAME']


```

### Threading

Threading enables you to run a python program and execute multiple scripts at the same time in "threads".

```python

import threading
import importlib

my_module = {}

MODULES = [
    'modulename1',
    'modulename2'
]

for module in MODULES:
    
    # dynamically imports modulename1.py and modulename2.py
    mymodule[module] = importlib.import_module(module)

    # starts threads by calling "function_name" function, has ability to pass args
    # it is ideal to create modules with exactly the same function names so you can scalably reference them
    thread = threading.Thread(target=mymodule[module].function_name, args=())
    thread.daemon = True
    thread.start()

```

### Coloring Console Output

```python

from colorama import init
init()

# for colorful logging to the console
class txcolors:
    WARNING = '\033[93m'
    BAD = '\033[91m'
    GOOD = '\033[32m'
    DIM = '\033[2m\033[35m'
    DEFAULT = '\033[39m'


```

### Variable Scope

```python

number = 5

def bad_scoping():

    # this breaks because number is not initialized
    number += 5 
    print(number)

def good_scoping():

    # access a global variable
    global number

    number += 5
    print(number)

```

### String Operations

```python

# Strings are immutable, when you modify a string it typically returns a new string back
string = "hello how are you"

if "hello" in string:
    # this is True

new_string = string.replace("hello", "hello guys")

if string.endswith("you"):
    # this is True

string = 'Hey, how are you?'

string.split(',') # default is to split by space


```

### Web Scraping - BeautifulSoup

Beautiful soup is used for HTML scraping. It formats and does error handling and returns the HTML in a consumable format

```python
import requests
from bs4 improt BeuatifulSoup

page = requests.get('https://something.somethingelse.com')
soup = BeautifulSoup(page.content, 'html.parser')

# prints the HTML page with indents
print(soup.prettify())

# prints ['html', 'n', <html> <head> <title>A simple example page</title> </head> <body> <p>Here is some simple content for this page.</p> </body> </html>]
list(soup.children)

# [bs4.element.Doctype, bs4.element.NavigableString, bs4.element.Tag]
newList = [type(item) for item in list(soup.children)]

# from the top we infer that all the tags are in the second element of the list
html = list(soup.children)[2]

# ['n', <head> <title>A simple example page</title> </head>, 'n', <body> <p>Here is some simple content for this page.</p> </body>, 'n']
list(html.children)

# grab the body
body = list(html.children)[3]

# grab the p tags within body - ['n', <p>Here is some simple content for this page.</p>, 'n']
list(body.children)

# isolate p tag
p = list(body.children)[1]

# returns 'Here is some simple content for this page.'
p.get_text()

# find all instances of a tag - we can loop through this list
soup.find_all('p')

# returns first instance of p
soup.find('p')

# find all elements in p with outer-text class
soup.find_all('p', class_='outer-text')

# can search by id 
soup.find_all(id="first")

# tags can be found by using the select method and CSS notation
soup.select("div p") # find all p tags inside div tags


```

### Regular Expressions

Also known as regexp or regex, they provide shortcuts to match strings of text.

```python

# library to access regular expressions

import re
""" Regular Expression Dictionary

^        Matches the beginning of a line

$        Matches the end of the line

.        Matches any character

\s       Matches whitespace

\S       Matches any non-whitespace character

*        Repeats a character zero or more times

*?       Repeats a character zero or more times (non-greedy)

+        Repeats a character one or more times

+?       Repeats a character one or more times (non-greedy)

[aeiou]  Matches a single character in the listed set

[^XYZ]   Matches a single character not in the listed set

[a-z0-9] The set of characters can include a range

(        Indicates where string extraction is to start

)        Indicates where string extraction is to end

"""

# functions

# searches for a patter within a string - returns boolean
re.search()

# searches for all instances of a pattern within a string - returns a list. If not match, list is empty
re.findall()

# examples
text = 'From: Beily'

# searches start of string
re.search('^From:', text)

textArray = [
'X-Sieve: CMU Sieve 2.3',
'X-DSPAM-Result: Innocent',
'X-Plane is behind schedule: two weeks',
'X-: Very short'
]

for text in textArray:

    # searches start of string for X, any character, repeated 0 or more times, and : - this matches lines 0,1,2,3
    re.search('^X.*:', text)

    # searches for X-, matches any non-whitespace character one or more times - this matches 0,1
    re.search('^X-/S+:')

text = 'My 2 favorite numbers are 19 and 42'

# matches every instance of numerical values of one or more digits
output = re.findall('[0-9]+', text) # returns ['2', '19', '42']

# greedy matching example - by default we try to match the largest possible string
text = 'From: Using the : character'

output = re.findall('^F.+:', text) # returns ['From: Using the :']
output = re.findall('^F.+?:', text) # returns ['From:'], adding the ? removes greedy matching

# example - retrieving an email address
re.findall('/S+@/S+', text)

# using parentheses can fine-tune what sub-sting to extract
text = 'From example@email.com'

# parentheses say what to extract. This ensures we extract an email but only if line starts with 'From'
re.findall('^From (/S+@/S+)', text)

# extract email domain from substring
text = 'From stephen.marquard@uct.ac.za Sat Jan  5 09:14:16 2008'

# find an @ sign, match non-blank character, one or more times. only extract these non-blank characters
output = re.findall('@([^ ]*)', text)

# more precise version of above
output = re.findall('^From .*@([^ ]*)', text)

```

### Classes

Classes in python, and other programming languages, are blueprints. Python is an object-oriented programming language, meaning that even the most primitive data types we use are actually classes.

When you initialize a list, for example:

```python

my_list = [1, 2, 3]

# this is a "list" class
type(my_list)

# this will enumerate all the "methods" associated to this class
dict(my_list)
```

Some important concepts are as follows:

- Classes are blueprints for "types" of data - a list, a string, a dictionary
- an Object is an "instance" of a class. my_list is an instance of a List class
- Classes have properties, and a list of functions associated with them. These are called "methods"

```python

# class example - create a Person data type

class Person:
    "This is the document string"

    # some class attribute
    age = 10

    # method - self is some "anticipatory" concept, it contains the name of the future object of this class
    def greet(self):
        print("Hello")

# prints 10
print(Person.age)

# Prints "This is the document string"
print(Person.__doc__)

# create an object of this class
Beily = Person()

# prints "Hello"
print(Beily.greet())

```

Classes are commonly defined with an __init__ method - a block of code that executes whenever you create an instance.

```python

class ComplexNumber:
    def __init__(self, r=0, i=0):
        self.real = r
        self.imag = i

    def get_data(self):
        print(f'{self.real}+{self.imag}j')


# Create a new ComplexNumber object
num1 = ComplexNumber(2, 3)

# Call get_data() method
# Output: 2+3j
num1.get_data()

# Create another ComplexNumber object
# and create a new attribute 'attr'
num2 = ComplexNumber(5)
num2.attr = 10

# Output: (5, 0, 10)
print((num2.real, num2.imag, num2.attr))

# but c1 object doesn't have attribute 'attr'
# AttributeError: 'ComplexNumber' object has no attribute 'attr'
print(num1.attr)

# delete an attribute
del num1.attr

# this won't work anymore
print(num1.attr)

# delete an object
del num1

```  

One way to scalably create classes is to re-use a previous class as a template. This is called inheritance.

```python

# this describes a polygon, object with 3 or more sides
class Polygon:
    def __init__(self, no_of_sides):
        self.n = no_of_sides
        # defines empty list with length number of sides
        self.sides = [0 for i in range(no_of_sides)]

    # this method asks us to fill the sides
    def inputSides(self):
        self.sides = [float(input("Enter side "+str(i+1)+" : ")) for i in range(self.n)]

    # this method displays the sides 
    def dispSides(self):
        for i in range(self.n):
            print("Side",i+1,"is",self.sides[i])


# if I want to define a triangle, I can re-use the properties of Polygon

class Triangle(Polygon):
    def __init__(self):
        # define a Triangle as a Polygon with 3 sides
        Polygon.__init__(self,3)

    def findArea(self):
        a, b, c = self.sides
        # calculate the semi-perimeter
        s = (a + b + c) / 2
        # just trust me this is the formula
        area = (s * (s - a) * (s - b) * (s - c)) ** 0.5
        print("The area of the triangle is ", area)

```

Please note that the Triangle Class and the Polygon Class both have an __init__ method. When calling the triangle class, its __init__ takes precedence.

### Docstring and Assert

Python programs can contain a small sample execution to test if the program is working as expected. 

```python

def sum_positive(x, y):
    """ Sum x and y if both positive or return 0

    >>> sum_positive(0,2):
    2
    >>> sum_positive(3,4):
    7
    >>> sum_positive(-1,2):
    0
    """"

    if x > 0 and y > 0:
        return x + y
    
    else:
        return 0

```

In order to test the correctness of the function or display the test itself, we can run these commands

```unix

# in the terminal - run the doctest
python -m doctest -v sum_positive.py

# in a python shell - display the docstring
help(sum_positive)

# alternative doctests in shell
from doctest import testmod, run_docstring_examples

# tests everything within sum_positive.py
testmod()

# tests a single function - second argument always fixed, thirs is to "verbose"
run_docstring_examples(sum_positive, globals(), True)

```

Some functions require a certain domain of inputs. When these are not provided, it is useful to make the call fail. An assert statement can help with this.

```python

def invert(x):

    return 1 / x

```

Notice how this function would break if we provide an input of 0. A solution is to use an assert statements.

```python

def invert(x):

    assert x != 0, 'Division by 0 breaks math.'

    return 1 / x

```

In this case, when we call the function with an input of 0 it will nicely exit with a traceback, and print our message to the console.

### Quine (Python)

A Quine is a program that writes itself. Purely developed for fun, here are two quines I have come up with, depending on whether the code is in a stand-alone function or part of a string.

```python

# case 1 - quine.py
quine = "print('quine = ' + repr(quine) + '; eval(quine)')"; eval(quine)

"""
    >>> python3 quine.py
    quine = "print('quine = ' + repr(quine) + '; eval(quine)')"; eval(quine)
"""
# case 2 - just the string is executed

quine = 'repr(print(eval(\'quine\'),end=\'\'))'


""" 
    >>> exec(quine)
    repr(print(eval('quine'),end=''))

```

### Short Circuit

Logical operators can be used in a neat way - because Python does not evaluate expressions unnecessarily. This is a form of control.

As an example, if I have:

```python

# The first value is False, the second value is never evaluated
>>> (1 + 1 == 3) and (2 + 5 == 7)

# The first value is True, the second value is never evaluated
>>> (1 + 1 == 2) and (1 + 5 == 50)

```

When is this useful? If we have operations that are not allowed, we can add a logical operator as a safety check. For example, if we divide by 0 or if we calculate the sqrt() of a negative number.

Short-circuit also exists in conditional expressions:

```python

>>> x = 0
>>> abs(1/x if x != 0 else 0)

# The above will print 0 instead of crashing, because it never evaluates 1/x
```

### Higher Order Functions

A powerful means of abstration is when we use a function to manipulate other functions.

One common usecase is if we have to repeat a slightly similar operation more than once. For example, let's assume we need to sum some squares and also sum some cubes - this is an opportunity for abstraction.

```python

# general function - performs a sum by calling the function term
def summation(n, term):
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total

# define a cube
def cube(x):
    return x*x*x

# define a square
def square(x):
    return x*x

# summing a cube n times, means calling summation and saying that the term should be a cube
def sum_cubes(n):
    return summation(n, cube)

# same example as above
def sum_squares(n):
    return summation(n, square)

result_cubes = sum_cubes(3)
result_squares = sum_squares(3)

```

Sometimes we define a generic function that performs an activity, but it may require more inputs than we can provide. By nesting functions within functions we can attempt to solve this - warning, this is mind-bending.

```python


def average(x, y):
    return (x + y)/2

"""This is our generic function. It starts from 1 and tries to guess what we are looking for.

It calls a close function to see if the guess is correct, in our case the difference is less than 1e-3.
While that is false, it updates the guess according to some method we specify.

Here lies the problem. Our generic update(guess) can only update the guess based on the guess parameter, it does not take two inputs.

We solve this with nested functions, aka Closures.

"""
def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess

def approx_eq(x, y, tolerance=1e-3):
    return abs(x - y) < tolerance

def sqrt(a):

    # the update function for a square root requires the current guess but also the actual square root 
    def sqrt_update(x):
        return average(x, a/x)

    # same goes for the close function
    def sqrt_close(x):
        return approx_eq(x * x, a)
    
    # we can call improve from within the function. Improve will exit first looking for close(guess). 
    # However, close(guess) is defined as sqrt_update(x) which actually passes two parameters to average.
    # Notice how by defining all of this within sqrt(a), you have also access to a in the local frame
    return improve(sqrt_update, sqrt_close)

result = sqrt(256)

```

To clarify the example, let's see what would happen if we do not nest functions.

```python

def average(x, y):
    return (x + y)/2

def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess

def approx_eq(x, y, tolerance=1e-3):
    return abs(x - y) < tolerance


# what is a?
def sqrt_update(x):
    return average(x, a/x)
def sqrt_close(x):
    return approx_eq(x * x, a)

# Here lies the problem. How can I call the improve function... if I don't know what square root I'm looking for..?
# Ok, I could globally define a = 256, but that is a poor way to calculate a square root.
# Much better to have it defined like above, where I can pass whatever-a I want to it.
square_root = improve(sqrt_update, sqrt_close)

```

As a last sub-topic, decorators are a way to run higher-order functions in short-hand notation. A common use-case for this is a trace.

```python

def trace(x):
    def wrapped(x):
        print('-> ', fn, '(', x, ')')
        return fn(x)
    return wrapped

@trace
def triple(x):
    return 3 * x 

# the above is equivalent to saying:
triple = trace(triple)

```

The output of running in the python shell:

```unix

>>> triple(12)
->  <function triple at 0x102a39848> ( 12 )
36

```

Another common use-case for decorators is to enhance a function.

```python

# avoids division by 0
def smart_divide(func):
    def inner(a, b):
        print("I am going to divide", a, "and", b)
        if b == 0:
            print("Whoops! cannot divide")
            return

        return func(a, b)
    return inner


@smart_divide
def divide(a, b):
    print(a/b)

# the above divide function is enhanced with the smart_divie logic. But you can still call divide(5, 0)

```

## Projects

### Project Requirements

requirements.txt is used to flag the library requirements in order to run the app.

Assuming you are working in a virtual environment (meaning you only install the packages you need), this can be achieved by:

```bash

pip install pipreqs

pipreqes /path/to/project

```

When you already have a requirements.txt file, you can install by:

```bash

pip install -r requirements.txt

```

### Virtual Environments

Since python is known for the large number of libraries, it is easy to clutter the system. In addition, code could work on your machine given a very specific version number of a library, but not work on other machines.

In order to isolate our development environment from any external factors and avoid cluttering our machine we can use virtualenv

```python

pip isntall virtualenv

# creates a virtual environment in the current directory
virtualenv project_name

# switches your python interpreter to read from virtualenv
source project_name/bin/activate

```

Good practice when setting up multiple virtual environments is to split your directories as follows:

- Projects
  - proj_1
  - proj_2
- VirtualEnvs
  - proj_1
  - proj_2

This ensures that we keep a consistent naming convention, knowing which is which, but also that we don't clutter the Project directory with virtualenv system files, especially if we intend to use GIT and don't want to ".gitignore" all the files.

## Databases

### Sqlite

```python

# Basic SQLite if personal use - BEWARE OF SQL INJECTION

import sqlite3

# first establish a connection
conn = sqlite3.connect('test.db')

# create a table
conn.execute('''CREATE TABLE TEST (ID INT PRIMARY KEY NOT NULL, NAME TEXT NOT NULL, AGE INT NOT NULL, ADDRESS CHAR(50) SALARY REAL);''')

# insert into table
conn.execute("INSERT INTO TEST (ID, NAME, AGE, ADDRESS, SALARY) VALUES (1, 'BEILY', 28, 'MONFY', 1000000);")

# select and retrieve data
cursor = connect.execute("SELECT * FROM TEST WHERE NAME = 'BEILY'")

for row in cursor:

    id = row[0]
    name = row[1]
    age = row[2]
    address = row[3]
    salary = row[4]

# needed to save changes
conn.commit()


# close connection
conn.close()

```

```python

# Advanced SQLite if used for web apps, other. Safe from SQL Injection



import sqlite3
from sqlite3 import Error

# import database - establish connection
def create_connection(db_file):
    """ create a database connection to a SQLite database """
    conn = None
    try:
        conn = sqlite3.connect(db_file)
        print(sqlite3.version)
    except Error as e:
        print(e)
    finally:
        if conn:
            conn.close()


# insert into projects table - notice the ?, safe from sql injection
def create_project(conn, project):
    """
    Create a new project into the projects table
    :param conn:
    :param project:
    :return: project id
    """
    sql = ''' INSERT INTO projects(name,begin_date,end_date)
              VALUES(?,?,?) '''
    cur = conn.cursor()
    cur.execute(sql, project)
    conn.commit()
    return cur.lastrowid

# create task table linked to project
def create_task(conn, task):
    """
    Create a new task
    :param conn:
    :param task:
    :return:
    """

    sql = ''' INSERT INTO tasks(name,priority,status_id,project_id,begin_date,end_date)
              VALUES(?,?,?,?,?,?) '''
    cur = conn.cursor()
    cur.execute(sql, task)
    conn.commit()

    return cur.lastrowid

# update statement on task table
def update_task(conn, task):
    """
    update priority, begin_date, and end date of a task
    :param conn:
    :param task:
    :return: project id
    """
    sql = ''' UPDATE tasks
              SET priority = ? ,
                  begin_date = ? ,
                  end_date = ?
              WHERE id = ?'''
    cur = conn.cursor()
    cur.execute(sql, task)
    conn.commit()


# delete statement on task table
def delete_task(conn, id):
    """
    Delete a task by task id
    :param conn:  Connection to the SQLite database
    :param id: id of the task
    :return:
    """
    sql = 'DELETE FROM tasks WHERE id=?'
    cur = conn.cursor()
    cur.execute(sql, (id,))
    conn.commit()


# select statement 1
def select_all_tasks(conn):
    """
    Query all rows in the tasks table
    :param conn: the Connection object
    :return:
    """
    cur = conn.cursor()
    cur.execute("SELECT * FROM tasks")

    rows = cur.fetchall()

    for row in rows:
        print(row)

# select statement 2
def select_task_by_priority(conn, priority):
    """
    Query tasks by priority
    :param conn: the Connection object
    :param priority:
    :return:
    """
    cur = conn.cursor()
    cur.execute("SELECT * FROM tasks WHERE priority=?", (priority,))

    rows = cur.fetchall()

    for row in rows:
        print(row)

# create two tables
def main():
    database = r"C:\sqlite\db\pythonsqlite.db"

    sql_create_projects_table = """ CREATE TABLE IF NOT EXISTS projects (
                                        id integer PRIMARY KEY,
                                        name text NOT NULL,
                                        begin_date text,
                                        end_date text
                                    ); """

    sql_create_tasks_table = """CREATE TABLE IF NOT EXISTS tasks (
                                    id integer PRIMARY KEY,
                                    name text NOT NULL,
                                    priority integer,
                                    status_id integer NOT NULL,
                                    project_id integer NOT NULL,
                                    begin_date text NOT NULL,
                                    end_date text NOT NULL,
                                    FOREIGN KEY (project_id) REFERENCES projects (id)
                                );"""

    # create a database connection
    conn = create_connection(database)

    # create tables
    if conn is not None:
        # create projects table
        create_table(conn, sql_create_projects_table)

        # create tasks table
        create_table(conn, sql_create_tasks_table)
    else:
        print("Error! cannot create the database connection.")

    with conn:
        # create a new project
        project = ('Cool App with SQLite & Python', '2015-01-01', '2015-01-30');
        project_id = create_project(conn, project)

        # tasks
        task_1 = ('Analyze the requirements of the app', 1, 1, project_id, '2015-01-01', '2015-01-02')
        task_2 = ('Confirm with user about the top requirements', 1, 1, project_id, '2015-01-03', '2015-01-05')

        # create tasks
        create_task(conn, task_1)
        create_task(conn, task_2)
    
        # udpate task
        update_task(conn, (2, '2015-01-04', '2015-01-06', 2))

        # delete task
        delete_task(conn, 2)

        
        print("1. Query task by priority:")
        select_task_by_priority(conn, 1)

        print("2. Query all tasks")
        select_all_tasks(conn)

if __name__ == '__main__':
    main()


```

## Image Processing

### CV2

```python

import cv2

# converts image to grayscale
image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# applies Gaussian Blur
image = cv2.GaussianBlur(img, (9, 9), 0)

# reverses colors on existing image
image = cv2.bitwise_not(image, image)

# find contours
contours = cv2.findContours(image, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

# get rotation necessary from corner array and dimension array
grid = cv2.getPErspectiveTransform(corners, dimensions)

# rotate image based on grid
warped = cv2.warpPerspective(image, grid, (width, height))

# resize an image to 2000 x 2000 pixels
image_large = cv2.resize(image, (2000, 2000))

# write image to filesystem
cv2.imwrite('location/on/filesystem/filename.img', image)

# read image from filesystem
cv2.imread('location/on/filesystem/filename.img')

```

### Pytesseract

```python

import pytesseract

# configuration parameters
xconfigs = '--psm 6 digits -c page_separator='''
# there are various psm modes, used to better identify different content types. 6 is good for single numbers
# page separator null means we will not get a symbol at the end of the string

# switch to --psm 8 digits to better read strings

# simple use for image recognition
string = pytesseract.image_to_string(imageLocationOnDisk, config = xconfig)


```

## Web Data Transfer

### XML

XML stands for eXtensible Markup Language. Before JSON, it was the standard for sending data across the internet.

```xml

<person>  <!-- start of tag -->

  <name>Content of Tag</name> 

  <phone type="emea"> <!-- this is an attribute -->

     +1 734 303 4456

   </phone>

   <!-- self-closing tag -->
   <email hide="yes" /> <!-- another attribute --> 

</person> <!-- end of tag -->


```

The data transfer works from a source dataset, which is *serialized*, then sent through and *deserialized*.

```xml

<!-- XML can be read as a path, as in a directory -->

<a>
  <b>X</b>
  <c>
    <d>Y</d>
    <e>Z</e>
  </c>
</a>  

<!--
    
    a/b
    a/c/d
    a/c/e
    
>

```

An XML Schema is a specification for how an XML should be built. You typically send an XML schema and a document to a validator and it will tell you if it is valid.

```xml

<!-- schema -->
<xs:complexType name=”person”>

  <xs:sequence>

    <xs:element name="lastname" type="xs:string"/>

    <xs:element name="age" type="xs:integer"/>

    <xs:element name="dateborn" type="xs:date"/>

   </xs:sequence>

</xs:complexType>

<!-- document -->
<person>

   <lastname>Severance</lastname>

   <age>17</age>

   <dateborn>2001-04-17</dateborn>

</person>

<!-- XSD is one of the more popular XML schema formats -->

<!-- XSD sample constraints -->
<xs:element name="person">

  <xs:complexType>

    <xs:sequence>

      <xs:element name="full_name" type="xs:string"  

          minOccurs="1" maxOccurs="1" /> <!-- there can only be one -->

      <xs:element name="child_name" type="xs:string" 

            minOccurs="0" maxOccurs="10" /> <!-- any number from 0 to 10 -->

    </xs:sequence>

  </xs:complexType>

</xs:element>

<!-- XSD datatypes -->
<xs:element name="customer" type="xs:string"/>

<xs:element name="start" type="xs:date"/>

<xs:element name="startdate" type="xs:dateTime"/>

<xs:element name="prize" type="xs:decimal"/>

<xs:element name="weeks" type="xs:integer"/>


```

How to read XML from Python:

```python

import xml.etree.ElementTree as ET

input = '''<stuff>

    <users>

        <user x="2">

            <id>001</id>

            <name>Chuck</name>

        </user>

        <user x="7">

            <id>009</id>

            <name>Brent</name>

        </user>

    </users>

</stuff>'''



stuff = ET.fromstring(input)

lst = stuff.findall('users/user')

print('User count:', len(lst))

for item in lst:

    print('Name', item.find('name').text)

    print('Id', item.find('id').text)

    print('Attribute', item.get("x"))


```

### JSON

JSON stands for JavaScript Object Notation. It is perhaps the most common way to format and share data across the internet.

JSON looks like a python dictionary, or a javascript object. Almost any language uses this format in some way or another.

```python

import json

input = '''[

  { "id" : "001",
    "x" : "2",
    "name" : "Chuck"
  },
  { "id" : "009",
    "x" : "7",
    "name" : "Chuck"
  }
]'''


info = json.loads(input)

print('User count:', len(info))

for item in info:

    print('Name', item['name'])
    print('Id', item['id'])
    print('Attribute', item['x'])


```

Using JSON to communicate is quite common in today's service-oriented world, where we leverage multiple APIs (Application Program Interfaces).

### APIs

Application Program Interfaces are ways in which clients can communicate to servers, typically by sending a piece of code, and receive a response in terms of data.

API Status Codes:

- 200: OK
- 301: Redirected
- 400: Bad Request
- 401: Not Authenticated
- 403: Forbidden
- 404: Not Found
- 503: Server cannot handle

How to call APIs in Python.

```python

import requests
import json

response = requests.get("https://api.open-notify.org/this-api-doesnt-exist")


print(response.status_code)
print(response.json())

obj = response.json()

# prints out the JSON as a string of text, sorted keys and indentation of 4 spaces
text = json.dumps(obj, sort_keys = True, indent = 4)

# loads the json into a python dictionary
dictionary = json.loads(obj)

```

APIs have "endpoints", which are links that we can "GET". To properly format an API request, we must read the documentation.

```python

# send API request with parameters

parameters = {
    "one": 40.71,
    "two": -74
}

response = requests.get('https://api-endpoint.com', params = parameters)

```
