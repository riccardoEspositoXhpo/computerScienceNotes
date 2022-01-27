# Java Wiki

## Basics

### Hello World

```java

public class hello {
    public static void main (Strings args[]) {
        System.out.println("Hello, World");
    }
}


```

### Built-in Data Types

Java has a few familiar built-in data types. Some of the language specific nuances are explained below:

```java

/*
char - character
String - sequence of characters
int - number, whole
double - floating point approximation of a real number
boolean - true or false

... and more
*/

// Strings

// int
int a = 1
int b = 0

int c = a / b // runtime error

// other values similar to int are 'short' (up to 2^15), 'long' (up to 2^61)

// double
double a = 1
double b = 0

double c = a / b // infinity

Math.sqrt(-1) // NaN

// other values are 'float'

boolean a = (1 > 0); // true


```

### Math

```java

Math.min(a, b);
Math.max(a, b);
Math.sin(x);
Math.cos(x);
Math.pow(x, 2);
Math.sqrt(x);

```

### Loops and Conditions

```java

if (x > 0) {
    x = 10
}
else if (x < 0) {
    x = -10
}
else {
    x = 0
}


while (x > 0) {
    x / 10
}

int sum = 0;

for (int i = 0; i < n; i++) {
    sum = sum + i;
}

```

Other less common control flow statements are shown below.

```java

// break statement
public class Prime {

    public static void main(String[] args) { 
        long n = Long.parseLong(args[0]);
        boolean isPrime = true;
        if (n < 2) isPrime = false;

        // try all possible factors of n
        // if if n has a factor, then it has one less than or equal to sqrt(n),
        // so for efficiency we only need to check factor <= sqrt(n) or
        // equivalently factor*factor <= n
        for (long factor = 2; factor*factor <= n; factor++) {

            // if factor divides evenly into n, n is not prime, so break out of loop
            if (n % factor == 0) {
                isPrime = false;
                break;
            }
        }

        // print out whether n is prime
        if (isPrime) System.out.println(n + " is prime");
        else         System.out.println(n + " is not prime");
    }
}

public class IncrementOdd {

    public static void main(String[] args) {

        for (int i = 0; i < 100; i++) {

            // the continue statement transfers control directly to the next increment ignoring any other code 
            if (i % 0 == 0) {
                continue
            }
            i += i
        }
    }
}

// switch statement controls more than 2 options simultaneously
public class NameOfDay {
    public static void main(String[] args) { 
        int day = Integer.parseInt(args[0]);
        switch (day) {
            case 0:  System.out.println("Sunday");      break;
            case 1:  System.out.println("Monday");      break;
            case 2:  System.out.println("Tuesday");     break;
            case 3:  System.out.println("Wednesday");   break;
            case 4:  System.out.println("Thursday");    break;
            case 5:  System.out.println("Friday");      break;
            case 6:  System.out.println("Saturday");    break;
            default: System.out.println("invalid day"); break;
        }
    }
}

public class RandomDo {
    public static void main(String[] args) { 
        do {
            // do something
        }
        while (n > 0)
    }
}

// concise conditional statement
int min = (x < y) ? x : y;

```

### Type Casting

In Java you must speficy the type of each variable when you declare it. This means that we need to be careful while doing math in order to avoid unexpected results.

```java

int a = 7;
int b = 2;

int c = a / b; // the answer should be 3.5, but this yields 3 because you are dividing two integers, and the result gets truncated

// this can be avoided with type casting
double d = (double) a / b;

// in the same way, some methods require a specific data type, for example
int n = (int) (Math.random() * 50) // random number between 0 and 49


```

## Command Line Arguments

```java

public class SumInts {

    public static void main(String[] args) {

        int a = Integer.parseInt(args[0]);
        int b = Integer.parseInt(args[1]);

        double d = Double.parseDouble(args[2]);
        String s = args[3] // args are passed as strings

        // above methods can be invoked on any datatype

        int c = a + b;

        System.out.println(c);
    }
}


```

## Input and Output

### Output Stream

Below we collect the various types of print statements available in java.

