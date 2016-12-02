Lesson 02
=========

## C memory model ##

Before we start, lets go over a very simple model of how computers work. Computers involve two things, a processor and memory. The processor can execute certain actions such as copy data from one part of memory to another, or add to numbers together. In order to know what action to perform the processor has to read an instruction from memory. However, in addition to the instructions, the memory must hold all of the data that the computer will manipulate in its program. In the von Neumann archetecture the memory accessable to the computer is divided neatly into two parts: one part that holds the instructions for the processor and one part that holds the all of the data. In order to write efficient fast code in C you have to understand how memory is organized in a C program. C follows the von Neumann archetecture but even further divides the data section into 3 different sections. The including the memory for instructions, the four sections of memory in a C program are:

**text** - This section holds all of the instructions for the processor.

**data** - This sections containts the data known at compile time. global constants and literals.

**stack** - Holds the data that is allocated through variable declarations. When a function is called

**heap** - Holds the data that is allocated manually.

In order to write efficient C, it is imporant to know where variables from each type of memory will go.

## Constants ##
  
* Constants
  - Literals
    - Define pragma
  - Global constants 
