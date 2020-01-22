---
title: "Exercise 2: Using Makefiles to Build"
date: 2019-08-27T14:41:32+03:00
draft: false
---

Make has been around for a while. In software development, Make is a build automation tool 
that automatically builds executable programs and libraries from source code by reading files 
called Makefiles which specify how to derive the target program. Though integrated development 
environments and language-specific compiler features can also be used to manage a build process, 
Make remains widely used, especially in Unix and Unix-like operating systems. 

Read: ```man make``` for more information.

Make works by reading instructions from the Makefiles.

In this exercise I created a Makefile, used Make and compiled a C program.

This is an example of a Makefile:(TAB Characters only)

```
CFLAGS=-Wall -g

all: ex1

clean:
    rm -f ex1
```

In C when you want to compile a program, just issue the below code:

```
make ex1
```
At this point, make goes through that folder, looks for any source file with a smilar name and compiles it to object code.
This is done preety fast since Make is old and it know quite a large number of programming languages. You can get away by
running Make XYZ only but as yor program becomes more complex, that when you require a Makefile, like above.

There is so much you can do with make and make files. Just read the manual :-). Its just implied dependancy and ancient lore.

* [Index Page](https://wilfred.githuka.com/posts/index-lcthw/)
* [Exercise 3: Formatted Printing](https://wilfred.githuka.com/posts/ex3/)
* [Exercise 1: Dust off that compiler](https://wilfred.githuka.com/posts/ex1/)
