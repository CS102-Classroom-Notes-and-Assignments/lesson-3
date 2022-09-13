# lesson-3

#### BITWISE OPERATORS
These can only be applied to integral operands, that is, char, short, int, and long, whether signed or unsigned.

- &  	bitwise AND
- |  	bitwise inclusive OR
- ^  	bitwise exclusive OR
- <<  	left shift
- \>> 	 right shift
- ~ 	 one's complement (unary)

Note that this is different than the logical operators && and ||. If x=1, and y=2, x & y = 0, but x && y=1.

The shift operators << and >> perform left and right shifts of their left operand by the number of bit positions given by the right operand, which must be non-negative. Thus x<<2, shifts the value of x by two positions, filling vacated bits with zero; this is equivalent to multiplication by 4. Right shifting an unsigned quantity always fits the vacated bits with zero, signed quantities have differing behavior based on the machine.

```c

#include <stdio.h>

int main()
{
    printf("5 & 4 = %d\n", 5 & 4);
    printf("5 | 4 = %d\n", 5 | 4);
    printf("5 ^ 4 = %d\n", 5 ^ 4);
    printf("5 << 2 = %d\n", 5 << 2);
    printf("12 >> 2 = %d\n", 12 >> 2); //1100 becomes 0011
    printf("~5 = %d\n", ~5);
    // Note 2's complement
    // 5 is 0000...0101
    // Doing on's complement, we have
    // ~5 is 1111...1010
    // which is MIN+sum(2^n) where n excludes n=0 and n=2
    // Or simpler: -8 + 0 + 2 + 0
    return 0;
}

```


#### ASSIGNMENT OPERATORS
- i = i + 2 is equivalent to i += 2
- i = i - 2 is equivalent to i -= 2
- expr1 = (expr1) op (expr2) is equivalent to expr1 op= expr2
- Also works for: * / % << >> & ^ |
- Commonly used in loops
- x *= y + 1 is the same as x = x *(y+1)

Assignment operators can occur in expressions as well, the same way that we have seen:
while (( c = getchar()) != EOF)

++ and – may be used either as a prefix or postfix operator. In both cases, the effect is to increment n, but ++n increments n before its value is used, while n++ increments n after its value has been used. 
x= n++; sets x to 5, but, 
x=++n; sets x to 6. In both cases, n becomes 6.

```c
if (c == ‘\n\) {
	s[i] = c;
++i;
}
```
Can be replaced to:
```c
if (c == ‘\n\) {
	s[i++] = c;
}
```

#### PRECEDENCE & ASSOCIATIVITY OPERATORS
The “operator” () refers to a function call. The operators -> and . are used to access members of structures, sizeof (size of an object), * (indirection through a pointer) and * (address of an object), and comma operator will all be discussed in later chapters.
![alt text](<img src="operators.png"  width="75%" height="75%">)


& is unary, && is binary.

C, like most languages, does not specify the order in which operands of an operator are evaluated. The exceptions are &&, ||, ?: and ‘,’). For example, in a statement like x = f() + g(); f may be evaluated before g or vice versa. Same goes with printf(“%d %d\n”, ++n, power(2, n));.  Another situation in which order might matter is a[i] = i++; The moral is that writing code that depends on order of evaluation is a bad programming practice in any language.

#### CONDITIONAL STATEMENTS

#### IF STATEMENTS
```c
if (a > b) 
{
    z = a; // do something
}
```
—--------------
```c
#include <stdio.h>

int main()
{
    int a  = 0;
    int b = 5;
    if (a < b)
    {
        printf("a is less than b\n");
    }
    return 0;
}
```

#### IF-ELSE STATEMENTS
```c
if (a > b) 
{
    z = a; // do something
}
else
{
    z = b; // do something else
}
```
or

expr1 ? expr 2 : expr 3
Note that if expr2 and expr3 are of different types, the type of the result is determined by the conversion result discussed earlier in this chapter. If f is a float and n an int, then the expression (n>0)? f : n is of type float regardless of whether n is positive.

