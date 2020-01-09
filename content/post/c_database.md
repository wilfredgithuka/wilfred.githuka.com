---
title: "A Simple Database in Plain Old C"
date: 2019-12-12T11:15:35+03:00
draft: false
---
C might be regarded as an old low level langage but it actually is very powerful.

A databse can be created very easily in C. The following is a manual on how to create a simple database in C.

This code is available in my github repo :-)


## Heap vs Stack Allocation

Understanding the difference between heap and stack is very important for this tutorial.

A chunk of RAM can be on heap or stack. 

Stack is a special region in memory that is used by functions to store variables which
when the function ends its cleared up by C. When you have too much data on stack, you will
get a stackoverflow error

Heap is memory created by malloc() and it returns a pointer to it. When you are done with it
you must free it with free() to return it to the OS, failure to do so will cause a program
to leak memory.

## Importing Necessary Tools

For this program we shall require to import the following:

```
#include <stdio.h>
#include <assert.h>
#inlcude <stdlib.h>
#include <errno.h>
#inlcude <string.h>
```

## Constants

We now get to set some very important constants which shall be MAX_DATA and MAX_ROWS as follows:

```
#define MAX_DATA 512;
#define MAX_ROWS 100;
```

## Structs

This database shall have 3 structs. A struct in C is simply objects which really dont have
functions in them. If you make a pointer to it, you use the -> arrow as you shall see later.
A structure has elements in it and it can be called a compound data type since it contains more
than one data type.

The Address struct has 4 elements of which name and email have max info on them.

```
struct Address {
        int id;
        int set;
        char name [MAX_DATA];
        char email [MAX_DATA];
};

```
This Database struct is essentially for accessing the database, and it has one element.

```
struct Database {
        struct Address rows[MAX_ROWS];
};

```
Finally the Connection struct is the most important since its used everywhere to handle connections.

```
struct Connection {
        FILE *file;
        struct Database *db;
};

```
## Die Function

We shall start off with the die function, its primary role is to handle error messages.
This function has an if statement which first prints out the perror message. Note that 
this perror is the C library: function void perror(const char *str) that prints a descriptive 
error message to stderr. First the string str is printed, followed by a colon then a space.

```
void die(const char *message)
{
        if (errno){
                perror (message);
        }else{
                printf("ERROR: %s\n", message);
        }
        exit(1);
}

```
However the next piece of code ensure that it can also print a specific message 'ERROR' + message.
I started off with the die function since its utilised by all major functions in the code.

## Address_print (Heap)

Next we have the Address_print function. Its role is to print out the addresses as assiged to the Address structure.

When you pass in a structure and use the *notation on a function then this is a heap, without it it becomes a stack.

Here we are using heap to move around structs that need to be shared accross functions.

```
void Address_print(struct Address *addr)
{
        printf("%d %s %s\n", addr->id, addr->name, addr->email);

}
```
Here we use the -> notation to access the Address Struct and print out the id, name, and email.
One of the parameters of the function is a pointer addr. By adding the *addr, we are de-referencing the pointer
so as to return the value of what addr is pointing to. 

So here when we call printf function, it shall simply print the id which shall be in addr pointer, name and email. All with their specific data types.

To get what value is being held in that pointer, just add a *addr to it.(de-referencing)

## Main Function

We shall now create a main function to test that our program is working well.

```
int main(int argc, char *argv[])
{
    if(argv < 3)
        die("USAGE: ex17 <dbfile> <action> [action params]");

        return(0);

        int addr = 10;
        Address_print(addr);
        
}

```
This function just checks that you have entered anything for argv and throws an error to tell you. Nuthing much, moving on...
With no errors, our database is okay, lets move to the next step.

# Step 2

## Databse_create

When we talk of a database, the key part is creating the database. So we shall start with the function that is responsible for that.
We shall call it: Database_create

```
void Database_create(struct Connection *conn)
{
        int i = 0;

        for(i = 0; i < MAX_ROWS; i++);
        {
                //make a prototype to initialise it
                struct Address addr = {.id = i, .set = 0};
                //then just assign it
                conn->db->rows[i] = addr;
        }
}

```

This function has the parameters struct Connection *conn. This is heap. Inside the function there is a variable declaration
which is used to check for the size of MAX_ROWS.

If you look carefuly you will notice that we are creating an address and setting the default values, and since we are not
using a *notation, then this is a stack. Stack means that this memory is created in RAM and once this function exists, then
the memory is deleted likewise. You dont have to free that memory.

Then the last statement simply used the pointer conn to go into the pointer db which has rows of i which is given to addr.

Before I compile the code I need to call the function Database_create in the main function for me to see results. However in the
main function, Database_create is called using an Case statement. When I call the function Database_create, I have to pass to it
a parameter conn like this:

