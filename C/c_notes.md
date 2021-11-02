# Wiki of C Notes divided by section

## Basics

#### File Headers
```c
#include <stdio.h>
```

#### Basic Code Format
```c

// void is the argument of the function, see argc/argv for more
int main(void) 
// main is the program that executes automatically
{
    
    // char * is a pointer to a set of characters
    char * test = "world";

    // printf is the standard printing function, does not include newlines
    printf("hello, %s\n", test);

    // long is a longer integer, takes up more memory
    long x = 2;
    long y = 4;

    // print requires to specify the format of the output - %i int, %f float, %c char
    printf("%ld\n", x + y);
}
```

#### Conditions

```c

int main(void)
{
    int x = 2;
    int y = 4;

    if (x < y)
    {
        // x smaller than y
    } 
    else if (x > y)
    {
        // x larger than y
    }
    else if (x == 2 || y == 2)
    {
        // either x or y are 2
    }
    else if (x ==2 && y ==2)
    {
        // both x and y are 2
    }
    else 
    {
        // x is equal to y
    }    
}
```

#### Loops

int main(void)
{

    while

}


## Section 2

## Section 3