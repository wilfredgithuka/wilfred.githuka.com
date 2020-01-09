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
pointing at the result of ```malloc(count * sizeoff(int))```