```java

System.out.println("ciao") // prints line and newLine
System.out.print("ciao") // prints but does not move to newLine


// infinite output stream example
public class RandomSequence {

    public static void main(String[] args) {
        int n = Integer.parseInt(args[0]);

        for (int i = 0; i < n; i++) {
            // we can write our own output stream
            // that is independent of System.out
            // this is an abstraction
            StdOut.println(Math.random());
        }
    }
}

// from the StdOut library we can use the prtinf function 

System.out.printf("%7.5f", variable);
// %7 is 7 characters in width
// .5 is 5 digit precision (or 5 character)
// f is a conversion specification (see below, d is int ...)
// variable is the number or string to print

// Examples

int n = 512;
System.out.printf("%-14d", n); // "           512"
System.out.printf("%14d", n); //  "512           "

double x = 1595.1680010754;
System.out.printf("%14.2f", x); // "     1595.17"
System.out.printf("%.7f", x); // "1595.1680011"
System.out.printf("%14.4e", x); // "1.5952e+03"

String t = "Hello, World";
System.out.printf("%14s", t); //    "  Hello, World"
System.out.printf("%-14s", t); //   "Hello, World  "
System.out.printf("%-14.5s", t); // "Hello         "

boolean bool = true; 
System.out.printf("%b", bool) // "true"  


```

We can redirect standard output using the terminal:

```unix
java RandomSequence.java > data.txt

```

### Input Stream

```java

// infinite output stream example
public class Average {

    public static void main(String[] args) {

        double sum = 0;
        int n = 0;

        // we can write our own input stream
        while (!StdIn.isEmpty()) {

            doube x = StdIn.readDouble();
            sum += x;
            n++;
        }
        StdOut.println(sum / n);
    }
}

```

To redirect standard input, we can use the terminal:

```unix
java Average.java < data.txt

```

### Connecting Input and Output

Piping is a useful way to connect the In and Out of two programs. See Input and Output Stream for the program definitions.

```unix
java RandomSequence.java 100000 | java Average.java

```

## Arrays

Arrays are commonly found in most programming languages and are useful to store large amounts of data. The syntax in Java is as follows:

```java

double[] a; // datatype followed by [] declares an array
a = new double[10]; // initialize a with 10 values - automatically with 0.0

boolean[] b = new boolean[10]; // compact statement


b = a; // this DOES NOT COPY anything, it just points b to the same location in memory as a

// this is the way to copy an array
double[] c = new double[a.length];

for (int i = 0; i < a.length; i ++) {

    c[i] = a[i];
};


// array can be initialized with literal values
double[] x = {0.2, 0.1, 5.4, 3.2};


// arrays can have more than one dimension
double[][] e = new double[10][10];

// initialize to literal values
double[][] p =
    {
    { .92, .02, .02, .02, .02 },
    { .02, .92, .32, .32, .32 },
    { .02, .02, .02, .92, .02 },
    { .92, .02, .02, .02, .02 },
    { .47, .02, .47, .02, .02 },
    };

// theoretically there is no limit to the dimension of an array
int n = 5;

double[][][] a = new double[n][n][n];


```

## Strings

Below we collate all useful string manipulation techniques.

```java

// string length
String s = "ciao";

s.length() // 4

s.charAt(1) // i

// combine the two concepts, loop characters of string
for (int i = 0; i < s.length(); i++) {
    if (s.charAt(i) = 'i') System.out.println("i is found");
}


```

## Equality

We need to be careful, the == symbol does not check for logical equality, but for equality in the memory address.
This can lead to bugs in code. To compare two strings, we should use the .equals() method.

```java

// These two have the same value
new String("test").equals("test") // --> true 

// ... but they are not the same object
new String("test") == "test" // --> false 

// ... neither are these
new String("test") == new String("test") // --> false 

// ... but these are because literals are interned by 
// the compiler and thus refer to the same object
"test" == "test" // --> true 

```

## Min and Max of many numbers

```java

double a = Double.parseDouble(args[0]);
double b = Double.parseDouble(args[1]);
double c = Double.parseDouble(args[2]);
double d = Double.parseDouble(args[3]);
double e = Double.parseDouble(args[4]);
double f = Double.parseDouble(args[5]);

// find min and max value   
double lowest = Math.min(a, Math.min(b, Math.min(c, Math.min(d, Math.min(e, f)))));
double highest = Math.max(a, Math.max(b, Math.max(c, Math.max(d, Math.max(e, f)))));

```

## Infinity

Double values support infinity in Java, this is useful when we want to initialize a Math.max or a Math.min operation.

```java

double a = Double.POSITIVE_INFINITY;
double b = Double.NEGATIVE_INFINITY;


```