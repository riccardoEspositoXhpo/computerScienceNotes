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
Math.random();

```

### Loops and Conditions

```java

int x = 2;

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

## Input Output

Java supports reading streams of data as opposed to just argument. You can technically connect two java programs by piping them together and providing a constant stream of data from one to the other, without overloading your current system storage.

### Parsing File Inputs

```java
// example code to count words in a file
public class WordCount {
    public static void main(String[] args) {

        int count = 0;    
        while (!StdIn.isEmpty()) {
            String word = StdIn.readString();
            count++;
        }
      
        // output
        StdOut.println("number of words  = " + count);
    }
}

```

### Command Line Input Stream

```java

public class TwentyQuestions {
    public static void main(String[] args) {

        // Generate a number and answer questions
        // while the user tries to guess the value.
        int secret = 1 + (int) (Math.random() * 1000000);

        StdOut.print("I'm thinking of a number ");
        StdOut.println("between 1 and 1,000,000");
        int guess = 0; 
        while (guess != secret) {

            // Solicit one guess and provide one answer
            StdOut.print("What's your guess? ");
            guess = StdIn.readInt();
            if      (guess < secret) StdOut.println("Too low");
            else if (guess > secret) StdOut.println("Too high");
            else                     StdOut.println("You win!");
        }
    }
} 


```

### Drawing

```java

public class Checkerboard {
    
    public static void main(String[] args) {
        
        int n = Integer.parseInt(args[0]);
        StdDraw.setXscale(0, n);
        StdDraw.setYscale(0, n);

        for (int i = 0; i < n; i++){
            for (int j = 0; j < n; j++){
                if ((i + j) % 2 == 0) StdDraw.setPenColor(StdDraw.WHITE);
                else StdDraw.setPenColor(StdDraw.BLACK);
                StdDraw.filledSquare(i + 0.5, j + 0.5, 0.5);

            
            }            
        }


    }
}


```

## Static Methods

Implementing functions in Java is simple and lends itself to modular programming.

```java

// disregard the low utility of this code - for demostration purposes only
public class Averages {
    // a class contains a list of functions, and main is the one that is executed
    public static double average(double a, double b) {
        return (a + b) / 2;
        
    }
    public static double average(double a, double b, double c) {
        return (a + b + c) / 3;
        // two static methods can have the same name and different number of arguments
        // they will be called appropriately
    }
    public static void main(String[] args) {
        
        StdOut.println(average(1, 5));
        StdOut.println(average(1, 5, 7));
    }
}


```

If you implement a static method just to host some functions then it is still mandatory to have an empty main method.

```java
public class FunctionExamples {

    // absolute value of an int value
    public static int abs(int x) {
        if (x < 0) return -x;
        else       return  x;
    }

    // absolute value of a double value (overloading)
    public static double abs(double x) {
        if (x < 0) return -x;
        else       return  x;
    }

    // primality test (multiple return statements)
    public static boolean isPrime(int n) {
        if (n < 2) return false; 
        for (int i = 2; i <= n/i; i++) 
            if (n % i == 0) return false; 
        return true; 
    }

    public static void main(String[] args) {
    }
}

```

## Recursion

Recursion occurs when a function calls itself. We willn not cover the basics here, but focus on some common pitfalls:

- You are missing the base case
- You are not reducing the size of the problem
- You go in StackOverflow if your input is too large

The last point is particularly important. You may think you have devised the best recursive solution to a problem only to find out that it is spectacularly inefficient. Always consider the memory requirements of your programs.

```java

// example of inefficient recursion

public class Fibonacci {
    public static long fibonacci(int n) {
        if (n <= 1) return n;
        else return fibonacci(n-1) + fibonacci(n-2);
    }

    public static void main(String[] args) {
        int n = Integer.parseInt(args[0]);
        StdOut.println(fibonacci(n));

    }

}

/* Why is this inefficient?

To calculate a Fibonacci number, you repeatedly re-run the recursion on numbers you have already computed. 
Wouldn't it be smarter to save down the result in some array and quickly retrieve it later?

*/

// example of top-down fibonacci
public class TopDownFibonacci {
    private static long[] f = new long[92];

    public static long fibonacci(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        // return cached value (if previously computed)
        if (f[n] > 0) return f[n];

        // compute and cache value
        f[n] = fibonacci(n-1) + fibonacci(n-2);
        return f[n];
    }

    public static void main(String[] args) {
        int n = Integer.parseInt(args[0]);
        for (int i = 1; i <= n; i++)
            StdOut.println(i + ": " + fibonacci(i));
    }

}


// example of bottom up Fibonacci

public class BottomUpFibonacci {

    public static long fibonacci(int n) {
        long[] f = new long[n+1];
        f[0] = 0;
        f[1] = 1;
        for (int i = 2; i <= n; i++)
            f[i] = f[i-1] + f[i-2]; // this is actually not recursion, we are building up the Fibonacci sequence
        return f[n];
    }

    public static void main(String[] args) {
        int n = Integer.parseInt(args[0]);
        for (int i = 1; i <= n; i++)
            StdOut.println(i + ": " + fibonacci(i));
    }

}

```