```
Database_create(conn)
```
At this moment C does not know what conn is so we have to define conn. Conn is a pointer. Here is how the main function looks like:

```
int main(int argc, char *argv[])
{
        if(argv < 3)
        die("USAGE: ex17 <dbfile> <action> [action params]");

        char *filename = argv[1];
        char action = argv[2][0];

        struct Connection *conn = Database_open(filename, action);

        switch (action) {
                case 'c':
                        Database_create(conn);
                break;
        default:
                die("Invalid action");

        }

        return(0);

}

```

We define *conn as:

```
struct Connection *conn = Database_open(filename, action);

```
The value of *conn is the result of Database_open(filename, action)

Therefore for our main function to work we have to create a Database_open function.

## Database_open

The Database_open function is primarily to open the database. It looks like below:

```
struct Connection *Database_open(const char *filename, char mode)
{
        struct Connection *conn = malloc(sizeof(struct Connection));
        if (!conn)
                die("Memory Error");
        conn->db = malloc(sizeof(struct Database));

        if (!conn->db)
                die("Memory error");
        if (mode == 'c'){
                conn->file = fopen(filename, "w");
        }else{
                conn->file = fopen(filename, "r+");
                if (conn->file){
                Database_load(conn);
                }
        }
        if (!conn->file)
                die("Failed to open the file");
        return conn;

}

```
This function take in two parameters: a pointer of type char which is constant and a mode variable of type char.

We first start by creating a struct Connection on heap with the pointer *conn. Remember *conn is now pointing to
memory created by malloc which is the size of the struct Conection. Since we put the * on conn, we are simply de-referencing
the pointer such that instead of getting the address to the memory location, we are returning the contents of that memory.

The next step is to check wether the memory creating was successful.

We also create a Database struct on heap again using malloc. After that we use an if statement inserting a (!conn) Logical Note to
see wether the pointer conn is linked to db, if Not then call die function and give an error. However is mode is equal to c that when 
the user inserts a c for database create(c is declared in the Case statement in the main function), then the file open is executed.

When you open a file using fopen(), The C library function FILE *fopen(const char *filename, const char *mode) opens the filename pointed to, by filename using the given mode. The usage is as follows:

```
FILE *fopen(const char *filename, const char *mode)
```
The follwing parameter must be given for the function fopen:

* filename − This is the C string containing the name of the file to be opened.
* mode − This is the C string containing a file access mode. It includes −

* "r" - Opens a file for reading. The file must exist.
* "w" - Creates an empty file for writing. If a file with the same name already exists, its content is erased and the file is considered as a new empty file.
* "a" - Appends to a file. Writing operations, append data at the end of the file. The file is created if it does not exist.
* "r+" - Opens a file to update both reading and writing. The file must exist.
* "w+" - Creates an empty file for both reading and writing.
* "a+" - Opens a file for reading and appending.

So when the user appends a 'c' the the file can be opened in "w" thats creating a an empty file or "r+" reading and writing. This is awesome.
We the proceed to call Databse_load function and pass to it the pointer conn.

This function ends by returning conn.

Let us create the Database_load function.

## Database_load

The Database_load function is used to load a database. It takes in the Struct Connection *conn pointer as its parameter.

```
void Database_load(struct Connection *conn)
{
        int rc = fread(conn->db, sizeof(struct Database), 1, conn->file);
        if (rc != 1)
                die("failed to load database");

}
```
We then create an rc variable of type int and store into it the value returned by fread(). fread() is a function that reads data from a given
stream into the array pointed to by a pointer. The fread() here takes in 4 parameters:

* conn->db - pointer linkage.  This is the pointer to a block of memory with a minimum size of size*nmemb bytes.
* sizeof(struct Database) - This is the size in bytes of each element to be read.
* 1 - This is the number of elements, each one with a size of size bytes.
* conn->file - This is the pointer to a FILE object that specifies an input stream.

The next line of code is to check whether the value of rc is NOT equal 1 then call die function, to print the error message.

With all those functions in place, its time to test our databse program. We first compile it

```
make ex17_Database_create
```
Then execute with the following parameters

```
./ex17_Database_create test.db c
```
The 'c' is for create. When you exectute this program, the int argc contains 'test.db' and char argv[] contains 'c' in the main function. 
At this point in this line:

```
struct Connection *conn = Database_open(filename, action);
```
Database_open is called and the filename and action are passed onto it. The function returns a value which is stored in the Struct Connection *conn pointer.
Since the file does not exist, in the Database_open function, it shall execute using the "w" option to create the file. The last section called the Database_create since
the 'c' option was selected in the Case. 

## Step 3



