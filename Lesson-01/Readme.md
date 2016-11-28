Lesson 01
=========

## Contents

* Introduction
  - text-file -> program
    * first source file : hello world!
    * command line compilers
    * compile and run
  -Analyse program
    * comments
    * includes
    * main function/subroutine
    * printf statement
  - command line options
    * output name
    * enable warnings
    * enable debugging
    * enable optimizations
 
* Assignment: change message and output name

* Variables
  - declare type and name: char, int, long, float, double
  - assign value
    - uninitialized variables
  - print value
  - re-assign value
  - simple arithmatic
    - order of operation
    - integer division
  - explicit cast
  - implicit cast (promotion)
  - comparisons
  
* Assignment: make a simple program that demonstrates:
  - integer arithmatic
  - integer overflow with `char`s
  - floating point arithmatic
  - invalid comparisons using floating point numbers
  - invalid arithmatic with integer division (common problem)
  - fix of invalid arithmatic using explicit cast
  
* Slightly fancier math using the math.h library
  - include math.h in file
  - trig, hyperbolic trig, inverses
  - sqrt, hypot
  - log, exp, pow
  - note: don't use the pow function if something else works
  
* Assignment: make a simple projectile motion program:
  - The inputs will be:
    * initial velocity
    * initial height
    * initial angle
  - Calculate and output:
    * max height
    * time of flight
    * distance traveled
    * angle of impact
    
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
(*Note: In the unix environment, executable programs have no extension.*) There are several other command line options that we will want to know about. For now, we will focus on adding just a few. First is the '-Wall' option. This turns on all possible warnings (-W for warning, then all; not the word wall). A warning is something the that will compile, but is often the result of a mistake - most often for me at least for leaving out semicolons. Next is the '-O0', '-O1', '-O2', '-O3' (that is dash capital O, then a number, not dash then the numeral 0). This enables or disables optimizations. You will often want to use '-O0' or '-O1' when you are writing the program, then switch to '-O2' or '-O3' when running the program. Finally, we will often want to enable debugging (covered much later) when we are developing the program with the '-g' option. A typical compilation command the combines all of these options is given below
```bash
$> gcc -Wall -O0 -g -o hello hello.c
```

### Assignment ###
Create a new source file called 'hw-01a.c' what prints out a different statement to the command line. Then compile it and name the program 'hw-01a'.



 
