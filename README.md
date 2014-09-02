Basic guide for gdb
===================

#####What is gdb?

GDB is a debugger which allows the user to see what is going on in the executed program. If the written program crashes, the user can use GDB to step through the program to see why the program crashed. GDB helps the user to find and locate bugs, segmentation faults, etc. By using GDB, it is more efficient than looking for bugs on your own.

#####Starting gdb

To start `gdb`, we need a program. Using a text editor, such as `vim`, write this simple program and name it `test.cpp`

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
Make sure that `test.cpp` compiles by typing

```
$ g++ -g test.cpp
```
And then press the enter key. The `-g` flag enables debugging and will use the variables and fuctions in `gdb`.

Once `test.cpp` compiles, we will start `gdb` with

```
$ gdb ./a.out
```
By entering in this command, you now are in the `gdb` debugging program. This command does not run the program but it opens the `a.out` file in `gdb`.

The command line in `gdb` will look like

```
(gdb) 
```
You can enter commands after the `(gdb)`

#####Running the program

Now you want to run the program in `gdb`. Type `run` or `r` to run the program.

```
(gdb) run
```
Remember that the commands go after the `(gdb)`.
This runs the `a.out` that was loaded into gdb with the `gdb ./a.out` command from the terminal.
The program runs normally just `$ ./a.out`.

```
(gdb) run
Starting program: /home/csmajs/kle016/Desktop/gdb/a.out
warning: no loadable sections found in added symbol-file system-supplied DSO at 0x2aaaaaaab000
Enter first number
2
Enter second nunber
4
2 times 4 equals 8

Program exited normally.
(gdb)   
```

Another way to run the program though `gdb` is to passing arguments.
```
r arg1 arg2
```

This runs the program with `arg1` and `arg2` already in place

#####Breakpoints

You can create breakpoints in `gdb`. A breakpoint causes a pause (break) in the program when it reaches a certain point.

To use breakpoints, type `break` or `b` in the `gdb` command line followed by the line number that you want to pause (break) at.

```
(gdb) break 10
Breakpoint 1 at 0x40092d: file test.cpp, line 10.
```
As you can see, it creates a breakpoint on line 10.

When you `run` the program, it will output

```
(gdb) run
Starting program: /home/csmajs/kle016/Desktop/gdb/a.out
warning: no loadable sections found in added symbol-file system-supplied DSO at 0x2aaaaaaab000

Breakpoint 1, main () at test.cpp:10
10      cout << "Enter first number" << endl;
(gdb)
```
Notice how the program pauses here at line 10. Line 10 has not been executed yet. It is because the breakpoint was set here on line 10, so it paused the program on line 10.

This is useful for because it suspends other lines of code from executing so that you can inspect the variables and exection of the program.

If you want to continue the program, type in `continue` in the command line

```
(gdb) continue
Continuing.
Enter first number
```

By typing in `continue` in the command line, the program will execute from the breakpoint, which is line 10. The program executes line 11, which is `Enter first number`.

You can make multiple breakpoints in the program through `gdb`. To make another breakpoint in the program, type `break point` followed by the line number. By setting another breakpoint, you are able to pause at another line in the program.

```
(gdb) break 12
Breakpoint 2 at 0x400957: file test.cpp, line 12.
```
Now there are two breakpoints in `test.cpp`. Now run the program from `gdb` by ttyping `run` in the command line

```
(gdb) run
Starting program: /home/csmajs/kle016/Desktop/gdb/a.out
warning: no loadable sections found in added symbol-file system-supplied DSO at 0x2aaaaaaab000

Breakpoint 1, main () at test.cpp:10
10      cout << "Enter first number" << endl;
(gdb)
```
The program paused at `Breakpoint 1`, which is the first breakpoint. To continue on to the next breakpoint, type `continue` in the command line. The program will continue until the next breakpoint, which is line 12.

```
(gdb) run
Starting program: /home/csmajs/kle016/Desktop/gdb/a.out
warning: no loadable sections found in added symbol-file system-supplied DSO at 0x2aaaaaaab000

Breakpoint 1, main () at test.cpp:10
10      cout << "Enter first number" << endl;
(gdb) continue
Continuing.
Enter first number
6

Breakpoint 2, main () at test.cpp:12
12      cout << "Enter second nunber" << endl;
(gdb)       

If you want to see all the breakpoints that you have made, type `info break` into the command line.

```
(gdb) info break
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040092d in main() at test.cpp:10
        breakpoint already hit 1 time
2       breakpoint     keep y   0x0000000000400957 in main() at test.cpp:12
        breakpoint already hit 1 time
(gdb)      
```


To delete a breakpoint, type `delete N`, where `N` is the breakpoint number.

```
(gdb) delete 2
(gdb) info break
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040092d in main() at test.cpp:10
        breakpoint already hit 1 time
(gdb)    
```
As you can see, we deleted 2, which was breakpoint 2. Then we used `info break` to confirm that it has been deleted.






You can also set breakpoints on fuctions. To set breakpoints on fuctions, you need to type out the name of the fuction right after the `break`

```
(gdb) break nameofthefuction
```

What this does is that it pauses that this fuction, just like how it paused when we used `break`.


