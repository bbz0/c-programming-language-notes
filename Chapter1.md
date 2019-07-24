# The C programming language
Brian W. Kerningham, Dennis M. Ritchie

## Chapter 1 - A Tutorial Introduction
### 1.1 Getting Started
* Hello World in C, `hello.c`:
```C
#include <stdio.h>

main()
{
	printf("hello, world\n");
}
```
* Compile it with the command:
```
cc hello.c
``` 
* When compiling will make `a.out`, run it with:
```
./a.out
```
* It will print:
```
hello, world
```
* A C program contains *functions* and *variables*.
* A function contains *statements* that specify computing operations to be done.
* Variables store values during computation.
* A program begins executing at the beginning of `main`.
* Every program must have a `main` somewhere.
* `#include <stdio.h>` tells the compiler to include the standard input/output library.
* provide *arguments* in the parentheses after the function to communicate data between functions.
* the statements of a function are enclosed in braces { }.
* a function is called by naming it followed by a parathesized list of arguments.
* `printf` is a library function that prints output.
* character in double quotes are called *character string* or *string constant*.
* an *esacpe sequence* are a way to represent hard-to-type or invisible characters.
  * `\n` is for *newline character*
  * `\t` for tab
  * `\b` for backspance
  * `\"` for double quote
  * `\\` for backslash

### 1.2 Variables and Arithmetic Operators
* Example program:
```C
#include <stdio.h>
/* print Fahrenheit-Celsius table
for fahr = 0, 20, ..., 300 */
main()
{
	int fahr, celsius;
	int lower, upper, step;
	lower = 0;
	upper = 300;
	step = 20;
	/* lower limit of temperature scale */
	/* upper limit */
	/* step size */
	fahr = lower;
	while (fahr <= upper) {
		celsius = 5 * (fahr-32) / 9;
		printf("%d\t%d\n", fahr, celsius);
		fahr = fahr + step;
	}
}
```
* A *comment* are characters between `/*` and `*/`, they are ignored by the compiler.
* In C, all variables must be declared before they are used.
* A *declaration* announces the properties of variables, it consists of a name and a list of variables.
* Basic Data Types:
  * The type `int` means that the listed variables are integers.
  * `float` means floating point, which are numbers that have a fractional part.
  * `char`, character - a single byte
  * `short`, a short integer
  * `long`, long integer
  * `double` - double-precision floatingpoint
* *assignment statements*:
```C
lower = 0;
upper = 300;
step = 20;
```
* Individual statements are terminated by semicolons.
* A `while` loop tests the conditions in the paretheses. If true, the statements in the braces are executed, then the condition is re-tested, and if true, the body is executed again. If false, the loop ends.
  * The body of a `while` loop can have single statements like:
```C
while (i < j)
	i = 2 * i;
```
* In C integer division *truncates*: any fractional part will be discarded.
* In `printf("%d\t%d\n", fahr, celsius);`, `printf`'s first argument is a string of characters to be printed. Each `%` indicates where the other arguments are to be substituted.
* Second version of program:
```C
#include <stdio.h>
/* print Fahrenheit-Celsius table
for fahr = 0, 20, ..., 300; floating-point version */
main()
{
	float fahr, celsius;
	float lower, upper, step;
	lower = 0;
	upper = 300;
	step = 20;
	/* lower limit of temperatuire scale */
	/* upper limit */
	/* step size */
	fahr = lower;
	while (fahr <= upper) {
		celsius = (5.0/9.0) * (fahr-32.0);
		printf("%3.0f %6.1f\n", fahr, celsius);
		fahr = fahr + step;
	}
}
```
* `fahr` and `celsius` are declared `float`, thus `5.0/9.0` will not be truncated because it is the ratio of two floating-point values.
* `int` + arithmetic operator + `int = int`.
* `float` + arithmetic operator + `int = float`.
* integers are converted to floating point before operation is done.
* `printf` specifications:
  * `%d` print as decimal integer
  * `%6d` print as decimal integer, 6 characters wide
  * `%f` print as floating point
  * `%6f` print as floating point, 6 characters wide
  * `%.2f` print as floating point, 2 characters after decimal point
  * `%6.2f` print as floating point, at least 6 wide and 2 after decimal point
  * others `%o` for octal, `%x` for hexadecimal, `%c` for character, `%s` for character string and `%%` for itself.

### 1.3 The for statement
* Example program:
```C
#include <stdio.h>
/* print Fahrenheit-Celsius table */
main()
{
	int fahr;
	for (fahr = 0; fahr <= 300; fahr = fahr + 20)
		printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}
```
* The `for` loop is a generalization of the `while`.
  * There are three parts separated by semicolons:
    * First part, the initialization `fahr = 0`, once done the loop proper is entered.
    * The second part, the condition `fahr <= 300`, if true the loop body is executed.
    * The increment step, `fahr = fahr + 20` is executed, and the condition re-evaluated.
    * If false, the loop ends.

### 1.4 Symbolic Constants
* A `#define` line defines a *symbolic name* or *symbolic constant*: `#define` *name* *replacement list*
* The *name* has the same form as a variable name.
* The *replacement text* can be any sequence of characters, not just numbers.
* Symbolic constant names are conventionally written in upper case.
* Example program:
```C
#include <stdio.h>
#define LOWER 0 /* lower limit of table */
#define UPPER 300 /* upper limit */
#define STEP 20 /* step size */

/* print Fahrenheit-Celsius table */
main()
{
	int fahr;
	for (fahr = LOWER; fahr <= UPPER; fahr = fahr + STEP)
		printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}
```

### 1.5 Character Input and Output
* Text input or output is dealt with as streams of characters.
* A *text stream* is a sequence of characters divided into lines.
* Each line consists of zero or more characters followed by a newline character.
* `getchar` reads the *next input character* from a text stream and returns that as it's value.
* `putchar` prints a character each time it is called.

#### 1.5.1 File Copying
* Example program:
```C
#include <stdio.h>
/* copy input to output; 1st version */
main()
{
	int c;
	c = getchar();
	while (c != EOF) {
		putchar(c);
		c = getchar();
	}
}
```
* The relational operator `!=` means "NOT EQUAL TO".
* Characters on the keyboard are stored internally as a bit pattern.
* `getchar` returns `EOF` or "End of File", when there is no more input.
* `c` is declared as an `int` so it can hold `EOF`.
* `EOF` is an integer defined in `<stdio.h>`.
* Example program:
```C
#include <stdio.h>
/* copy input to output; 2nd version */
main()
{
	int c;
	while ((c = getchar()) != EOF)
		putchar(c);
}
```
* The `while` assigns the character to `c` then tests the condition.
* The *precedence* of `!=` is higher than `=` without parentheses it is equivalent to `c = (getchar() != EOF)` which would set `c` to 0 or 1.

#### 1.5.2 Character Counting

