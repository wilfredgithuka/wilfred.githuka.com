---
title: "Structs & Pointers in C "
date: 2019-07-22T10:23:29Z
draft: false
---
In the simplest of terms, an array can hold info of a single data type while
a struct (user defines)can hold data of different data types.

In this example, you will need to #include:

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <assert.h>
```

### Defining a Struct

Struct definition is the first step before one can start working with it.
Note that my struct has more than one data type which is different from
arrays which have one data type. Structs are like objects but they really dont have functions in them.

When creating the struct, you need to have the struct keyword and the name
of the struct which is the tag/structure tag.

```sh
struct Person {
char *name;
int age;
int height;
int weight;
} 

```
In the above struct, one of the members (*name) is a pointer. Not that this member points to the memory address of where the name is and NOT to the name itself.

```c
struct Library {
char author_name;
char title;
char subject;
int isbn;
}

```
### Creating the structures using functions

So now that we have defined the struct which has 4 elements or members. I will use a function to create the structures from raw memory using malloc. Remember a computer has limited RAM memory where malloc create the memory from. Memory created or given must be destroyed or returned. The memory created is not initialized, and thus remains with indeterminate values. 

The malloc() function reserves a block of memory of the specified number of bytes. And, it returns a pointer of type void which can be casted into pointer of any form.

```sh
struct Person *Person_create(char *name, int age, int height, int weight){

struct Person *who = malloc(sizeof(struct Person));
assert(who != NULL);

who->name = strdup(name);
who->age = age;
who->height = height;
who->weght = weight;

return who;

}

```
In the above snippet I create a function with 4 arguments: name, age, height and weight. I then call malloc to give me a chunk of memory(RAM) the size off Person which is the struct. Afterards I use the assert just to make sure that the memory is valid. The assert is basically checking to make sure that malloc did not return a NULL invalid pointer. The assert.h can help programmers find bugs in their programs or even handle exceptional cases via a crash that will spit put debugging info.

```sh
man assert.h
```
### De-Referencing a Pointer-> & Element vs dot 

* dot : Not a pointer
* ->  : When its a pointer

In my above example I use malloc which gives me the memory. I then use *who to
get the address of the memory that I have been given. The *who is a pointer so to access this memory I cannot just directly say who.name which would work fine 
in OOP programming. I have to find a way to link to a pointer.

```
who->name = strdup(name);
```
The arrow -> notation is the simplest way to de-reference a pointer so that we
can use it in the struct. If you try to use the dot way ie: who.name the compiler will throw errors. Also the strdup(name) is a string duplicate which duplicated the name and also gets the address of it.

```
man strdup
```

The  strdup() function returns a pointer to a new string which is a du‐plicate of the strings.  Memory for the new string  is  obtained  with malloc, and can be freed with free.

### Destroy

Every chunk of memory created must be destroyed or freed. So I have a function called Person_destroy to do exactly that.

```
void Person_destroy(struct Person *who)
{
assert(who != NULL)

free(who->name);
free(who);
}
```
In this function I also use the assert tool just to confirm that the memory does not return a null pointer.

### Creating The Actual Structures

What I was doing up there was defining the structures, now in the main menu I create actual structures with actual data.

```
struct Person *wil = Person_create("Wilfred Githuka", 32, 64, 140);
struct Person *vic = Person_create("Victoria Marine", 20, 72, 180);
```
The above code snippet creates a memories for wil and vic. The structs now exists in memory which is pointed by *wil and *vic. I can now where wil and vic exist and can also know the contents. This can be accomplished in 2 ways:

* Print the memory address of the pointer *wil
* Print the contents of wil by using the function: Person_print

#### Print memory location of *wil and *vic

```
printf("Wilfred is at memory location %p\n", wil);
printf("Victoria is at memory location %p\n", vic);
```
In C %p is a format specifier which is used if we want to print data of type (void *) i.e, in simple words address of pointer or any other variable . 
The output is displayed as a hexadecimal value.

Result...

```
Wilfred is at memory location 0x55577d6d2260
```
#### Print out the memory contents of wil and vic

```
Person_print(wil);
Person_print(vic);
```
### Destroy all of them

Just as I had created the names in the struct Person, I can and have to destroy them
so that the program can close well. This is how to do it.

```
Person_destroy(wil);
Person_destroy(vic);
```
## Breaking It

### 1. Passing NULL to Person_destroy

In this attempt to kill the program, I will attempt to pass NULL to the Person_destroy function.
```
void Person_destroy(NULL)
{
assert(who != NULL);

free(who->name);
free(who);
}

```
#### Result

After compiling it, it throws an error. Completey destroyed :-)

```
ex16_starting.c:29:21: error: expected declaration specifiers or ‘...’ before ‘(’ token
   29 | void Person_destroy(NULL)
      |                     ^~~~
ex16_starting.c: In function ‘main’:
ex16_starting.c:70:3: warning: implicit declaration of function ‘Person_destroy’ [-Wimplicit-function-declaration]
   70 |   Person_destroy(wil);
      |   ^~~~~~~~~~~~~~
make: *** [<builtin>: ex16_starting] Error 1

```

### 2. Forget to call Person_destroy at the end.

In this attempt I will 'forget' to give back or destroy the memory and see what will happen. I will do this
by simply commenting out the call functions at the end of the code. I will also run this under a debugger to see what it shall report.

## References

* [Learn C The Hard Way](https://learncodethehardway.org/c/)
* [Wikipedia's Article on C Structs](https://en.wikipedia.org/wiki/Struct_(C_programming_language))
* [GeeksforGeeks](https://www.geeksforgeeks.org/structures-c/)


