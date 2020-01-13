---
title: "Pointers To Functions In C"
date: 2020-01-07T15:47:42+03:00
draft: true
---

Functions are actually pointers to a spot in a program. The syntax is:

```
int (*POINTER_NAME)(int a, int b)

```
The process for creating a pointer is as follows:

* Write a normal function declaration: ``` int  callme(int a, int b)```
* Wrap the function name with the pointer syntax: ``` int(*call_me)(int a, int b)```
* Change the name to the pointer name: ```int (*compare_cb)(int a, int b)```

 
We are going to start off by creating the bubble sort function pointer.

```
int *bubble_sort(int numbers, int count, compare_cb cmp)
{
        int temp = 0;
        int i = 0;
        int j = 0;

        int *target = malloc(count * sizeoff(int));
        if (!target)
                die("Memory Error")

        memcpy(target, numbers, count * sizeof(int));

        for (i = 0; i< count; i++){
                for(j = 0; j<count - 1; j++){
                        if (cmp(target[j], target[j+1]) > 0) {
                                temp = target[j+1];
                                target[j+1] = target[j];
                                target[j] = temp;

                                }

                }

        }

        return target;
}

```
It looks like a complex function but I we shall break into parts to understand it. The bubble sort
function pointer takes in numbers, count and cmp as its arguments. We start the function by declaring
3 variables: temp, i and j all in integer data type. We then declare a pointer of type int which is
pointing at the result of ```malloc(count * sizeoff(int))```. If the result is NOT Logicaly target, then
call the die function to print an error. This is to check that the memory was created successfully.

The next line is where we use the memcpy function: ``` memcpy(target, numbers, count * sizeoff(int))```
The C library function memcpy: void *memcpy(void *str1, const void *str2, size_t n) copies n characters 
from memory area str2 to memory area str1. The parameters are as follows:

* str1 - This is a pointer to the destination array where content is to be copied to, type-casted to 
a pointer of type void*
* str2 - A pointer to the source of data to be copied, type casted to a pointer of type void*
* n - Number of bytes to be copied.

So in our case, the target is the pointer to the destination array. numbers is the pointer to the source
of data and count * sizeof(int) is the data size in bytes. This function returns a pointer to a destination, 
which is str1

Next we have some loops which do the ounting.

The next set of 3 functions are do the sorting. Namely sorted_order, reverse_order and strange_order.

The next funtion does the sorting and prints it out. Let us examine it in more detail:

```
void test_sorting(int * numbers, int count, compare_cb cmp)
{
        int i = 0;
        int *sorted = bubble_sort(numbers, count cmp);

        if (!sorted)
                die("Failed to sort as required");
        for (i = 0; i<sorted; i++){
                printf("%d", sorted[i]);
        }
        printf("\n"
        free(sorted)
        }
}

```
This sort function is really a test so that we are sure that the sorting function is being done correctly. It takes in
4 parameters namely: numbers, count, compare_cb and cmp



