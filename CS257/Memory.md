
There are 4 main structural components of a computer
- CPU 
- Main Memory
- I/O
- System interconnection 

Designers dilemma: 
desire low cost high capacity memory
desire high performance

### Memory hierarchy

Main reason for this is economics

Usually you want to access memory in same location as well - Spacial locality

If one particular location is referenced, it will probably be accessed again, temporal locality

Reasonable assumption: studies show 90% of access within 2kb of each others, compilers want to optimise for close memory

### Semiconductor memory types

 ##### Random access memory
 - Read Write
 - Electrically written
 - Volatile

###### DRAM vs SRAM

DRAM generally better

Faster, ...


### Memory organisation

Arranged in rows and columns according to word size

i.e if word size is 8
16 rows of 8 bits would be 128 bits of 16 bytes

Also need 7 pins for the decoder to activate the correct rows

Also need read/write pin and chip select pin

Can also have more than the word size amount of columns and use a multiplexer for the data to select the right word

Can stack these memory cells on top of each other, creating a 2048x2048x4 memory circuit
Only need 11 address lines if you have a row address select, column address select etc

### Interleaved Memory

A collection of DRAM chips can be read from

i.e retrieve from memory bank 1 and place it in the cache, at the same time place data from bank 2 into the cache.

Since memory is the bottleneck, this speeds up things a lot as long as you are addressing different banks each time

### Synchronous DRAM

Burst mode to grab data from same address line at the same time, fast


### DDR Ram

Double data rate
Instead of only sending data on the rising edge, send at the rising and falling edge

## Prefetch buffer

If we know that most of the data we need is within 3 kb of the address we are selecting, can store all of the local data in the cache, prefetch. to speed it up 

## Rank and module

Rank: multiple chips operated together to form a wide interface

All chips composing a rank are controlled t the same time
- respond to a single command
- Share address and command busses but provide different data

DRAM modules consist of different ranks

Each rank consists of different memory banks

In general, some number of ranks are connected to a memory controller, with multiple memory controllers to allow optimisation

## Related
- [[introduction to Advanced Computer Architecture]]
- [[Cache memory]]
- [[Processor Organization]]
- [[Code Optimization]]








