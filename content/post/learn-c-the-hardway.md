---
title: "Learn C the Hardway - Introduction & Lesson 1"
date: 2017-11-20T15:05:47+03:00
subtitle: "52 Days of Self Discipline To Learn Good Old C"
tags: [c, c++, learning, self-study, python]
draft: "True"
---
![image](/img/c/intro.JPG)
Last year at around the same time I began my journey into Python. Its been a
year so far and am pleased with my progress. Now for the next year am starting
another journey in C

C is a general purpose computer programming language developed by 
Dennis Ritchie back in  1969-1973 at Bell Labs. Its an imperative programming 
language and designed to be compiled using a relative straightforward compiler 
to provide low level access to memory.

### Why Study C?

I made this choice since am in the electronics field and I would like to have
a low level understanding of the computer/electronic system. Also as I dive 
into the self driving car world, I would like to have a deeper understanding 
of a system and able to manipulate if using code. Lastly since I use C++ once 
in a while I feel that to master programming, one needs a dose of C. 
Just my thoughts.

### Which Book?

I used learnpythonthehardway when learning Python. I plan on using
learncthehardway to learn C. I have some reference books in my library to 
enforce my study. The book has 52 Lessons which I will publish them on my site
as I progress.

### Spacemacs Baby :-)

I just got my feet wet in spacemacs(emacs) and I will forcemyself to use it
so that I can get myself into into it and off the mouse.

### Your Strategy?

I am using a unique strategy which I have called #NoNet. This means no internet
as much as possible. Its a rule that will teach me to go back to books to 
solve problems and learning how to solve them other than googling the error and
stackoverflowing the result. If there is no answer on the books(which I doubt)
its when I will consult myself.

### Exercise1: Dust Off That Compiler

This exercise is about using variables and data types. You can download my code 
below ex1.c

#### Code

include <stdio.h>
/*This is a comment*/
int main (int argc, char * argv)
{
 int distance = 100;
 
 //This is also a commnent
 
 printf("You are %d miles away .\n", distance);
 printf("I love you this much %d \n", distance);
 printf("This is the distance for today %d \n", distance);
 printf("The distance for today is %d \n", distance);
 printf("The best distance for today is %d \n", distance);
 
 return 0;
}

### Assignment

* Write the code as it
* Change or delete random parts and see what happens
* Print out 5 times of different texts and see what happens
* Check out man printf and read it
* For each line write out the symbols that you dont understand.

### Explanation

Here is a neat explanation of whats going on. I will explain the really
crucial parts in the program.

#### include <stdio.h>

In C this means take the contents of the header files into this source file.

#### int main (int argc, char * argv)

Programs in C run in a very interesting way. The OS first runs the main
function and for the function to be totally complete it needs to return
an int and take 2 parameters: an int for the argument count and an 
array of char* strings for the argument.

#### int distance = 100;

This is avariable declaration which follows the type name = value; 
syntax.

#### curly braces {block}

In C block are represented using the curly braces.

### Spacemacs

* ESC-m-f-s : Save a document

See you in exercise 2

Code written at Java Westlands. Masala tea at Java is Ksh.170. Totally worth 
it :-)
