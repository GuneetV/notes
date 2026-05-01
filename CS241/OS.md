
# Introduction to OS
## What is an OS?

Software acting as intermediary between user and hardware of a device

OS is responsible for allocating resources to their processes in an appropriate way as to not cause errors

OS must be able to:
- Load programs into memory
- Execute the program by creating process
- Stop the process

Os needs to be able to:
- IO operations
- File management
- Program execution
- Communication with same/networked computer
- Error handling
- Resource allocation
- Accounting, what processes are running and how many resources they are taking
- Protection and security
## Kernel

kernel is the core part of the OS
Loaded into main memory at startup and runs continuously

kernel space is the memory where the kernel executes, its protected from user space

The user can only access the kernel space through system calls

There are different methods of developing a kernel


### Monolithic kernel

Al functionalities built into the kernel

Very little overhead in the system call interface

Very hard to debug kernel code

### Layered approach

Modular design, with layers

Layer k makes calls to layer k-1

Bottom layer is the hardware and the top layer is the user

### Microkernels

Remove all non essential components from a kernel

only provide minimal process and memory management and inter process communication

Easy to extend and make secure and reliable but a lot of performance issues due to system call overhead

### loadable kernel modules

Modern approach

Kernel starts with core services and dynamically implements the other servives as the kernel is running 

# Processes 

A program is a passive entity stored on disk
A process is a program in execution

## Process in memory

In the virtual address space of a process there are several sections:
- Text - stores instructions
- Data - stores global variables
- Heap - dynamically allocate memory
- Stack - local variables, function parameters

Space between stack and heap allows them to grow and shrink during runtime

## Process control block

Each process has a PCB that tracks everything about it

including:
- Process state
- Program counter (location of next instruction)
- CPU registers
- CPU scheduling
- Memory management information
- Accounting information (CPU used, time since start)
- IO status (list of open files)

This is used for context switching and easy access in case of any crashes 

![[CPUSwitching.png]]

Context switching is described here

OS saves current state and switches to another state
Causes some overhead, longer the more complex the PCB structure is


## Process scheduling

Most OS support concurrency, allow multiple process to execute at once 
OS schedulers choose what process gets a specific resource and when
OS maintains several queues to schedule processes:
- Job queue: all processes in the new state (long term)
- Ready queue: all processes in the ready state (short term)
- Device queue: processes waiting for a specific device (different queue for each device)


The long term scheduler  is the gatekeeper for programs. It decides which programs get loaded into memory at all
It allows processes to get loaded and enter the ready queue
Runs rarely, minutes apart 
controls how many processes are in memory at once
This is mainly for supercomputer clusters and research, user focused OS like windows and linux don't have one

Short term scheduler is the CPU allocator. 
This is where stuff like scheduling algorithms work
Picks which process which is already ready and in memory gets the CPU right now
only looks at ready queue
Runs constantly, at least every 100ms
Very important for this to be fast, 10ms means 9% of CPU is wasted


## Process creation and termination

### Creation
Processes can be created in many ways, Clicking an icon, running a command (./a.out)

#### Child processes

The `fork()` command creates a child process

if fork fails it returns -1 for both parties
for the parent process fork returns the actual pid of the child process
for the child process it returns 0
which is why

``` c
int main(){
	pid_t pid;
	pid = fork;
	if (pid == 0){
		excelp("executable", "program name", "arguements");
	} else if (pid > 0){
	wait(NULL);
	printf("child has finihed")}
}
```

`wait` waits for any child process to finish and stores the exit code into the memory address provided as an argument

`excelp` allows you to run another program, the second arg allows you to lie about a program's name

Essentially, fork copies everything from the parent process like local variables and everything 

Address Space Options:
- In fork(), the child's address space is a duplicate of it's parent
- In Windows, CreateProcess() specifies the new program directly
-  Sort of like doing fork() and execlp() together
Resource Sharing Options (CPU, Memory, File pointers):
- Parent and child share all resources
- Children share subset of parent resources
- Parent and children show no resources
Execution Options
- Parent and children run execute concurrently
- Parent waits (wait()) until children terminate
### Process termination

