---
title: "Exercise 0: The Setup"
date: 2019-08-25T13:56:08Z
draft: false
---
This is ground zero for the tutorial. But before starting any developent using C, you need to prepare your computer
to make sure you have the necessary tools. This tutorial is for an Archlinux machine, which am using.

The Linux kernel and the GNU userland are written primarily in C. Arch Linux uses the GNU C Library (glibc) as the 
C standard library; it is a dependency of the base meta package. You can use the GNU toolchain or the LLVM toolchain 
to develop software in C, C++ or Objective-C.

On Linux, preferably Archlinux, there is a [good documentation](https://wiki.archlinux.org/index.php/C) on required tools.


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
* I also recommend installing [man pages](https://wiki.archlinux.org/index.php/Man_page). They come in-handy when you want to understand what certain terms mean.

```
sudo pacman -S man man-page man-db
```
Now all is ready for writing programs in C.

Next >> [Exercise 1: Dust off that compiler](https://wilfred.githuka.com/post/ex1/).
Index >> [Index](https://wilfred.githuka.com/post/index/)
