---
title: "Sizeof-Ex12:Size&Arrays in C"
date: 2019-09-29T08:44:42Z
draft: false
---

The main objective of this exercise is to learn about sizeof and how it relates to arrays.

C strings are just arrays of bytes.

Sizeof is a unirary operator and C developers are obsessed about size of everything.
In C memory size is key and you have to be keen on learning how much space is being taken up by stuff.

See the following code snippet:

```
#include <stdio.h>

int main(int argc, char *argv[])
{
        int areas[] = {10, 12, 13, 14, 20};
        char name[] = "Zed";
        char full_name[] = {'Z','e','d',' ','A','.','S','h','a','w','\0'};

        //Warning: On some systems you may have to change the %ld to %u

```
In the above code I define the arrays which am going to use. Mainly work with int and char data types. Note the
'\0' byte at the end of the char full_name array. Its quite important. Next I start the checking of size using sizeof.

```
	printf("The size of an int: %ld bytes\n", sizeof(int));
        printf("The size of areas (int[]): %ld bytes\n", sizeof(areas));
        printf("The number of int in areas: %ld \n", sizeof(areas)/sizeof(int));
        printf("The first area is %d and the last area is %d \n", areas[0], areas[4]);
        return 0;
```
After Making the above, you will get an warning about uninitialised/unused variables which is okay, just proceed to run it.
This is the result.

```
The size of an int: 4 bytes
The size of areas (int[]): 20 bytes
The number of int in areas: 5 bytes
The first area is 10 and the last area is 20 
```
The above result is straight to the point. Note that for the last statement, I started reading from 0 to 4 since in C arrays start
from 0 NOT 1.

Proceed...

In this next part I investigate the size of characters...

```
	printf("The size of a char: %ld bytes\n", sizeof(char));
        printf("The size of name(char[]): %ld bytes\n", sizeof(name));
        printf("The number of char: %ld \n", sizeof(name)/sizeof(char));
```
The above code is preety straight foward and this is what I got.

```
The size of a char: 1 bytes
The size of name(char[]): 4 bytes
The number of char: 4 
```

The last part of the code is to print put the size and content of name and full_name

```
	printf("The size of full name(char[]):%ld\n", sizeof(full_name));
        printf("The number of chars: %ld\n", sizeof(full_name)/sizeof(char));
        printf("name=\"%s\" and full name=\"%s\"\n", name, full_name);

```
And the result shall be...

```
The size of full name(char[]):11
The number of chars: 11
name="Zed" and full name="Zed A.Shaw"
```


