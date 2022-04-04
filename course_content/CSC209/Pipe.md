---
layout: articles
tags: CSC209
---
# Pipe

## Lower IO

Beyond the pipe, we only learn how to use functions like `fopen`, `fclose`, `fgets`, `fprintf`, `fwrite` ... to operate on streams using the `FILE` objects. Those kinds of function helps us to easily to do IO operation we want, but hide some of complexity of the actual IO system calls.

Firstly, before we open or do any operation for any files. There are three files automatically opened: `stdin`, `stdout`,and `stderr`. That is, whenever we open a new file the file descriptor always `>=3`. 

-    `stdin` stands the standard input(something like `scanf`, or the input from the command line) usually with descriptor `0`, 
-   `stdout` stands the standard output(something like `printf`) with descriptor `1`, 
-   `stderr` stands the standard errors(we somehow use often call when we want to warning errors when open,read or close files) with descriptor `2`.

Notice, the descriptor is one field in a `FILE` struct, also is the index of the `FILE`, and children inherits all open files descriptors.

## Pipe

`pipe(int * fd):`  `fd` is a length 2 int array.

In the process model module, we talk about how a process call another process so that they can work simultaneously to enhance our efficiency. We can use `fork` to have a children process or use `excel` to change program to run.

`Pipe` is a kind of communication mechanism we can use to transfer data between related processes. And it takes an array of two file descriptors. One for reading(index 0), one for writing(index 1). Here, the reading is for the other process to read from pipe, and writing is this process write stuff into pipe. And also **pipe is a data structure**.

Notice:
- The maximum bytes of pipe is `64kb`,
- If the pipe is close, the `read` from pipe will be 0 to indicate no more data to read.
- `pipe` should call before `fork` since child inherits open file descriptors from the parent.
- `read` for `pipe` will holding 'till all writing descriptors are close.
- We have to call `fork` after `pipe` for the pipe to have the right file descriptors open in both processes. 
- If we have multiple children and multiple pipe for those children, notice if one of those process holding pipe, the other pipe will wait for the work. 

## More about pipe

As mention in process model module, the process will running in order designed by operation system, similarly, pipe will also face the question:
- The process's write speed is slower than the other process's read speed. Specifically, the process write data into pipe slower than the process read data. (This time, the operation system will help to stop reading)
- The process's write speed much faster than the other process's read speed so that the pipe always full no where for writing anymore. Similarly, operation system will stop writing 'till finishing reading.

## dup2 system call

`int dup2(int oldfd, int newfd):` return the new file descriptor or `-1` on error

The `dup2` will make a copy of an open file descriptor so that we can use it to reset the `stdout` descriptor so that the writing to `stdout` can go to our own output file. (We can also read from `stdout` by `dup2`)

The `dup2` needs 2 parameters, one is the old `fd` (file descriptor), the other one is the new `fd`. New one will be the copy of old one after calling this function

## select system call

`int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout):`  return the number of file descriptors contained in given sets, or `0` timeout expires before action or `-1` on error

For `fd_set`, we can 

-   use `FD_ZERO(fd_set *set)` to initialize all value to `0`
-   `FD_SET(int fd, fd_set *set)` to add file descriptor into `fd_set`
-   `FD_ISSET(int fd, fd_set *set)` to see if file descriptor in this set.

When we use `select` the `nfds` should be the highest file descriptor + 1

We can use select to solve the pipe issues where multiple children write on same pipe and some other pipe to wait 'till they stop.