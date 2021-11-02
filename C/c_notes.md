# C Wiki

## Basics

### File Headers
```c
#include <stdio.h>
```

### Basic Code Format
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

    // characters require single quotes, everything else uses double quotes!
    char c = 'c'

}
```

### Conditions

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

### Loops

```c
int main(void)
{

    while (true)
    {
        // infinite loop in c
    }

    int i = 0;

    while (i < 50)
    {
        // execute loop 5 times
    }

    for int (j = 0; j < 50; j++>)
    {
        /* initialize variable
        set the stop value
        decide the increment (increment could be negative with --)
    }


    int n = 0;

    do 
    {
        //this executes a block of code once, and then checks the condition
    }
    while (n > 0);

}
```

### Byte Size Imprecision

```c
int main(void){

    // try to divide 1 by 10
    float x = 1;
    float y = 10;

    printf("%.50f\n", x / y);
    // result is imprecise after a few digits
}
```

### Custom Functions and Prototypes


```c

// the code is executed in order, you must signal the existence of a function before main actually
// calls it. In this way you can keep it at the bottom.
void meow(int);

int main(void)
{
    meow(3)
}

void meow(int n)
{

    for (i = 0; i < n; i++)
    {
        printf("meow\n");

    }
}
```

### Constants

```c

// typical to declare constants in capital letters
const int TOTAL = 3;

int main(void)
{

    // When you declare an array you must specify the size
    int socres[TOTAL];
}
```

### Useful Libraries and Functions

```c

// standard library
#include <stdio.h>

// includes string manipulation like toupper tolower and so on
#include <ctype.h>

// more string manipulation, including strcopy
# include <string.h>

int main(void)
{

    // list of useful functions here

    // compares two strings giving a 0 or a <> 0 (depending on like ascii character order)
    strcmp('Beily','Beily')

    // length of string
    strlen(string)

}

```

### Custom Data Types

```c

// you can define custom data types as follows
typedef struct
{
    string name;
    string number;
}
person;

const int NUMBER = 10;

int main(void)
{
    person people[NUMBER];

    for (int i = 0; i < NUMBER; i++)
    {
        people[i].name = "Beily"
        people[i].number = "1234"
    }
}
```


### User Input

```c
// argc is the count of args, please note main.c is included if you type 'main.c something'
// argv is the value of the args, argv[1] grabs the first command line argument, arg[0] is main.c
int main(int argc, string argv[])
{
    if (argc !=2)
    {
        // missing command line argument
        return 1;
    }
}
```

### Type casting

```c 

int main(void)
{

    float x = 1.2;

    // in order to use or compare variables, they must be of the same datatype
    // type casting let's you change a datatype, beware of truncation and other side effects
    printf("%i\n", int(x))
}

```

## Advanced Topics

### Pointers

```c

int main(void)
{

    int n = 50;

    // p is che code for 'address' in memory (i.e. location)
    // a pointer contains the address for a variable
    // &n = tell me the location of N in memory
    // *n = go to that address
    // essentially you can undo the effects of & with *

    // Create a pointer to the value of n
    int *p = &n

    // prints the value of p 
    printf("%i\n", *p)

    // in fact, a string is just a pointer to the first character of itself, you can expose it as follows

    string s = "hi!"

    printf("%p\n",s);
    printf("%p\n",&s[1]);

    // with pointer addresses you can do arithmetic
    printf("%c\n", *s);
    printf("%c\n", *(s + 1));
    printf("%c\n", *(s + 2));


}
```

### Pointers in Functions

```c

void swap(int *a, int *b)

int main(void)
{

    int x = 1;
    int y = 2;

    // we use pointers to properly swap two numbers
    swap(&x,&y);

}

void swap(int *a, int *b)
{
    int temp;

    // this function is using two pointers to integers
    // in fact we pass in the ADDRESS of the variables
    // in this way we can actually swap their locations in memory
    temp = *a;
    *a = *b;
    *b = temp;

    // if you do not use pointers and try to swap, it will not work
    // if you simply do temp = a ; a = b; b = temp
    // it won't work
}


```

### Malloc

```c 

int main(void)
{
    // List of size 3. Malloc provides us with enough memory to use
    int *list = malloc(3 * sizeof(int));

    // if something goes wrong in memory allocation we exit
    if (list == NULL)
    {
        return 1;
    }

    // Initialize list of size 3 with numbers
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;

    // Resize list to be of size 4. Realloc gives you a different size of memory
    int *tmp = realloc(list, 4 * sizeof(int));
    if (tmp == NULL)
    {
        free(list);
        return 1;
    }
    list = tmp;

    // Add number to list
    list[3] = 4;

    // Print list
    for (int i = 0; i < 4; i++)
    {
        printf("%i\n", list[i]);
    }

    // Free list
    free(list);
    return 0;

    // EVERY TIME YOU USE MALLOC / REALLOC YOU MUST USE FREE. It is good practice
    // linux command line tools such as valgrind can help out in assessing memory leaks
}
```

### Files

```c
int main(void)
{
    // opens file (which is a pointer) in append mode ("r" is read, "w" is write)
    FILE *file = fopen("filename.csv", "a")'

    fprintf(file, "add some data to file");

    fclose(file);

    FILE *input = fopen("input.csv","w");
    // reads into a variable called header, in sizeof(uint8_t) bytes, 44 times, from a file called input
    fread(header, sizeof(uint8_t), 44, input)

    // same concept for write
    fwrite(header, sizeof(uint8_t), 44, input)

    // shortcut to go to end of file
    fseek(input, 0, SEEK_END);


}
```


### ASCII

```c

int main(void)
{

        word = "YOWHATUP"; 

        if (word[i] >= 'A' && word[i] <= 'Z')
        {
            // take each letter and subtract 65 (A's value in ASCII)
            score += POINTS[(int)(word[i] - 65)];

            // essentially you can do math with characters, because they are expressed in ASCII
        }

    }

}
```

### Linked Lists

```c

// Implements a list of numbers with linked list

#include <stdio.h>
#include <stdlib.h>

// Represents a node
typedef struct node
{
    int number;
    struct node *next;
}
node;
// interesting syntax to call itself inside the definition

int main(void)
{
    // List of size 0
    node *list = NULL;

    // Add number to list
    node *n = malloc(sizeof(node));
    
    
    if (n == NULL)
    {
        return 1;
    }
    
    // we assign a value to node n, but we point the next one to nothing
    n->number = 1;
    n->next = NULL;
    
    // the first item of the list
    list = n;

    // Add number to list
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free(list);
        return 1;
    }

    n->number = 2;
    n->next = NULL;

    // this notation is equivalent to list.(*next)
    // it essentially is creating a link between the numbers (this n1 and the n2)
    list->next = n;

    // Add number to list
    n = malloc(sizeof(node));
    
    if (n == NULL)
    {
        // when we free we must free all the way up the chain
        free(list->next);
        free(list);
        return 1;
    }
    n->number = 3;
    n->next = NULL;
    
    list->next->next = n;


    // Print list
    for (node *tmp = list; tmp != NULL; tmp = tmp->next)
    {
        printf("%i\n", tmp->number);
    }

    // Free list
    while (list != NULL)
    {
        node *tmp = list->next;
        free(list);
        list = tmp;
    }
    return 0;
}

```


### Binary Tree

```c

// Represents a node
typedef struct node
{
    int number;
    struct node *left;
    struct node *right;
}
node;

void free_tree(node *root);
void print_tree(node *root);

int main(void)
{
    
    // Tree of size 0
    node *tree = NULL;

    // Add number to list
    node *n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1;
    }
    n->number = 2;
    n->left = NULL;
    n->right = NULL;
    tree = n;

    // Add number to list
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1;
    }
    n->number = 1;
    n->left = NULL;
    n->right = NULL;
    tree->left = n;

    // Add number to list
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1;
    }
    n->number = 3;
    n->left = NULL;
    n->right = NULL;
    tree->right = n;

    // Print tree
    print_tree(tree);

    // Free tree
    free_tree(tree);
}

void free_tree(node *root)
{
    if (root == NULL)
    {
        return;
    }
    free_tree(root->left);
    free_tree(root->right);
    free(root);
}

void print_tree(node *root)
{
    if (root == NULL)
    {
        return;
    }

    // we use recursion to keep navigating down the tree
    print_tree(root->left);
    printf("%i\n", root->number);
    print_tree(root->right);
}

```

### Recursion

```c

// sampel struct to define purson, has two pointers to different person structs for parents
typedef struct person
{
    struct person *parents[2];
    char alleles[2];
}
person;

const int GENERATIONS = 3;

int main(void)
{
    // Seed random number generator
    srand(time(0));

    // Create a new family with three generations
    person *p = create_family(GENERATIONS);

    // Print family tree of blood types
    print_family(p, 0);

    // Free memory
    free_family(p);
}
// Create a new individual with `generations`
person *create_family(int generations)
{

    /*
    Recursion is a mind-bend.
    Assuming we have 3 generations, we start in the if condition
    The first parent is "create family" of generation 2
    It actually stays in there and creates parent[0] of generation 1
    but in generation 1 we know we are at the "top"
    so we point every parent to NULL
    and generate the AB alleles
    then the function returns.
    We are back in generation 2,
    Parent[1] is created in the same way
    The alleles are "inherited" from the parents  randomly
    Now our individual is setup like both of the parents
    The cycle can continue until we are actually back in the first function call (gen 3)
    */ 


    // Allocate memory for new person
    person *p = malloc(sizeof(person));

    // Generation with parent data
    if (generations > 1)
    {



        // Recursively create blood type histories for parents
        p->parents[0] = create_family(generations - 1);
        p->parents[1] = create_family(generations - 1);

        // Randomly assign child alleles based on parents
        p->alleles[0] = p->parents[0]->alleles[rand() % 2];
        p->alleles[1] = p->parents[1]->alleles[rand() % 2];
    }

    // Generation without parent data
    else
    {
        p->parents[0] = NULL;
        p->parents[1] = NULL;

        p->alleles[0] = random_allele();
        p->alleles[1] = random_allele();
    }

    // Return newly created person
    return p;
}


```  

Visualized, recursion looks like this:

- [Gen 3] Enter Function
    - [Gen 2] Enter Function
        - [Gen 1] Enter Function
        - Assign data to Gen 1
        - Function returns
    - Assign data to Gen 2
    - Function returns
- Assign data to Gen 3
- Function returns

Essentially, it starts and goes all the way to the end, and then returns again and again until it is back at the top.


## Tips and Tricks