In general it is better to use braces to make it clear which else is associated with which if. Indentation/spacing does not matter so you must make it clear to the compiler if you have nested if/else.

  
#### IF-ELSE STATEMENT EXAMPLE
```c
#include <stdio.h>

int main()
{
    int a = 7;
    int b = 5;
    if (a < b)
    {
        printf("a is less than b\n");
    }
    else
    {
        printf("a is greater than or equal to b\n");
    }
    return 0;
}
```

#### IF-ELSE IF-ELSE STATEMENTS
```c
if (a > b) 
{
    z = a; // do something
}
else if (a > c)
{
    z = c; // do something
}
else
{
    z = b; // do something else
}
```

#### IF-ELSE IF-ELSE STATEMENT EXAMPLE
```c
#include <stdio.h>

int main()
{
    int a = 1;
    int b = 2;
    int c = 3;
    if (a < b)
    {
        printf("a is less than b\n");
    }
    else if(a < c)
    {
        printf("a is less than c and greater than or equal to b\n");
    }
    else
    {
        printf("a is greater than or equal to b and a is greater than or equal to c\n");
    }
    return 0;
}

```

#### BASIC INPUT/OUTPUT
Text input or output, regardless of where it originates or where it goes to, is dealt with as streams of characters. A text stream is a sequence of characters divided into lines;each line consists of zero or more characters followed by a newline character. 
getchar() - reads the next input character from a text stream and returns that as its value.
putchar(c) - prints the contents of the integer variable c as a character, usually on the screen.

#### GETCHAR
gets one character from the command line
```c
#include <stdio.h>

int main()
{
    char c = getchar();
    putchar(c);
    printf("%c", c);

    return 0;
}
```

In this example, we used int for c because we must declare c to be a type big enough to hold any value that getchar() returns. When there is no more input, the end of file (EOF) value is returned. EOF is an integer defined in <stdio.h> but the specific numeric value does not matter as long as it is not the same as any char value.
```c
#include <stdio.h>
/* copy input to output; 1st version */
main()
{
	int c;
	
	c = getchar();
	while( c != EOF) {
		putchar(c);
		c = getchar();
	}
}
```

Can be simplified to below:
```c
#include <stdio.h>
/* copy input to output; 1st version */
main()
{
	int c;
	while( (c = getchar()) != EOF) {
		putchar(c);
	}
}
```

#### SWITCH STATEMENTS
Another way to write if, else-if, and else
Each const-expr is a constant integer value
Each case is like an if, default is like the else
Limited by the number of chars/ints
Default it optional - if none of the cases are there and there is no default, then nothing happens
Must use breaks  to cause an exit from the switch and not execute the next case
```c
switch(expression) {
  case const-expr: statements
  case const-expr: statements
  default: statements
}

```

#### SWITCH STATEMENT EXAMPLE
break causes the switch to end, otherwise, it will continue to the next case
echo $? will show the result of the program
```c
#include <stdio.h>

// This is a simplified version of the example on K&R pg. 59
// Loops and arrays are removed from this example
// We will build upon this example as we continue
int main()
{
    int c, i, nwhite, nother, ndigit;
    nwhite=nother=ndigit=0;

    c = getchar();
    switch (c)
    {
        case '0': // same as 48
        case '1':
        case '2':
        case '3':
        case '4':
        case '5':
        case '6':
        case '7':
        case '8':
        case '9':
            ndigit++;
            break;
        case ' ':
        case '\n':
        case '\t':
            nwhite++;
            break;
        default:
            nother++;
            break;
    }
    printf("ndigits = %d", ndigit);
    printf(", white space = %d, other = %d\n", nwhite, nother);


    return 0;
}
```

Break is not needed in the default case, but it is a good idea to leave it there for defensive programming. If more cases are added later after default, and the programmer forgets to update the prior case, this will make sure that the code does not continue execution to the next case.


## HOMEWORK:
- The C Programming Language, 2nd Edition - Kernighan & Ritchie, Chapter 2.6-2.12, 3.1-3.3, 1.5
- Coding Homework:




