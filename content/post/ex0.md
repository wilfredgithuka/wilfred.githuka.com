---
title: "Exercise 0: The Setup"
date: 2019-08-25T13:56:08Z
draft: false
---
This is ground zero for the tutorial. But before starting any developent using C, you need to prepare your computer
to make sure you have the necessary tools. This tutorial is for an Archlinux machine, which am using.

### Installation

* To start with ensure that your system is up to date

```
pacman -Syu
```

* Install the [base-devel package](https://www.archlinux.org/groups/x86_64/base-devel/). Base-devel has 26 items which are necessary for
C-type development.

```
paman -S base-devel
```
* Now check that you have the GNU C compiler. The GNU Compiler Collection includes front ends for C, C++, Objective-C, Fortran, Ada, Go, and D, as well as libraries for these languages (libstdc++,...). GCC was originally written as the compiler for the GNU operating system. The most updated version is GCC 9.2 released [2019-08-12].
```
cc --version
```

Now all is ready for writing programs in C.

Lets go to Exercise 1: Dust off that compiler.
