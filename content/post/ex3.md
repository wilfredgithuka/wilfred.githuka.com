---
title: "Exercise3: Formatted Printing"
date: 2019-08-28T09:59:45+03:00
draft: flase
---
In the previous exercise It was all about using Makefiles to build. Now its
all about printing stuff.

The code for this exercise is preety straightforward but contains an important function. Have a look:

```
#include <stdio.h>

int main()
    {
        int age = 10;
        int height = 72;
        
        printf("I am %d years old \n", age);
        printf("I am %d inches tall \n", height);
            
        return 0;
        
    }

```
This code base uses some basic implementations. We start by loading the stdio header
files then creating our main function. This code does not have other functions apart 
from the main function. 2 Variable declarations follow then we call the printf function
to print the values stored in the variables.

### printf

When you ```man printf``` you realise that its simply for formating and printing data. Printf has
many options which can be relased by issuing the following command:

```
printf --help
```

## Example

Here is an example of the cool usage of printf which I got from [Tutorialspoint](https://www.tutorialspoint.com/c_standard_library/c_function_printf.htm)

```
#include <stdio.h>

int main()
    {
        int ch;
        for (ch = 75; ch <= 100; ch ++)
            printf("ASCII value = %d Char value = %c\n, ch, ch);
        }
        
    return 0;
    
    }

```

Printf has many fuctions and I would suggest you ```man printf``` anytime you have an issue.

* [Exercise 4](https://www.wilfred,githuka.com/post/ex4/)
* [Exercise 3](https://www.wilfred.githuka.com/post/ex3/)
* [Index Page](https://www.wilfred.githuka.com/post/lcthw-index/)
