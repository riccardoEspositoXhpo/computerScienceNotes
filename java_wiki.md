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
