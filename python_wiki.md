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

# this works even if your file is not called "main.py"
if __name__ == '__main__'

    # please note the if condition remains the same, but the code block to be executed does not need to be "main"
    main()

```

Functions can also take default values for arguments.

```python

def sum_stuff(a, b, c = 5):

    return (a + b + c)

```

### Variable Operations

```python

# swapping variables is easy
a = 1
b = 2

a, b = b, a

0 # False
False # False


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

With higher-order functions we can use the "nonlocal" statement.

```python

def make_withdraw(balance):
    """Return a withdraw function that draws down balance with each call."""
    def withdraw(amount):
        nonlocal balance                 # Declare the name "balance" nonlocal. It can reference to the balance above
        if amount > balance:
            return 'Insufficient funds'
        balance = balance - amount       # Re-bind the existing balance name. Only work thanks to nonlocal statement
        return balance
    return withdraw

```

## Copy and Deepcopy

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

## Files

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

## Lambda Function

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

## Containers

### Mutability

- Lists, Dictionaries are mutable
- Strings, Tuples are immutable

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

# combining lists into other lists
s = [1, 2, 3]
t = [4, 5, 6]

new = [[s[i], t[i]] for i in range(0, len(s))]

# manipulating existing lists with list comprehensions
# this below is a way to perform a riffle shuffle on a list
deck = range(20)

