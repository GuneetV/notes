

[[3a - Code Optimisation and Code Refactoring-1.pdf]]
### C is row major

Easier to access rows contiguously than columns due to memory layout
only if whole matrix doesn't fit in the L1 cache

## Code optimisation techniques

### Loop Fusion

Used when checking the loop condition may be expensive

Combine many smaller loops into one loop

Can use peeling for this

### Loop Fission


Used when there is poor temporal locality of memory accesses between loop iterations

Break down one loop containing many unrelated operations into two or more loops so improve efficiency in fetching
### Loop unrolling

Write out a loop fully instead of having a loop
Use when checking the loop condition is expensive

### Loop pipelining

Similar to loop unrolling

Use when the CPU is capable of pipelining

Prolog - Pipeline - Eplilog


[[3b - Compiler Optimisations and Parallelism.pdf]]
### Loop vectorization


Flynn's Taxonomy: SISD, SIMD ...

A vector register is multiple pieces of data at once
Can apply a single instruction to it and apply it to all data inside, like a vector

ie \[1, 2, 3, 4] + \[5, 6, 7, 8] = \[6, 8, 10, 12]

SSE is the intel vector register
each SSE register can hold 16 bytes: 4 ints or 2 doubles
when doing operations to anything in those registers can do it to 4 ints at a time

To bring in the data to place into vector registers from ram to cache to register it is best to align the memory so that when the cpu is placing them in, it doesn't take as many "word reads" to place into the registers 

#### Loop unrolling + vectorization

When unrolling a loop, inside the unrolled loop instead of individually operating on each piece of data, can use vector registers for it. Speeds up the 

![[memory_alignment.png]]


#### Matrix multiplication with vectorization

Can also vectorize the block matrix multiplication technique

Speeds up the loops

#### SSE Conditionals

Branching is a impediment to vectorization

Ie if you do different operations depending on the base data

You can create a mask for the condition and compute both results for the vector, the output is the masked, merged version of both of those results

#### Vector Shuffling

If you want to calculate the sum of all the element in a vector, you can shuffle it in 4 different config vectors and then sum them together

Use the slides

Can represent each element in vector as a 2 digit binary string
element 0: 00
element 1: 01
element 2; 10
element 3: 11

then if i want element 2310 i use the binary number

10 11 01 00 = 170

170 is the config of this vector

## Multi threading

Instead of higher clock speed, use multiple cores

More flexible than a vector but more expensive

Can also lead to race conditions and so need to communicate to avoid them

Can use either Pthread or OpenMP for multithreading

OpenMP is a lot higher level than pthread

Its based on the existence of multiple threads in the shared memory programming paradigm

Have to set the number of threads either by using global
`OMP_NUM_THREADS=n`
OR
`omp_set_num_threads(n);`

```Common_thread_functions

omp_get_num_threads() get the max num of threads 
omp_set_num_threads()
omp__get_thread_num() get the current thread id
```

`# pragma omp barrier` is used to ensure that all threads have reached that step in the program before it moves on
Pretty computationally expensive but can be useful for data integrity


`# pragma omp critical` defines a critical section of code that can only be perfomed by one thread

`# pragma omp atomic` only applies for one statement, allows update to be carried atomically and prevents race conditions

scope of private, firstprivate, shared and default

also keywords reduction (when summing a variable create subtotal sums then update the final value serially to multithread for one variable)
and parallel for (split a for loop between threads to share workload as much as possible)

also chunksize

## Related
- [[introduction to Advanced Computer Architecture]]
- [[Pipelining]]
- [[Memory]]
- [[Cache memory]]
