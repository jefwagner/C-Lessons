Lesson 01
=========
      
## Introduction: Compiled Programming Languages ##

Programming languages let us give instructions to computers in human readable form. The instructions are often written in a simple text file. The text is called source code. The extension on the file depends on the language. We will use the C programming language in these lessons, and the extension for a C source code is '.c'. The source files can be created/opened in a program called a text editor. I won't tell you which editor to use. I will recommend using a so called 'programming text editor' which can do syntax highlighting and can interface with the command line. Start your text editor and create a file  with the following contents replacing "Your name" with your name, and "Today's date" with today's date. Save the file with the name "hello.c".

```c
/* Author : Your name */
/* Date : Today's date */

#include <stdio.h>

int main(){
  printf( "Hello World!\n");
  return 0;
}
```

After you have a source file a second program translates the human readable program into instructions that the computer can understand. This program is called a compiler. (*Note: There are other methods of going from source code to program. Google, compiled vs interpreted languages if you are interested.*) Most compilers are command line programs, and are accessed from the command line. We will use the gnu C Compiler, which is called with the command 'gcc'. (*There are other C compilers: some important ones are clang, Apple's compiler and icc, intel's compiler.*) In the command line, use the `cd` command to navigate to the directory where you saved the "hello.c" source file. Type the following command at the command prompt.
```bash
$> gcc hello.c
```
(*Note: When giving commands on the command line, I will write precede them with a $> to represent the command prompt. Do not copy these two symbols. If you do you will get an error message.*) The command should have created a new file called "a.out". This is your compiled program. You can now run you program by typing it's name preceded by a './':
```bash
$> ./a.out
```
If everything worked, it should print "Hello World!" to the command line and give you a new prompt. 
```bash
$> ./a.out
Hello World!
$>
```
If it didn't work you get your first try at debugging! The most common mistake is that you have not correctly navigated to the directory that holds your "hello.c" source file. You can check the present working directory with the 'pwd' command, and you can check the contents of the directory with the 'ls' command. The second most common mistake is not having gcc compiler installed correctly.

If it did work, Contragulations! You have just written and compiled your first program. Lets go through the program line by line to see what parts it has. The very first thing we see are two comments.
```c
/* Author : Your name */
/* Date : Today's date */
```
A comment is any thing between `/*` and `*/`. It is important to comment you code. In this case, the code was used to note the author and date of creation. You also often describe the purpose of the code and any inputs and outputs it might have. The next thing we see is an include statement.
```c
#include <stdio.h>
```
An include statement includes the source from another file into the current file. Note that the line starts with a hash '#' and does not end in a semi-colon. This is the mark of a pre-processor command. The preprocessor commands are run before the compiler runs and does things such as including the contents of other files, or simple text substitutions. In the above line we included the 'STandarD Input/Output' header file, which has the 'prototypes' for the input/output functions in the standard library. We will go over what a prototype is next lesson. For now, it is suffucient to say we have to include this line if we want to use the 'printf' function which allows us to output text to the command line. Next we see the definition of the main function.
```c
int main(){
```
The main function is what is executed when you run the program. For a program to be executable, it must contain a single main funciton. We will revisit the syntax of this declaration next lesson when we discuss functions and how to define them. The function in this case is everything inside the curly braces '{}'. Next comes the meat of the program, the 'printf' function.
```c
  printf( "Hello World\n");
```
There are several parts we need to discuss here. First, lets address the function call itself. We call a function by writing it's name followed by parenthesis. Inside the parenthesis we put the arguments. The 'printf' function takes a various number of arguments, the first argument is a string (discussed in lesson 2) and all of the remaining arguments are variables to print out. In this case there are no variables, so only the string is printed. The next line is the return statement, which ends rhe function.
```c
  return 0;
```
The return statement signifies the end of a function. The return value is given back to the caller, in this case that is the operating system. It is standard practice that the main function returns 0 if the program exits successfully, and returns a non-zero value if there is an error that forces the program to exit early.

After you've written the source code, you have to compile it. This is done on the command line with the 'gcc' command as shown above. However, there are several options that can be added to the command that give the compiler a little more detail about what we would like to do. The first option is to choose an output file name different than 'a.out'. This is done with the '-o OUTPUT_NAME' options. For example if we wanted to call the program 'hello' we would give the command written below.
```bash
$> gcc -o hello hello.c
```
(*Note: In the unix environment, executable programs have no extension.*) There are several other command line options that we will want to know about. For now, we will focus on adding just a few. First is the '-Wall' option. This turns on all possible warnings (-W for warning, then all; not the word wall). A warning is something the that will compile, but is often the result of a mistake - most often for me at least for leaving out semicolons. Next is the '-O0', '-O1', '-O2', '-O3' (that is dash capital O, then a number, not dash then the numeral 0). This enables or disables optimizations. You will often want to use '-O0' or '-O1' when you are writing the program, then switch to '-O2' or '-O3' when running the program. Finally, we will often want to enable debugging (covered much later) when we are developing the program with the '-g' option. However, we often leave off the '-g' option when we used a higher optimzation setting. Two typical compilation commands that combine all of these options is given below.
```bash
$> gcc -Wall -O0 -g -o hello hello.c
$> gcc -Wall -O3 -o hello hello.c
```

### Assignment ###
Create a new source file called 'hw-01a.c' what prints out a different statement to the command line. Then compile it and name the program 'hw-01a'.

