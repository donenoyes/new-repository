## Chapter 1. Introduction.........................................................................................................

```
Writing correct programs is hard; writing correct concurrent programs is harder.
There are simply more things that can go wrong in a concurrent program than
in a sequential one. So, why do we bother with concurrency? Threads are an
inescapable feature of the Java language, and they can simplify the develop-
ment of complex systems by turningcomplicated asynchronous code into simpler
straight-line code. In addition, threads are the easiest way to tap the computing
power of multiprocessor systems. And, asprocessor counts increase, exploiting
concurrency effectively will only become more important.
```
#### 1. 1 A (very) brief history of concurrency

```
In the ancient past, computers didn’t have operating systems; they executed a
single program from beginning to end, and that program had direct access to all
the resources of the machine. Not only was it difficult to write programs that ran
on the bare metal, but running only a single program at a time was an inefficient
use of expensive and scarce computer resources.
Operating systems evolved to allow more than one program to run at once,
running individual programs in processes : isolated, independently executing pro-
grams to which the operating system allocates resources such as memory, file
handles, and security credentials. If they needed to, processes could communi-
cate with one another through a variety of coarse-grained communication mech-
anisms: sockets, signal handlers, shared memory, semaphores, and files.
Several motivating factors led to the development of operating systems that
allowed multiple programs to execute simultaneously:
```
