# Scheme

Scheme is a dialect of the Lisp programming language. It was invented during the 1970s but is still popular today (2021).

## Executing Code

Executing Scheme requires an interpreter. This can be either built from scratch or downloaded from the internet.
To construct this wiki I have used the following - <https://inst.eecs.berkeley.edu//~scheme/>.

## Expressions

Expressions are contained within parentheses. You must prefix the operation you want to compute, and then list out the values separated by spaces.

```scheme

(quotient 10 5)
2

(+ (* 3 5) (- 10 6))
19

(+ (* 3
      (+ (* 2 4)
         (+ 3 5)))
   (+ (- 10 7)
      6))

57


(modulo 29 5)
4

(or 1 2 )
; returns true

(and 1 2)
; returns true


```

Indentation is irrelevant, but is often used to provide some order to the code.

## Special Forms

Special forms in Scheme look syntacticallly like an expression, but are evaluated differently.

### Conditional Statements

```scheme

(if (> x 0) x -x)

```

The above is some kind of abs function, if x is greater than 0, we return x, else we return -x.

```scheme

; if statements can be nested too

(define (over-or-under-if num1 num2)
    (if (< num1 num2) -1 (if (> num1 num2) 1 0)))

; a different way to provide if - elif - else without nesting ifs is to use cond

(cond (test1
       (action1))
      (test2
       (action2))
      (test3
       (action3))
      (else
       (action4)))


```

### Booleans

```scheme

(>= 2 1)

; true value in scheme, the above returns this
#t

; false value
#f

scm> (even? (quotient 45 2))
#t

```

### Procedures

We can define procedures, which are the scheme equivalent of functions.

We can either name some values like this,

```scheme

(define pi 3.14)
(* pi 2)
6.28

```

or we can name new procedures themselves.

```scheme

(define (square x) (* x x))

(define (abs x)
    (if (< x 0)
        (- x)
        x))

(define (average x y)
  (/ (+ x y) 2))

```

The define keyword is followed by a function name, formal parameters and evaluation expression.

### Lambda

Lambda is used as in other languages to create anonymous procedures.
Two alternative ways to perform x + 4.

```scheme
(define (plus4 x) (+ x 4))
(define plus4 (lambda (x) (+ x 4)))
```

Lambdas can also be used within a normal call expression directly.

```scheme
((lambda (x y z) (+ x y (square z))) 1 2 3)
```

## Compound Values

Compound values such as lists (which in Scheme are implemented as linked lists), require special syntax.

```scheme
(cons 1
      (cons 2
            (cons 3
                  (cons 4 nil))))
; cons is the synax to create a list
; it should have two elements, the value and the "rest" of the list
; special value nil or '() is used to define the empty list
(1 2 3 4)

; alternative way to define a linked list
(list 1 2 3 4)
(1 2 3 4)

(define one-through-four (list 1 2 3 4))

; car is used to access the first element
(car one-through-four)
1

; cdr is used to access the rest
(cdr one-through-four)
(2 3 4)

(car (cdr one-through-four))
2

(cons 10 one-through-four)
(10 1 2 3 4)

(cons 5 one-through-four)
(5 1 2 3 4)

```

## Symbolic Data

By using special notation, we can actually flag to scheme that we want to insert a variable into a list instead of its value.
This can interstingly happen before any such value is defined.

```scheme

(list 'a 2)
(a 2)

```

The a is not evaluated and is thus said to be quoted.

With quotation we can actually simplify some syntax. Let's see how we can use this to define lists.

```scheme

(car '(a b c))
a
(cdr '(a b c))
(b c)

```

In this way we were able to just access the representation of scheme lists without defining them.
