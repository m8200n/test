
Basic guide for gdb
===================

#####What is gdb?

GDB is a debugger which allows the user to see what is going on in the executed program. If the written program crashes, the user can use GDB to step through the program to see why the program crashed. GDB helps the user to find and locate bugs, segmentation faults, etc. By using GDB, it is more efficient than looking for bugs on your own.

#####Starting gdb

To start gdb, we need a program. Using a text editor, such as vim, write this simple program and name it test.cpp

```
#include <iostream>

using namespace std;

int main()
{

int x = 2;
int y = 3;
int z = 2*3;
cout << "This is a test!" << endl;
cout << x << " times " << y << " equals " << z << endl;

return 0;
}
```
Make sure that test.cpp compiles by typing

```
$ g++ -g test.cpp
```
And then press the enter key. The -g flag enables debugging and will use the variables and fuctions in gdb.

Once test.cpp compiles, we will start gdb with

```
$ gdb ./a.out
```
By entering in this command, you now are in the gdb debugging program. This command does not run the program but it opens the a.out file in gdb.

The command line in gdb will look like

```
(gdb) 
```
You can enter commands after the `(gdb)`

#####Running the program

Now you want to run the program in gdb. Type `run` or `r` to run the program.

```
(gdb) run
```
Remember that the commands go after the `(gdb)`.
This runs the `a.out` that was loaded into gdb with the `gdb ./a.out` command from the terminal.
The program runs normally just `$ ./a.out`.

Another way to run the program though gdb is to passing arguments.
```
r arg1 arg2
```

This runs the program with `arg1` and `arg2` 

#####Breakpoints