## Java Class and Variables

```java

public class Test {

    // this gets instantiated together with the class. Also you can't access it outside it.
    private static int a = 2;

    // this method can be accessed by all parts of the program
    public static int pub(int a) {
        return a;
    }

    // this one is only accessible by the Test class
    private static int priv(int a) {
        return a;
    }

}

```  

In general, a method can be public, private or protected. Below is a table that summarizes where the data can be read:

|           |Class|Package|Subclass - same Pkg|Subclass - diff Pkg|World|
|-----------|-----|-------|-------------------|-------------------|-----|
|public     |  +  |   +   |         +         |         +         |  +  |
|protected  |  +  |   +   |         +         |         +         |  -  |
|no modifier|  +  |   +   |         +         |         -         |  -  |
|private    |  +  |   -   |         -         |         -         |  -  |

## Objects

Java is very suited for OOP, as everything in Java is a Class. Below we show some code on how to create / instantiate new data types in Java.

One creates a new object by: obj = new Clock(2, 30);

```java

public class Clock {

    // private means that this cannot be accessed externally from Clock
    // final means this can't be changed - i.e. a CONSTANT
    private static final int MINUTES_PER_HOUR = 60;
    private static final int HOURS_PER_DAY = 24;
    private int hour, min;


    // this is the "constructor"
    public Clock(int h, int m) {
        hour = h;
        min = m;
        if (hour < 0 || hour >= HOURS_PER_DAY || min < 0 || min >= MINUTES_PER_HOUR)
            throw new IllegalArgumentException();
    }

    // Creates a clock whose initial time is specified as a string, using the format HH:MM.
    public Clock(String s) {
        if (!s.contains(":")) throw new IllegalArgumentException();
        int i = s.indexOf(':');
        String shour = s.substring(0, i);
        String smin = s.substring(i + 1);
        if (shour.length() != 2 || smin.length() != 2) throw new IllegalArgumentException();
        hour = Integer.parseInt(shour);
        min = Integer.parseInt(smin);
        if (hour < 0 || hour >= HOURS_PER_DAY || min < 0 || min >= MINUTES_PER_HOUR)
            throw new IllegalArgumentException();
    }

    // Returns a string representation of this clock, using the format HH:MM.
    public String toString() {
        String shour = Integer.toString(hour);
        String smin = Integer.toString(min);
        if (shour.length() == 1) shour = "0" + shour;
        if (smin.length() == 1) smin = "0" + smin;
        return shour + ":" + smin;
    }

    // Is the time on this clock earlier than the time on that one?
    public boolean isEarlierThan(Clock that) {
        return (hour < that.hour) || (hour == that.hour && min < that.min);
    }

    // Adds 1 minute to the time on this clock.
    public void tic() {
        if (min != MINUTES_PER_HOUR - 1) min++;
        else if (hour == HOURS_PER_DAY - 1) {
            hour = 0;
            min = 0;
        }
        else {
            hour++;
            min = 0;
        }
    }

    // Adds Δ minutes to the time on this clock.
    public void toc(int delta) {
        if (delta < 0) throw new IllegalArgumentException();
        int minRepresentation = hour * MINUTES_PER_HOUR + min;
        minRepresentation += delta;
        int newHour = minRepresentation / MINUTES_PER_HOUR;
        int newMin = minRepresentation - MINUTES_PER_HOUR * newHour;
        hour = newHour % HOURS_PER_DAY;
        min = newMin % MINUTES_PER_HOUR;
    }

    public static void main(String[] args) {
        Clock userTime = new Clock(23, 55);
        Clock otherTime = new Clock("08:45");
        StdOut.println(userTime.toString());
        userTime.tic();
        StdOut.println(userTime.toString());
        userTime.toc(15);
        StdOut.println(userTime.toString());
        StdOut.println(userTime.isEarlierThan(otherTime));
        StdOut.println(otherTime.toString());
        otherTime.toc(1441);
        StdOut.println(otherTime.toString());
    }
}



```



## Exceptions

Exceptions are a signal that something went wrong in the execution of the program. However, we can plan ahead and proactively throw exceptions ourselves.

```java


if (condition === True)
    // this is an existing exception in Java, you can create your own as well. In the evn everything is a class.
    throw new IllegalArgumentException();


```