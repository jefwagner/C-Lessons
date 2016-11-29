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
 
  - Assignment: change message and output name

* Variables
  - declare type and name: char, int, long, float, double
  - assign value
    - uninitialized variables
  - print value
  - simple arithmatic
    - order of operation
    - integer division
  - comparisons
  - implicit cast (promotion)
  - explicit cast

  - Assignment: make a simple program that demonstrates:
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
  
  - Assignment: make a simple projectile motion program:
    - The inputs will be:
      * initial velocity
      * initial height
      * initial angle
    - Calculate and output:
      * max height
      * time of flight
      * distance traveled
      * angle of impact
