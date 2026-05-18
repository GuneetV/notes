
There are 4 main structural components of a computer
- CPU 
- Main Memory
- I/O
- System interconnection 

Designers dilemma: 
desire low cost high capacity memory
desire high performance

# Memory hierarchy

Main reason for this is economics

Usually you want to access memory in same location as well - Spacial locality

If one particular location is referenced, it will probably be accessed again, temporal locality

Reasonable assumption: studies show 90% of access within 2kb of each others, compilers want to optimise for close memory

# Semiconductor memory types

## Ram 

 ##### Random access memory
 - Read Write
 - Electrically written
 - Volatile

### DRAM vs SRAM

#### SRAM:
- Better read write times
- Uses flip flop logic gate config
- Will hold data as long as power is supplied
#### DRAM:
- Transistor + capacitor
- Greater cell density
- Cheaper
- Refresh tech is a one off cost

### Memory organisation

Arranged in rows and columns according to word size

i.e if word size is 8
16 rows of 8 bits would be 128 bits or 16 bytes

Also need 7 pins for the decoder to activate the correct rows since $log_2(128) = 7$

Need 8 output pins to get the data out so 15  pins total

Can use a one bit word size for same data of 1024 bits, requires 11 I/O pins, less than 8x128 but accesses are inefficient

Also need read/write pin and chip select pin

Can also have more than the word size amount of columns and use a multiplexer for the data to select the right word

ie use 256x256 and have 8 for the row address and 4 for the column address so you can have 16 bit words

Can stack these memory cells on top of each other, creating a 2048x2048x4 memory circuit
Only need 11 address lines if you have a row address select, column address select etc

### Interleaved Memory

A collection of DRAM chips can be read from

i.e retrieve from memory bank 1 and place it in the cache, at the same time place data from bank 2 into the cache.

Since memory is the bottleneck, this speeds up things a lot as long as you are addressing different banks each time

### Synchronous DRAM

You have a clock that syncs with the processor clock to ensure the processor can carry out other tasks as data is being fetched from memory

You can use burst mode to send a lot of data to the cache at once, instead of asking for a cache line and then getting it back, just ask for the 2 or 4 or 8 or even whole page, this way you don't have to keep waiting for memory

SDRAM performs best when working on large serial block transfers
### DDR Ram

Double data rate
Instead of only sending data on the rising edge, send at the rising and falling edge

DDR also uses a 2n-prefetch buffer

Voltage drops with every gen

Front side bus rates double every gen

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


Uses SRAM instead of DRAM

More expensive, needs 2 transistors rather than a transistor and a capacitor
The memory is volatile but doesn't require refreshing

Faster than DRAM due to not doing through buffers and multiplexers and stuff

#### eDRAM

DRAM integrated on the same chip as the multi chip module of an application specific intereated circuit r microprocessor

Intermediary between DRAM and SRAM

## ROM

Non volatile data storage

No power source required

No errors should be in data

### PROM

Programmable ROM

Electrically writable, needs specialist equipment but not beyond consumer budgets

### EPROM

Erasable PROM

Incorporate a window to allow UV light to shine into storage cells to erase content

### EEPROM

Electrically erasable programmable ROM

Allowed individual bytes to be erased and written, best ROM for people who want to write

Huge overhead for write operations around 400-800ms

## Flash memory

Form of semiconductor memory

Typlically one transistor per bit

As DRAM density drops, flash will play a role in performance

Uses a single transistor, jey point is it can be in 2 states

Will eventually deteriorate

## Related
- [[introduction to Advanced Computer Architecture]]
- [[Processor Organization]]
- [[Code Optimization]]