Processes terminate after either
- Last statement
- after reaching `exit()` statement
- return a status value (exit code)
- All resources of the process are released by the OS

Zombie Process:
Process has been terminated but parent has not collected exit status code
All resources are released, but entry is still in process table
Once parent recieves the exit status, entry is released from table

Orphan Process
parent has exited without `wait` ing
In UNIX-based systems, the init process is assigned as the parent
init process then periodically wait() to collect exit status of all orphan processes
Allows exit status to be collected, releases orphans pid and process table entry

Parents can terminate children with `abort`
Can be used if a child has exceeded alocated resources

## Inter Process communication

Processes running concurrently may want to communicate with each other

Two fundamental models of IPC: 
- Shared memory - establish region of memory shared by communicating
- Message Passing - messages are exchanged between processes

Message Passing:
- processes message each other
- kernel provides comm channel
- system calls pass messages

Shared Memory
- Processes read/write shared part of memory
- Kernel only establishes shared memory
#### Shared memory

The shared memory resides in the address space of one of the communicating processes
The other processes request permission to access it

Kernel is required to setup shared memory and give perms
Up to user processes to maintain proper sync

Producer - process that produces information
Consumer - process that consumes the information
A process can be both

Good way to implement a shared buffer is a circular queue

#### Message passing

The system needs to provide at least 2 operations:
- `send(message)`
- `recieve(message`

implemented as system calls

##### Direct communication

Processes must explicitly name each other
`send(p, message)`
`recieve(q, message` or `recieve(id, message)`

Link established automatically
Link has one pair of communicating
Can't hardcode PID since PID can change

##### Indirect communication 
Messages are directed and received from mailboxes also known as ports

`send(mailboxID, message)`
`recieve(mailboxID, message)`

Established only if processes share a common mailbox

Link may have many processes



#### Synchronisation  
 Blocking is considered  synchronous  
-  Blocking send: sender blocked until  message received  
- Blocking receive: receiver blocked until message available
Non blocking is considered asynchronous:
- Non blocking send: sender sends message and continues
- Non blocking receive: receiver receives valid or null message

Can use different combinations of blocking and non blocking send and receive

Communication link is a buffer:
if the buffer is:
- zero capacity: sender must block until recipient recieves message

#### Real IPC systems

Shared memory using mmap

Ordinary pipes in UNIX
- One way message passing- Pipe connects output of one process to input of another
- Create pipes using | in bash

Named pipes
- `mkfifo namedpipe`
- First in first out file which multiple processes can communicate with
- Treated like any other file

# Threads

A thread is a unit of CPU execution
Single threaded -> one chain of execution, running each line sequentially

To achieve speedup and achieve concurrency (doing many things at once)
Threads share more with their parents than processes do,, code, data, heap, opened files, signals

Each thread has:
- Thread id
- Program counter
- Register set
- Stack

Thread creation has less overhead than process creation due to sharing more

Most modern applications are multi threaded

Servers are very often multi threaded due to having to process many clients at once

Threads allow:
- cheaper than process creation
- Can scale to a large number of concurrent tasks
- Can allow continued execution of one thread even when another is blocked
- Can share resources of the process making it easier than shared memory or message passing

### Concurrency vs Parallelism

Concurrency is more than one task making progress, ie by interleaving execution of tasks

Parallelism implies that a system can perform multiple tasks at the same time

Can have concurrency without parallelism 

### Data vs task parallelism

Data distributes subsets of the same data across multiple cores each performing the same operation on their subset
like summing the array to find an average

Task splits threads performing tasks across multiple cores
For example one thread finds average another finds median

Amdahl'ls Law 

$$speedup \leq \frac{1}{S+\frac{(1-S)}{N}}$$

