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

```python

titles = new Dict()

# the sorted function accepts a custom sorting algo
# the lambda function is a nemeless function, you just specify input/output
# in this case we are sorting, in reverse order, based on the value and not the key of the dict
sorted(title, key=lambda title: titles[title]), reverse = True)

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
