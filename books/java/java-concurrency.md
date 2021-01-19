
Chapter 1

*Introduction *

Writing correct programs is hard; writing correct concurrent programs is
harder.

There are simply more things that can go wrong in a concurrent program
than

in a sequential one. So, why do we bother with concurrency? Threads are
an

inescapable feature of the Java language, and they can simplify the
develop

ment of complex systems by turning complicated asynchronous code into
simpler

straight-line code. In addition, threads are the easiest way to tap the
computing

power of multiprocessor systems. And, as processor counts increase,
exploiting

concurrency effectively will only become more important.

**1.1 A (very) brief history of concurrency **

In the ancient past, computers didn’t have operating systems; they
executed a

single program from beginning to end, and that program had direct access
to all

the resources of the machine. Not only was it difficult to write
programs that ran

on the bare metal, but running only a single program at a time was an
inefficient

use of expensive and scarce computer resources.

Operating systems evolved to allow more than one program to run at once,

running individual programs in *processes*: isolated, independently
executing pro

grams to which the operating system allocates resources such as memory,
file

handles, and security credentials. If they needed to, processes could
communi

cate with one another through a variety of coarse-grained communication
mech

anisms: sockets, signal handlers, shared memory, semaphores, and files.

Several motivating factors led to the development of operating systems
that

allowed multiple programs to execute simultaneously:

**Resource utilization.** Programs sometimes have to wait for external
operations

such as input or output, and while waiting can do no useful work. It is

more efficient to use that wait time to let another program run.

**Fairness.** Multiple users and programs may have equal claims on the
machine’s

resources. It is preferable to let them share the computer via
finer-grained

time slicing than to let one program run to completion and then start an

other.

1

Java Concurrency in Practice. Java Concurrency in Practice, ISBN:
0321349601

Prepared for Salesh.fbsi.Kumar@fidelity.co.in, Salesh Kumar

Copyright © 2006 Pearson Education, Inc.. This download file is made
available for personal use only and is subject to the Terms of Service.
Any other use requires prior written consent from the copyright owner.
Unauthorized use, reproduction and/or distribution are strictly
prohibited and violate applicable laws. All rights reserved.

2 *Chapter 1. Introduction *

**Convenience.** It is often easier or more desirable to write several
programs that

> each perform a single task and have them coordinate with each other as

necessary than to write a single program that performs all the tasks.

In early timesharing systems, each process was a virtual von Neumann com

puter; it had a memory space storing both instructions and data,
executing in

structions sequentially according to the semantics of the machine
language, and

interacting with the outside world via the operating system through a
set of I/O

primitives. For each instruction executed there was a clearly defined
“next in

struction”, and control flowed through the program according to the
rules of the

instruction set. Nearly all widely used programming languages today
follow this

sequential programming model, where the language specification clearly
defines

“what comes next” after a given action is executed.

The sequential programming model is intuitive and natural, as it models
the

way humans work: do one thing at a time, in sequence—mostly. Get out of

bed, put on your bathrobe, go downstairs and start the tea. As in
programming

languages, each of these real-world actions is an abstraction for a
sequence of

finer-grained actions—open the cupboard, select a flavor of tea, measure
some

tea into the pot, see if there’s enough water in the teakettle, if not
put some more

water in, set it on the stove, turn the stove on, wait for the water to
boil, and so on.

This last step—waiting for the water to boil—also involves a degree of
*asynchrony*.

While the water is heating, you have a choice of what to do—just wait,
or do

other tasks in that time such as starting the toast (another
asynchronous task) or

fetching the newspaper, while remaining aware that your attention will
soon be

needed by the teakettle. The manufacturers of teakettles and toasters
know their

products are often used in an asynchronous manner, so they raise an
audible

signal when they complete their task. Finding the right balance of
sequentiality

and asynchrony is often a characteristic of efficient people—and the
same is true

of programs.

The same concerns (resource utilization, fairness, and convenience) that
mo

tivated the development of processes also motivated the development of
*threads*.

Threads allow multiple streams of program control flow to coexist within
a proc

ess. They share process-wide resources such as memory and file handles,
but

each thread has its own program counter, stack, and local variables.
Threads also

provide a natural decomposition for exploiting hardware parallelism on
multi

processor systems; multiple threads within the same program can be
scheduled

simultaneously on multiple CPUs.

Threads are sometimes called *lightweight processes*, and most modern
oper

ating systems treat threads, not processes, as the basic units of
scheduling. In

the absence of explicit coordination, threads execute simultaneously and
asyn

chronously with respect to one another. Since threads share the memory
address

space of their owning process, all threads within a process have access
to the same

variables and allocate objects from the same heap, which allows
finer-grained data

sharing than inter-process mechanisms. But without explicit
synchronization to

coordinate access to shared data, a thread may modify variables that
another

thread is in the middle of using, with unpredictable results.