## Kernel vs User threads

The kernel itself may be running multiple threads
Some kernel threads provide services to user
Kernel can scedule them on different CPUs

User threads
Exist within user processes
For a user level thread to execute on the CPU it must be associated with a kernel level thread

Basially each process owns multiple threads and the models talk about how they are registered with the kernel

__Each user thread needs to be associated with a kernel thread to be able to make system calls like read from disk__
### One to one model

Each user level thread maps to a kernel thread, on Linux and Windows

Means the kernel is aware of all the threads running in the user process so the user process can completely rely on kernel to manage its threads

Means creating each user thread involves the kernel so more expensive and user process is limited by thread management policies implemented by OS

__This means each new thread is immediately registered with the kernel and can be seen seperately__ 

### Many to one model
All user level threads are mapped to a single kernel thread

Means less overhead and more flexibility in thread management in the user level thread library

But also means multiple user level threads cannot run in parallel  and than one blocking user level threads are mapped to a single kernel thread

__This means the kernel sees only as one block and so you cannot parallelise in this model__

### Many to many model

Mixture of both, allows user threads to be multiplexed into smaller or equal number of kernel threads
kernel threads can run in parallel meaning one user thread cannot block the entire process
Programmers can decide on how many kernel threads to use and how many user threads should be mapped to each one

## Threading strategies

Determines interaction among threads in a process
2 strategies:
- one thread per request
- thread pooling


### One thread per request
Server creates a seperate thread to handle each client request
- High overhead for each thead
- - High traffic will make a large number of threads slowing system by burdening it

### Thread pooling
Fixed number of worker threads which take from a queue of requests

- Sllightly faster to service a request with an existing one diue to creation overhead
- Allows number of threads to be bound in size, taking into account number of cores and memory
But:
- A request may have to wait in a queue to get served
- Deciding number of workers is hard


One main downside is the workers keep checking queue even when its empty, wastes cpu time and energy

Condition variables solve this, they tell a worker when to wake up and work

### Signal handling

Signal handling is used in UNIX to notify a process about when an event occurs

Synchronous - generated be a process, ie div by 0 illegal mem access 

Asynchronous - externally generated  by terminating process using control c or sigint

All signals follow the same pattern
- signal is generated
- signal is delivered to the process to which it replies
- signal is dealt with

handling can be default or user defined

In multthreaded programs signal can be deliver to all threads or specific ones

Synchronous signals are usually delivered to the thread generating signal
Some async ones like sigint should be sent to all

Can also be sent to a specific thread


# Synchronisation

Both threads and processes need to sync to ensure they don't enter a race condition when updating variables
- race to see which one writes last
Critical section - When shared variables are updated
Mutual exclusion - if one process is in its critical section the others should not be allowed to enter it

A perfect solution would ensure mutual exclusion while allowing other programs to make other progress while one is writing and no program should have to wait indefinitely

## Solutions for syncing
### Shared variable

Have a shared variable
when its 0, process 0 can do its critical section then set it to 1
when its 1 process 1 can do its critical section then set it to 0
Busy wait when the shared variable doesn't match

Kind of does nothing since when one isn't in critical section it does nothing
Also if one finishes and doesn't set the turn to the other the program never terminates for other process

### Peterson's Algorithm

Theres a flag array that signals intention before you enter the critical section
Busy wait while the turn variable is set to other and the others flag is true
If either are false then can enter your critical section

Still busy waits and can not work on modern architecture

### Mutex locks
```c
while(True){
	acquire lock
		critical section
	release lock
		remainder section
}
```

Locking should be performed atomically, non interruptible
Modern machines use specific hardware to implement locks

one example is `test_and_set()`

### Semaphores
Semaphores have integer values
Value <= 0 means semaphore not available
Positive value means its available

Can only be accessed via atomic operations
- `wait()`
- `signal()`

wait means the calling process waits until it becomes positive
if its positive it decrements the value by 1