## Variables in C ##
In a programming language, a variable is used to store information. The amount of memory needed depends on the type of information being stored. For example, it requires less memory to store an integer number than it does to store a decimal number. In the C programming language you have to tell the compiler what the type of every variable you use will be. There are 5 basic types in C:
  
**`char`** - A `char` can store 1 byte, or 8 bits. A single character of ASCII text, so we most often use `char` types to hold single ascii characters. A `char` can also be used to hold a small integer between (-2^7,2^7-1) or (-128,127) inclusive.

**`int`** - An `int` is made up of multiple bytes (most often 2 or 4) and represents an integer represented in bianary. The min and max numbers that can be represented are (-2^15,2^15-1) for the 2 byte representation or (-2^31,2^31-1) for the 4 byte representation.

**`long`*** - A `long` is also an integer representation, but has to have at least 4 bytes in it.

**`float`** - A `float` is a floating point number that occupies 4 bytes of data. A floating point number is essentially a number represented in (bianary) scientific notation. That is: a number is represented as base, called the mantissa, times 2 to a power called the exponent. (*Note: this is identical to standard scientific notation with the simple swap of 2 for 10.*) In the 4 byte representation, 24 bits are used to store the mantissa and 8 bits store the exponent. This allows you to represent numbers from 10^-38 to 10^38 (positive and negative) and gives about 7 decimal places of accuracy.

**`double`** - A `double` is a floating point number that occupies 8 bytes of data. In the 8 byte floating point representation 53 bits are used to story the mantissa and 11 for the exponent. This allows you to represent numbers from 10^-308 to 10^308 and gives you about 15 decimal places of accuracy.

We say that you 'declare' a variable when you give it a type and a name. In C, the variable declaration syntax as shown below.
```c
int i; /* loop index */
double x; /* independent variable */
double a, b, c; /* quadratic coefficients */
```
You start out with the variable type followed by the variable name, finished with a semicolon. As is shown on the last line, you can declare multiple variables of the same type on the same line if you use commas to separate names.

We will often want to assign values to the variables, either when we declare them, or sometime after we declare them. This is done with the assignment operator `=` (a single equals sign).
```c
int i=0;
int j=1, k=2;
float a, b, c;
a = 1.0;
b = 3.14159;
c = b;
```
You can either assign a value to the variable when you assign it, as seen in the first two lines, or you can wait until later, as in the 4th and 5th line. You can also asign the value of a variable from another variable, as seen in the 6th line. It is strongly recommended that you assign values to all variables when you declare them. This eliminates one possible source of bugs: using unitilialized data. The following program demonstrates using uninitialized data.
```c
/* This program demonstrates using
 * an uninitialized value.
 *
 * Author : Jef Wagner
 * Date : 01-06-2014
 */
 
#include <stdio.c>

int main(){
  float a; /* declare an uninitialized variable */

  printf("a = %f \n", a); /* print the value */
  return 0;
}
```
First, if I try to compile this program, I will get a warning about using an uninitialized value. Second, I might notice different behaviour if I compile with different optimization options. That is it might behave one way if compiled with '-O0' and another when compiled with '-O3'.

Once a variable has been declared and its value determined, we will need to output that value in some what. The simplest way is using the `printf` function, which stands for formatted print. An example was used in the short program above.
```c
  printf("a = %g \n", a); /* print the value */
```
The `printf` function takes a variable number of arguments. The first argument is a string. This string should contain 'format specifier's. A 'format specifier' is a percent sign possibly followed by a number followed by a letter, and tells the computer how to format the output. For us, the imporant format specifiers are `%s` for a string, `%d` for a decimal integer, `%f` for a floating point number in decimal notation, `%e` for a floating point number, and `%g` for the shorterof the `%e` and `%f` options. (*Note: I've given you the bare minimum for using the printf statment -- you should google 'printf' to learn more about the format specifiers.*)

Variables really become useful when we start manipulating them. C allows you to do simple arthmatic will the numeric variables: negation (`-`), addition (`+`), subtraction (`-`), multiplication (`*`), and division (`/`). (*Note: Raising to a power is **not** one of the basic operations.*) Parenthesis can be used to group operations. The order of operations are the usual ones from algebra: parenthesis first, multiplication and division second, addition and subtraction third.
```c
  int a = 6, b = 10, c = 3;
 
  int d = -a; /* -6 */ 
  int e = a + b; /* 16 */
  int f = b - a; /* 4 */
  int g = a*c; /* 18 */
  int h = a/c; /* 2 */
  int i = b*c+a /* 36 */
  int j = b*(c+a) /* 90 */
```
These operations behave as you would expect for both integer types (`int` and `long`) and floating points types (`float` and `double`) with a few caveats. 

For the first caveat, you have to be careful about division with integer types. Intergers are not closed under division, when you divide two integers you get both a quotient and a remainder. For integer types, the division operator gives only the quotient. (*Note: The modulo operator (`%`) gives the remainder.*) The second caveat is what happens when the values go out of the ranges listed above. This is undefined behavior according to the C language standard, which means that it is up to the compiler writers to determine what happens and can change from compiler to compiler, or even computer to computer. It is important to make sure that your programs do not rely on the non-standard behavior.



```c
  int a = 1/3 /* 0 */
```

* Variables
x  - declare type and name: char, int, long, float, double
x  - assign value
x    - uninitialized variables
x  - print value
x  - re-assign value
x  - simple arithmatic
x    - order of operation
x    - integer division
  - explicit cast
  - implicit cast (promotion)
  - comparisons


 