riffled = [deck[i // 2] if i % 2 == 0 else deck[i//2 + len(deck)//2] for i in range(0, len(deck))] 


# two layer list comprehension - assume you want to subtract i from i - 1 in a list of lists. You can do it with list comprehension.
# input  - [[75, 81, 84, 90, 92], [19, 29, 35, 36, 38]]
# output - [[6, 3, 6, 2], [10, 6, 1, 2]]


times = [[times_per_player[i][j] - times_per_player[i][j - 1] \
         for j in range(1, len(times_per_player[i]))] \
         for i in range(len(times_per_player))]


```

### Slicing

```python

# list slicing means grabbing items from original list and returning them in a new list


# there are three arguments to list slicing [start=0:end=0:step=1]

list1 = [1, 2, 3, 4]

list2 = list1[:2] # grabs [1, 2, 3]
list3 = list1[1:2] # grabs [2, 3]
list4 = list1[1:] # grabs [2, 3, 4]

# slicing notation works the same as ranges. In fact, it is equivalent to:
list2 = [list1[i] for i in range(2)]

# How to grab the last element of a list
lst = [0, 1, 2, 3, 4, 5, 6]
lst[-1] # grabs the last element! 6
lst[-2] # grabs the semi-last! 5


[::-1]   # Make a reversed copy of the entire list
[6, 5, 4, 3, 2, 1, 0]
>>> lst[::2]  # Skip every other; step size defaults to 1 otherwise
[0, 2, 4, 6]

```

Slicing also works on strings.

### List Methods

```python

"""" General
- 'append': adds element to end of list
- 'clear': removes all elements from list
- 'copy': returns a copy of list
- 'count': counts elements with certain value
- 'extend': adds elements of a list (or iterable) to end of current list 
- 'index': returns the index of element with certain value
- 'insert': inserts element in specific position
- 'pop': removes a specific element
- 'remove': removes first element with certain value
- 'reverse': inverts order of list
- 'sort': re-orders the list according to key function

"""

# Detail

# append(list)

a = ["apple", "banana", "cherry"]
b = ["Ford", "BMW", "Volvo"]
a.append(b)


# clear()

fruits = ['apple', 'banana', 'cherry', 'orange']

fruits.clear()


# copy()

fruits = ['apple', 'banana', 'cherry', 'orange']

x = fruits.copy()


# extend(iterable)

fruits = ['apple', 'banana', 'cherry']

points = (1, 4, 5, 9)

fruits.extend(points)


# index('item')

fruits = ['apple', 'banana', 'cherry']

x = fruits.index("cherry")


# insert(where, what)
fruits = ['apple', 'banana', 'cherry']

fruits.insert(1, "orange")


# pop(where)

fruits = ['apple', 'banana', 'cherry']

fruits.pop(1)


# remove(what)

fruits = ['apple', 'banana', 'cherry']

fruits.remove("banana")


# reverse()

fruits.reverse()


# sort()

# A function that returns the length of the value:
def myFunc(e):
  return len(e)

cars = ['Ford', 'Mitsubishi', 'BMW', 'VW']

cars.sort(reverse=True,key=myFunc) # sorts from longest to shortest


```

Below is a list of other common functions that support lists.

```python

sum([1, 2, 3]) # 6
max(range(10)) # 9

min(range(10)) # 0
# the all function returns a bool. It is True if all the values are true as well
all(x < 5 for x in range(5)) # True
all(x < 1 for x in range(5)) # False

# the complement of all is any
any(x < 1 for x in range(5)) # True because at least one is True



```

### String Methods

```python

# Strings are immutable- when you modify a string it returns a new string back

""" There are a trillion string methods. Here is the full list


capitalize()    -     Converts the first character to upper case
casefold()    -     Converts string into lower case
center()    -     Returns a centered string
count()    -     Returns the number of times a specified value occurs in a string
encode()    -     Returns an encoded version of the string
endswith()    -     Returns true if the string ends with the specified value
expandtabs()    -     Sets the tab size of the string
find()    -     Searches the string for a specified value and returns the position of where it was found
format()    -     Formats specified values in a string
format_map()    -     Formats specified values in a string
index()    -     Searches the string for a specified value and returns the position of where it was found
isalnum()    -     Returns True if all characters in the string are alphanumeric
isalpha()    -     Returns True if all characters in the string are in the alphabet
isdecimal()    -     Returns True if all characters in the string are decimals
isdigit()    -     Returns True if all characters in the string are digits
isidentifier()    -     Returns True if the string is an identifier
islower()    -     Returns True if all characters in the string are lower case
isnumeric()    -     Returns True if all characters in the string are numeric
isprintable()    -     Returns True if all characters in the string are printable
isspace()    -     Returns True if all characters in the string are whitespaces
istitle()    -     Returns True if the string follows the rules of a title
isupper()    -     Returns True if all characters in the string are upper case
join()    -     Joins the elements of an iterable to the end of the string
ljust()    -     Returns a left justified version of the string
lower()    -     Converts a string into lower case
lstrip()    -     Returns a left trim version of the string
maketrans()    -     Returns a translation table to be used in translations
partition()    -     Returns a tuple where the string is parted into three parts
replace()    -     Returns a string where a specified value is replaced with a specified value
rfind()    -     Searches the string for a specified value and returns the last position of where it was found
rindex()    -     Searches the string for a specified value and returns the last position of where it was found
rjust()    -     Returns a right justified version of the string
rpartition()    -     Returns a tuple where the string is parted into three parts
rsplit()    -     Splits the string at the specified separator, and returns a list
rstrip()    -     Returns a right trim version of the string
split()    -     Splits the string at the specified separator, and returns a list
splitlines()    -     Splits the string at line breaks and returns a list
startswith()    -     Returns true if the string starts with the specified value
strip()    -     Returns a trimmed version of the string
swapcase()    -     Swaps cases, lower case becomes upper case and vice versa
title()    -     Converts the first character of each word to upper case
translate()    -     Returns a translated string
upper()    -     Converts a string into upper case
zfill()    -     Fills the string with a specified number of 0 values at the beginning

"""

# some examples
string = "hello how are you"

"hello" in string
# this is True

new_string = string.replace("hello", "hello guys")

string.endswith("you")
# this is True

string = 'Hey, how are you?'

string.split(',') # default is to split by space

s1, s2, s3 = '1','2','3'

':'.join(s1, s2, s3) # '1:2:3'


s = 'hi '
s2 = s + 'hello' # 'hi hello"

s3 = 'hey' * 3 # "heyheyhey"


s = 'hey how are You'
s.title() # 'Hey How Are You'

s.swapcase() # HEY HOW ARE yOU

s = ' hey how are you '

s.lstrip() # 'hey how are you '
s.rstrip() # ' hey how are you'



```

### Dictionaries

Dictionaries represent key/value pairs. Only immutable datatypes can be used as keys (i.e a string, a tuple, ...)

```python

numerals = {
    'I': 1,
    'V': 5,
    'X': 10
}

# you look-up by key
numerals['X'] # 10

# re-assign values
numerals['X'] = 12

list(numerals) # ['I', 'V', 'X']

# returns a sequence that is iterable, but it is not a list
numerals.values() # dict_values([1, 5, 10])

# this returns a list
list(numerals.values())


# Add a key into a dictionary while using a loop, if it doesn't exist - shorthand

dict[item] = dict.get(item, 0) + 1 # this will either retrieve the current count and increment it, or initialize it at 0 and set it to 1

```

### Dictionary Comprehension

Work similarly to list comprehension, but the syntax must be adjusted.

```python

dict_comp = { x * x: x for x in [1, 2, 3, 4, 5] if x > 2}

dict_comp # {9: 3, 16: 4, 25: 5}


```

### Dictionary Methods

```python

"""

clear() - Removes all the elements from the dictionary
copy() - Returns a copy of the dictionary
fromkeys() - Returns a dictionary with the specified keys and value
get() - Returns the value of the specified key
items() - Returns a list containing a tuple for each key value pair
keys() - Returns a list containing the dictionary's keys
pop() - Removes the element with the specified key
popitem() - Removes the last inserted key-value pair
setdefault() - Returns the value of the specified key. If the key does not exist: insert the key, with the specified value
update() - Updates the dictionary with the specified key-value pairs
values() - Returns a list of all the values in the dictionary
add() - Adds key, value pair to dictionary

"""


dict.get(item, fallback)

# if you don't provide defaultvalue this will Error if it can't find the key
dict.pop(key, defaultvalue)


```

### Tuples

Tuples are an immutable data type in python.

```python

tup = (10, 20)

# empty typle
empty = ()

# one element - weird syntax
one = (10, )



```

## Loading Configuration Files

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

## Threading

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

## Coloring Console Output

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

## Web Scraping - BeautifulSoup

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

## Regular Expressions

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

## Objects

### Classes Introduction

Classes in python, and other programming languages, are blueprints. Python is an object-oriented programming language, meaning that even the most primitive data types we use are actually classes.

When you initialize a list, for example:

```python

my_list = [1, 2, 3]

# this is a "list" class
type(my_list)

# this will enumerate all the "methods" associated to this class
dir(my_list)
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

### Inheritance

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
        self.sides = [float(input("Enter side " + str(i+1)+" : ")) for i in range(self.n)]

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


class Square(Polygon):
    def __init__(self):
        # this method can be used to access the parent class method, it is much cleaner than above imo
        super().__init__(no_of_sides = 4)

```

Please note that the Triangle Class and the Polygon Class both have an __init__ method. When calling the triangle class, its __init__ takes precedence.

### Multiple Inheritance

Let us explore a more complex example to understand how multiple inheritance works. We will model bank accounts.

```python

class Account:
    """An account has a balance and a holder.
    All accounts share a common interest rate.
    """

    interest = 0.02  # A class attribute

    def __init__(self, account_holder):
        self.holder = account_holder
        self.balance = 0

    def deposit(self, amount):
        """Add amount to balance."""
        self.balance = self.balance + amount
        return self.balance

    def withdraw(self, amount):
        """Subtract amount from balance if funds are available."""
        if amount > self.balance:
            return 'Insufficient funds'
        self.balance = self.balance - amount
        return self.balance

# this shows how inheritance works, we just modify the withdraw method, but it is good practice to re-use code instead of hard-coding

# example of inheritance - checking accounts ARE accounts
class CheckingAccount(Account):
    """A bank account that charges for withdrawals.

    >>> ch = CheckingAccount('Jack')
    >>> ch.balance = 20
    >>> ch.withdraw(5)
    14
    >>> ch.interest
    0.01
    """

    withdraw_fee = 1
    interest = 0.01

    def withdraw(self, amount):
        return Account.withdraw(self, amount + self.withdraw_fee)
        # Alternatively:
        return super().withdraw(amount + self.withdraw_fee)


# in this example we use a class to create other instances of other classes.

# example of composition - a bank HAS accounts
class Bank:
    """A bank has accounts and pays interest.

    >>> bank = Bank()
    >>> john = bank.open_account('John', 10)
    >>> jack = bank.open_account('Jack', 5, CheckingAccount)
    >>> jack.interest
    0.01
    >>> john.interest = 0.06
    >>> bank.pay_interest()
    >>> john.balance
    10.6
    >>> jack.balance
    5.05
    """
    def __init__(self):
        self.accounts = []

    def open_account(self, holder, amount, account_type=Account):
        """Open an account_type for holder and deposit amount."""
        account = account_type(holder)
        account.deposit(amount)
        self.accounts.append(account)
        return account

    def pay_interest(self):
        """Pay interest to all accounts."""
        for account in self.accounts:
            account.deposit(account.balance * account.interest)


# same inheritance as above - different example
class SavingsAccount(Account):
    deposit_fee = 2
    def deposit(self, amount):
        return Account.deposit(self, amount - self.deposit_fee)

# multiple inheritance

# what exactly happens here:
# special withdraw behavior is inherited from CheckingAccount
# special deposit behavior is inherited from SavingsAccount
# the rest is inherited from Account - which is just the interest
class BestAccount(CheckingAccount, SavingsAccount):
    def __init__(self, account_holder):
        self.holder = account_holder
        self.balance = 1
     
```

### Magic Methods

Objects and classes have a list of standard methods that work well with python features. One of these is the __init__ method, that initializes an instance of a class during construction. There are many such methods and below we list them out.

```python

class Sudoku:


    # this method gets called first, and returns an object that is then passed in the __init__ method
    def __new__(cls):
        print ("__new__ magic method is called")
        inst = object.__new__(cls)
                return inst

    # the init method gets automatically called when you run something like ; me = Sudoku(9, 3)
    def __init__(self, row_len, box_size):
        self.name = "Sudoku Puzzle"
        self.row_length = row_len
        self.col_length = row_len # sudokus must be square
        self.box_size = box_size
        self.num_cells = row_len * row_len 
        # these 4 variables will be called by me.box_size, etc. 

    # the str method overrides the __repr__ method, which is called by default
    def __str__(self):
        return "This is a " + self.name

    # this method is used for Python's interpretation. Can be anything for custom classes
    def __repr__(self):
        return self.name
    
    def __add__(self, x):
        # method used to add two values if it makes sense

    def __del__(self):
        # destructor method - caled when you delete object


```

### Trees - Class

See section "Tree - Data Abstraction" for comparison. Here we implement the same tree but using Python Objects. Personally I believe this is cleaner, but to each their own.

```python

class Tree:
    """A tree is a label and a list of branches."""
    def __init__(self, label, branches=[]):
        self.label = label
        for branch in branches:
            assert isinstance(branch, Tree)
        self.branches = list(branches)

    def __repr__(self):
        if self.branches:
            branch_str = ', ' + repr(self.branches)
        else:
            branch_str = ''
        return 'Tree({0}{1})'.format(repr(self.label), branch_str)

    # this method calls the indented function to return a "pretty" tree representation
    def __str__(self):
        return '\n'.join(self.indented())

    def indented(self):
        lines = []
        for b in self.branches:
            for line in b.indented():
                lines.append('  ' + line)
        return [str(self.label)] + lines

    def is_leaf(self):
        return not self.branches


def fib_tree(n):
    """A Fibonacci tree.

    >>> print(fib_tree(4))
    3
      1
        0
        1
      2
        1
        1
          0
          1
    """
    if n == 0 or n == 1:
        return Tree(n)
    else:
        left = fib_tree(n-2)
        right = fib_tree(n-1)
        fib_n = left.label + right.label
        return Tree(fib_n, [left, right])


def leaves(tree):
    """Return the leaf values of a tree.

    >>> leaves(fib_tree(4))
    [0, 1, 1, 0, 1]
    """
    if tree.is_leaf():
        return [tree.label]
    else:
        return sum([leaves(b) for b in tree.branches], [])


def height(tree):
    """The height of a tree."""
    if tree.is_leaf():
        return 0
    else:
        return 1 + max([height(b) for b in tree.branches])


def prune(t, n):
    """Prune sub-trees whose label value is n.

    >>> t = fib_tree(5)
    >>> prune(t, 1)
    >>> print(t)
    5
      2
      3
        2
    """
    t.branches = [b for b in t.branches if b.label != n]
    for b in t.branches:
        prune(b, n)


```

## Docstring and Assert

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

# tests a single function - second argument always fixed, this is to "verbose"
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

## Quine (Python)

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

## Short Circuit

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

## Higher Order Functions

A powerful means of abstration is when we use a function to manipulate other functions.

### Abstraction

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

### Nested Functions

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

### Decorators

Decorators are a way to run higher-order functions in short-hand notation. A common use-case for this is a trace.

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

### Dynamic Function Behavior

Another benefit of higher-order functions becomes apparent when we would like to always call the same function but have it's behavior change over time. We can code this as a function that returns itself.

```python

# self-returning function - keeps track of what you have done before
def higher_lower(i, j):

    def say(i, j):
        
        if i > j:
            print(f'{i} is greater than {j}')

        if i < j:
            print(f'{i} is smaller than {j}')

        else:
            print('The two numbers are equal')
    
    return say


```

Running the following in the python shell will lead to two different results!

```python

>>> case1 = higher_lower(1,2)
>>> case1(1,2)
1 is smaller than 2
>>> case2 = higher_lower(2,1)
>>> case2(2,1)
2 is greater than 1 
```

Let us look at another example.

```python

def announce_lead_changes(last_leader=None):
    """Return a commentary function that announces lead changes.

    >>> f0 = announce_lead_changes()
    >>> f1 = f0(5, 0)
    Player 0 takes the lead by 5
    >>> f2 = f1(5, 12)
    Player 1 takes the lead by 7
    >>> f3 = f2(8, 12)
    >>> f4 = f3(8, 13)
    >>> f5 = f4(15, 13)
    Player 0 takes the lead by 2
    """

    def say(score0, score1):
        if score0 > score1:
            leader = 0
        elif score1 > score0:
            leader = 1
        else:
            leader = None
        if leader != None and leader != last_leader:
            print('Player', leader, 'takes the lead by', abs(score0 - score1))
        return announce_lead_changes(leader)
    return say

```

In this example we define announce_lead_change, which itself defines and also returns a different function.

```python

# when we first call the function, the last_leader=None and f0 now stores the say function
>>> f0 = announce_lead_changes()

# I call the say function, last_leader=None but leader=0, so it prints the output.
# At the same time, it redefines annouce_lead_changes with last_leader=0, which in turn returns say again.
>>> f1 = f0(5, 0)
Player 0 takes the lead by 5

# this is how you can dynamically change a function behavior based on past behavior


```

## Dynamic Variable Names

If we need to construct dynamic variable names, we can leverage the following.

```python

player0 = 5
player1 = 10
# assume you want to find a list of players
for i in range(2):

    # this will return player0, and then player1 
    eval('player' + i)

```

## Recursion

A recursive function is a function that calls itself. There are many ways to think about recursion, here I will outline the method that works best for me.

A problem can be handled by recursion if it is possible to break down the problem in smaller pieces, until we arrive at a very simple case that we can check for.

- Base Case: This is the smallest sub problem which we can check for
- Recursive Case: This is the actual recursion, the act of breaking down the problem in smaller pieces
- Condition: A check to see if the base case has occurred

### Standard Recursion

Let us consider an example.

```python

# One problem that can be handled with recursion is the sum of integers from 1 to n.
# The nice thing about recursion is that you don't need to know how to solve the whole problem, just a very small part of it
def sum_ints_recursion(n):

    # step 2 - how to construct the base case? Even if we don't know how to sum integers, we definitely know that the
    # sum of 1 is just 1. We construct the base case like this.
    if n == 1:
        return n # you can also return 1 it is the same
    
    # step 3 - now we have a base case of 1, we just need to make sure our recursive case "gets us to 1 at some point"
    else:
        # step 1 - how do I sum the numbers from 1 to n? Well, I can break the problem up by saying
        # sum of 1 to n --> n + sum(1 to (n - 1))
        # How to validate recursion - "leap of faith". Assume sum_ints_recursion(n - 1) is CORRECT, do you get the right answer?
        # n + sum(1 to (n - 1)) = sum of 1 to n. Yes. 
        return n + sum_ints_recursion(n - 1)

sum_ints_recursion(3): # -> returns n + sum_ints_recursion(2)
# sum_ints_recursion(2) -> returns n + sum_ints recursion(1)
# sum_ints_recursion(1) -> base case = 1

```

The best way to understand recursion is to actually draw it out. By doing so we will see that recursion is like peeling and unpeeling an onion - you start from a function call, climb all the way down to the most nested case, find the base case, and then start rapidly returning functions until you are back to your original call.

Visualizing the example above, we have the following:

```python

    sum_ints_recursion(3) 
    _______|_______
    |             |
    n = 3  + sum_ints_recursion(2)
                _______|_______
                |             |
                n = 2  + sum_ints_recursion(1)
                                |
                            Base Case -> n = 1

# Step 0: Call f(3)
    # Step 1: Call f(2)
        # Step 2: Call f(1)
            # Step 3: Base case, f(1) is 1
        # Step 4: Return f(1) = 1
    # Step 5: Return f(2) = 2 + f(1) = 2 + 1 = 3
# Step 6: Return f(3) = 3 + f(2) = 3 + 3 = 6


```

### Recursion with Higher Order Functions

Recursion is so hard to understand because it effectively evaluates your problem in reverse. The function calls stop when we hit a base case, so we are not really "summing up the numbers from 1 to n", we are "summing up the numbers from n to 1".

We are not evaluating 1 + 2 + 3 + 4 + 5, but we are evaluating 5 + 4 + 3 + 2 + 1.

This is fine for many recursive functions, but what if we need to "sum the numbers from 1 to n, but ignore any number higher than 3"?

Our approach will not work, let us use the same implementation to prove why:

```python

# please let us ignore that we can set n = 3 and ignore all the rest - this is just an explanation
def sum_upto_three_wrong(n):

    # we change our base case to look for 3 and start returning
    if n == 3:
        return n
    
    else:

        return n + sum_upto_three_wrong(n - 1)

sum_upto_three_wrong(4) # what should the answer be? 1 + 2 + 3 = 6 (we stop at 3)

# the problem is this is evaluated in reverse.
# f(4) = 4 + f(3)
# f(3) = 3! We hit the base case
# f(4) = 4 + 3 = 7

```

In order to solve this, we must be able to traverse the numbers in the "correct order"- i.e. from 1 to n. How do we achieve this?
We can leverage higher-order functions.

```python

def sum_upto_three(n):

    def sum_in_ascending_order(n):
         if n == 3:
            return n
    
        else:

            return n + sum_in_ascending_order(n + 1)

    return sum_in_ascending_order(1)

# sum_upto_three(4) returns a sum_in_ascending_order(1)
# sum_in_ascending_order(1) --> 1 + sum_in_ascending_order(2)
# sum_in_ascending_order(2) --> 2 + sum_in_ascending_order(3)
# sum_in_ascending_order(3) --> 3
# 3 + 2 + 1 = 6

```

Using helper, nested and higher-order functions is not only useful when you want to traverse in a specific order, but also when we require some additional variables to "keep track of", in addition to the arguments of the main function.
Another more involved example of this type of recursion is the pingpong algorithm.

```python

def pingpong(n):
    """Return the nth element of the ping-pong sequence.
    The ping-pong sequence starts counting up from 1, and reverses the direction every time it finds an 8, multiple of 8, or number ending in 8.

    >>> pingpong(8)
    8
    >>> pingpong(10)
    6
    >>> pingpong(15)
    1
    >>> pingpong(21)
    -1
    >>> pingpong(22)
    -2
    >>> pingpong(30)
    -2
    """

    # step 2 - why do we need a helper? Because we need to keep track of the index, the current score, and the direction we are going
    def helper(i, x, step):
    
        # when we are done counting we return the result
        if i == n:
            return x 
        
        # step 3 - every time we call the function, we increase the index, we either add or substract x, and the step itself.
        # The counting occurs here when we do x + step / x + (- step)
        return helper(i + 1, x + next_dir(step, i), next_dir(step, i))

    # step 1 - we use nested functions because we initialize the helper with 1, we "seed it"    
    return helper(1, 1, 1)


# step 3.1 - we abstract the check for eights, assume the below works.
def next_dir(step, i):

    if i % 8 == 0 or num_eights(i) > 0:
        return -step

    return step

def num_eights(i):
    return number_of_eights

```

### Mutual Recursion

Mutual recursion occurs when two functions call each other recursively. There is nothing different compared to this type of recursion, just that we are using two functions. The base case can either live in both functions, or only one.

```python

# let's assume that we want to find out if a number is odd or even. Let's also ignore that n % 2 gives us that answer.
# We can say that an odd number is the same as even plus one, and the same goes for even. Our base case is that 0 is even.

# outer function asks if n is even
def is_even(n):
    
    # base case
    if n == 0:
        return True
    else:
        # calls another function with lower input
        return is_odd(n-1)

    def is_odd(n):
    
    # base case also here
    if n == 0:
        return False
    else:
        # calls back the original function
        return is_even(n-1)

    # True
    result = is_even(4)

```

### Tree Recursion

Tree recursion is a special type of recursion, which could involve either a simple case or a higher order function, in which we must evaluate two different options to reach our result. Each one of our options breaks down the problem further.

```python


def count_coins(change):
    """Return the number of ways to make change using coins of value of 1, 5, 10, 25.
    >>> count_coins(15)
    6
    >>> count_coins(10)
    4
    >>> count_coins(20)
    9
    >>> count_coins(100) # How many ways to make change for a dollar?
    242
    """

    def helper(change, coin):
        
        # step 3 - as we decrease the coins, at some point the change will be 0.
        # how many times can you split 0 with 1? one time.
        if change == 0:
            return 1
        
        # step 4 - coin is None if we have called descending_coin(1), we have finished cycling coins.
        # how many times can I split 5 with 0 ? well 0 times.
        elif coin == None:
            return 0

        else:

            if coin > change:
                coin = descending_coin(coin)
            
            # step 2 - we build a tree. Assume n = 30 for the example. 
            # How do we count the number of times to split 30 with all coins up to 25?
            # in one scenario, we assume we use 25, and ask - how we count the times to split 5 with all coins up to 25
            # in the other, we do not use 25, and as - how do we count the times to split 30 with coins up to 10
            with_largest = helper(change - coin, coin)
            without_largest = helper(change, descending_coin(coin)) # descending coin gives 25 -> 10, 10 -> 5, ... 

            return with_largest + without_largest

    # step 1 - we seed the helper function by using a coin of 25, the largest
    return helper(change, 25)

# simple function that returns the smaller coin compared to the one passed in
def descending_coin(coin):
    """Returns the next descending coin in order.
    >>> descending_coin(25)
    10
    >>> descending_coin(10)
    5
    >>> descending_coin(5)
    1
    >>> descending_coin(2) # Other values return None
    """
    if coin == 25:
        return 10
    elif coin == 10:
        return 5
    elif coin == 5:
        return 1

```

## Key Functions

Certain functions such as sort, max, etc. have a default way of operating. However, this can typically be overridden by providing a key.

```python

# how do I find the highest value in a parabola of x?
max(range(10), key = lambda x: 7 - (x - 4)*(x - 2)) # 3

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

## File Formats

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

### Yaml

YAML stands for "YAML Ain't MArkup Language" and is another popular data serialization file format. It is commonly used for configuration files. Below we explore various features of the language

```yaml

# three dashes indicate start of file - required
---

# key is always a string - value can be anything. String go without quotes
hi: how are you

# integer
foo: 12345
# hex
bar: 0x12d4
# octal
plop: 023332
# float
foo: 1230.15
# scientific
bar:  12.3015e+05

# infinity and NaNs
foo: .inf
bar: -.Inf
plop: .NAN


# can use double quotes for strings if we want newlines
foo: "this is not a normal string\n"


# nulls
foo: ~
bar: null

# All possible boolean values
foo: True
bar: False
light: On
TV: Off
good: Yes
bad: No

# containers
items: [ 1, 2, 3, 4, 5 ]
names: [ "one", "two", "three", "four" ]

# can also be represented as follows
items:
  - 1
  - 2
  - 3
  - 4
  - 5

# complex structures are supported
items:
  - things:
      thing1: huey
      things2: dewey
      thing3: louie
  - other things:
      key: value


```

## Data Abstraction

Just like we can use functions to abstract ideas, below we show a powerful method to build complex programs by manipulating data.
When we implement a complex function, we can call auxilliary functions to perform our calculations and we do not need to know how these are implemented.

In the same way, we can deal with complex data types (not the classes that are pre-defined in python) without knowing exactly how these are implemented. 

This creates some barriers in our code, where we are programming at different levels. This is extremely helpful when maintaining and updating code.

### Rational Numbers

```python

# the example chosen below is the one of rational numbers, or fractions. 

# One layer of data abstraction is to define the concept of rational, numerator, denominator.
# If we assume that these concepts exist, we can program operations with rationals without knowing their implementation details.


# Abstraction Level - Operations with Rationals
#----------------------------------------------------------#


# these operations are valid irrespective of how the functions are implemneted. This also means I can change how rational is calculated, and it will not affect the below.
def add_rationals(x, y):
    nx, dx = numer(x), denom(x)
    ny, dy = numer(y), denom(y)
    return rational(nx * dy + ny * dx, dx * dy)

def mul_rationals(x, y):
    return rational(numer(x) * numer(y), denom(x) * denom(y))

def print_rational(x):
    print(numer(x), '/', denom(x))

def rationals_are_equal(x, y):
    return numer(x) * denom(y) == numer(y) * denom(x)


# Abstraction Level - Defining Rationals
#----------------------------------------------------------#

def rational(n, d):
    return [n, d]

def numer(x):
    return x[0]

def denom(x):
    return x[1]


# Abstraction Level - Bonus - Defining Pairs
#----------------------------------------------------------#


# above we assume that there exists a concept of list such that [n, d] gives us the representation of rational.
# it doesn't have to be this way. We can abstract even the lowest details.


# a pair is just a function that, given x and y, can return either of those values.
def pair(x, y):
    """Return a function that represents a pair."""
    def get(index):
        if index == 0:
            return x
        elif index == 1:
            return y
    return get


# the select function can then easily return pair(i), where i is either 0 or 1
def select(p, i):
    """Return the element at index i of pair p."""
    return p(i)


```

### Trees - Data Abstraction

Typically when you are dealing with a complex data structure it is a good idea to implement it as an abstract data type. It is easier for scalability and maintainablity. Here we discuss implementing trees in such a way.

A tree has a root node (or label) and is composed of one or more branches. Each branch can be a tree itself, until we reach a node that has no "children" and we call that a leaf.

```python

# Abstraction - a tree is a list of labels and branches. How we implement these is part of the abstraction.

# I can define a tree as follows:
my_tree = tree(3, [tree(1),
                     tree(2, [tree(1),
                              tree(1)])])

# We use the tree "constructor" to build the tree, without specifying how it is built. The tree function will take care of that

def tree(label, branches=[]):
    # for each branch we make sure it is a tree
    for branch in branches:
        assert is_tree(branch)
    
    return [label] + list(branches) # return a list of branches, in case we don't implement tree as a list of lists anymore 

# selectors
def label(tree):
    return tree[0]

def branches(tree):
    return tree[1:]

# validity check
def is_tree(tree):

    # check the structure of tree
    if type(tree) != list or len(tree) < 1:
        return False

    # check that each branch is a tree itself
    for branch in branches(tree):
        if not is_tree(branch):
            return False
    return True

def is_leaf(tree):

    # if it is the last level we call it a leaf
    return not branches(tree)


```

How do we recursively build a tree without specifying it one by one? Example on Fibonacci sequence:

```python

def fib_tree(n):

    if n <= 1: 
        return tree(n)
    
    else:
        left, right = fib_tree(n - 1), fib_tree(n - 2)
`
    return tree(label(left) + label(right), [left, right])
    

```

Other functions that we can implement on top of this data abstraction.

```python

# this function creates a list of all the leaves it finds. summing it together counts the number of leaves
def count_leaves(tree):

    if is_leaf(tree):
        return 1
    
    else:
        return sum([count_leaves(b) for b in branches(tree)])


# this function goes through the tree and prints all the branches and leaves with indentation 
def print_tree(tree, indent = 0):

    print(' ' * indent + str(label(tree)))

    for b in branches:
        print_tree(b, indent + 1)
    


```

## Iteration

Iterators are ways to loop a list of values "lazily", meaning the computation only occurs when it is needed.

A range also computes values lazily, if we set range(10, 100000), it does not compute all the values immediately, but only once you start calling it.

Dictionaries, strings, list, tuples and sets are all iterable items.

```python

lst = [1, 2, 3, 4]

# creates iterator object
iterator = iter(lst)

next(iterator) # 1
next(iterator) # 2 
next(iterator) # 3
next(iterator) # 4
next(iterator) # Traceback: StopIteration

# once you finish looping you cannot go back, but the iterator keeps track of exactly where you are

# one typical way to handle iterators is the following

try:
    next(iterator)

except StopIteration:
    print("Iteration ended")

# you can call iter on an iterator, but it will bind it's name to the same object
f = iter(iterator)
f is iterator # True

# Some functions that return iterators:

range()
map()
filter()
zip()
reversed()

```

Bonus - how does a for loop actually work? It returns the iterator method of the iterable item and loops over it!

```python

counts = [1, 2, 3]

for count in counts:
    print(count)

# what is actually happening in here is the following:

items = counts.__iter__() # calls the iter method and bind it to items
try:
    while True:
        count = items.__next__() # keeps calling next
        print(count)
except StopIteration: # until we reach the end
    pass

```

A generator is a function that instead of *returning* values it *yields* them.
It returns a generator itself, which is a special type of iterator. This means we can loop through a generator function.

```python

def letters_generator():
    current = 'a'
    while current <= 'd':
        yield current
        current = chr(ord(current)+1)

for letter in letters_generator():
    print(letter)


# prints:
# a
# b
# c
# d


# generator can also be called recursively

def countdown(k):
    if k > 0:
        yield k

        # now this is both a recursion and a "yield from".
        # generator functions are themselves iterable, this keeps yielding every number from k downwards. 
        yield from countdown(k -1) 

    else:
        yield('Iteration complete.') 

# more complex example - get the permutations of a sequence

def gen_perms(seq):
    """Generates all permutations of the given sequence. Each permutation is a
    list of the elements in SEQ in a different order. The permutations may be
    yielded in any order.

    >>> perms = gen_perms([100])
    >>> type(perms)
    <class 'generator'>
    >>> next(perms)
    [100]
    >>> try: #this piece of code prints "No more permutations!" if calling next would cause an error
    ...     next(perms)
    ... except StopIteration:
    ...     print('No more permutations!')
    No more permutations!
    >>> sorted(gen_perms([1, 2, 3])) # Returns a sorted list containing elements of the generator
    [[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]
    >>> sorted(gen_perms((10, 20, 30)))
    [[10, 20, 30], [10, 30, 20], [20, 10, 30], [20, 30, 10], [30, 10, 20], [30, 20, 10]]
    >>> sorted(gen_perms("ab"))
    [['a', 'b'], ['b', 'a']]
    """
    if not seq:
        yield []
    else:
        for perm in gen_perms(seq[1:]):
            for i in range(len(seq)):
                yield perm[i:] + [seq[0]] + perm[:i] 


```
