---
title: "Exercise 1: Dust off that Compiler"
date: 2019-08-25T14:16:09Z
draft: false
---
In this second exercise, its all about writing code and seeing what happens.
Click here for the tutorial's index page.

This is the code snippet for this exercise.

```
#include <stdio.h>

/*This is a comment*/
int main(int argc, char *argv[])
{
int distance = 100;

//This is another comment
printf("You are %d miles away \n", distance);

return 0;

}

```

## Compiling

To compile it you have to use make. GNU Make is a tool which controls the generation of executables and other non-source files of a program from the program's source files. Make gets its knowledge of how to build a program from a file called the makefile, which lists each of the non-source files and how to compute it from other files. When you write a program, you should write a makefile for it, so that it is possible to use Make to build and install the program.

But for now we shall not create/modify our make file.

```
make ex1
```
Before we execute our program we need to check for errors(debug) using a special tool called lldb. The LLDB Debugger (LLDB) is the debugger component of the LLVM project. It is built as a set of reusable components which extensively use existing libraries from LLVM, such as the Clang expression parser and LLVM disassembler. LLDB is free and open-source software.

```
lldb ex1
```
When it reports no errors, then you can exectute the program. To exit from lldb, just type: exit and hit enter.

```
./ex1

You are 100 miles away
```

## What I've Learnt

First of all by running:

```
man printf
```
I got to realise that it was developed by MacKenzie and it takes a variety of parameters. To check how printf works, I shall run the above
code but remove the last variable parameter and see what my program tells me. Here we go...

```
printf("You are %d miles away \n");
```
The compilation stage passes with no errors. I then execute it to see what happens. This is the result I get.

```
You are -969057704 miles away
```
The reason why I get the negative result is because printf and C operate on raw memory. In C there is no virtual machine
that protects the programmer from such errors. Its Raw memory as it is. Because C expects there to be a parameter it find
nothing so returns whatever memory is available at the expected point. That is how raw things get here.

I then check with lldb on whats happening inside.

## Index

* [Exercise 2](https://www.wilfred.githuka.com/posts/ex2/)
* [Exercise 0](https://www.wilfred.githuka.com/posts/ex0/)
* [Index Page](https://www.wilfred.githuka.com/posts/lcthw-index/)