signal increments the value by 1

Can control the amount of processes that can concurrently access a resource

Trying to solve the reader-writer problem, allowing multiple reads while still only one write

## Syncing issues

### Deadlock
2 or more processes waiting indefinitely for an event that can only be caused by one of the waiting one

A waits for B, B waits for A, A and B are in deadlock

### Starvation
Occurs when one process has to wait indefinitely while others make progress


To avoid this signal should randomly pick process to wake

### Priority inversion

If lower priority process holds lock needed by a higher one


## Problems

### Bounded buffer

n buffers each can hold one item
Producer produces and consumer consumes

Producer should not make more when buffer is full
Consumer should not consume when buffer is empty

### Readers and writers problem
Data set shared
Readers can only read not update
Writers can read and write

Can only have:
- Multiple readers
- OR one writer
At one time

Use semaphores to solve this 
Need
```c
semaphore rw_mutex = 1;
semaphore mutex = 1;
int read_count = 0;

writer:
do {
	wait(rw_mutex);
	...
	/* writing is performed */
	...
	signal(rw_mutex);
} while (true);

reader:
do {
	wait(mutex);
	read_count++;
	if (read_count == 1)
		wait(rw_mutex);
	signal(mutex);
	...
	/* reading is performed */
	...
	wait(mutex);
	read_count--;
	if (read_count == 0)
	signal(rw_mutex);
	signal(mutex);
} while (true);

```
### Dining Philosophers problem

Philosophers thinking or eating

To eat they have to pick up their left and right chopsticks
Always pick their leftmost chopstick once

If all grab their left chopstick at once there is a deadlock

To solve this use a asymmetric solution
Odd philosophers pick up left then right
Even right then left



# Scheduling

There are different queues for processes in different states
i.e i/o queue, ready queue

The scheduler takes processes from the ready queue to the CPU
Goal is to increase CPU utilisation - Fraction of time CPU is busy when jobs are in ready queue

Processes are usually CPU bust followed by I/O burst. During I/O can do other processes

non-premtive means it completes the task before moving on
premtive means it can let go of current task before completing, usually faster

## FCFS
First come first served  scheduling

Processed in the order of arrivals

Average wait time for 3 processes: p0 -  24ms, p1 - 3ms, p2 - 3ms
$(0+ 24+ (24+3))/3 = 17$

Heavily reliant on shorter jobs arriving first for shorter wait times
Is non preemptive
## Shortest Job First 
Proven to give the minimum average waiting time

But you need to estimate how long the CPU bust will be

Uses a formula to predict how long next burst will be based on previous bursts  for each process
$$\tau_{n+1} = \alpha \cdot t_n + (1 - \alpha) \cdot \tau_n$$

| Symbol       | Meaning                                          |
| ------------ | ------------------------------------------------ |
| $t_n$        | Actual length of the $n$-th CPU burst (observed) |
| $\tau_n$     | Predicted length for the $n$-th burst            |
| $\tau_{n+1}$ | New prediction for the **next** burst            |
| $\alpha$     | Smoothing factor, $0 \leq \alpha \leq 1$         |
Expands to

$$\tau_{n+1} = \alpha t_n + \alpha (1-\alpha)t_{n-1} +\alpha (1-\alpha)^2t_{n-2} + ... $$

High alpha means the prediction is solely on the previous burst
Low alpha means ignore observations, prediction never changes

### preemptive vs non preemptive 
Preemptive allows a cpu to switch to another job if a shorter one arrives


SJF is a special case of Priority scheduling
Problem with this is starving the low priority ones
But can use ageing to solve this

## Round robin
Each process gets a small amount of CPU time, q

After each q, process is pre empted and added to end of queue
generally visits in order of arrivals

A large q is basially FCFS
Small q means too many context switches
Usually between 10-100ms

Average wait time:
![[RoundRobin.png]]

Wait time = Finish time - arrival time - burst time


# Related
- [[Networks]]


