
Instruction set architecture involves stuff a programmer can reason about like the state of the registers and operations

Microarcitecture is the electronic/logical design of how the processor was built

User visible registers are used by low level programmers to optimize code:
data registers, address registers, index registers, segment ptr register, condition code register

Control and status registers are used by the control unit to keep track of operations and os level stuff:
PC, MAR, MDR, IR, MBR

Program status world
??? ask after


### Instruction types
4 types of instructions

#### Data processing
Arithmetic or logic instructions
ADD, SUB, OR, AND, MUL

#### Data storage
Movement of data into or out of register memory
LD, ST

#### Control

Test instructions to test value of data word
Branch instructions for control flow 
BEQZ, JR

#### Data movement
I/O to transfer data in and out from ports
IN, OUT


### Addressing modes

![[addressing_modes.png]]

Scaled???

### ISA encoding

Fixed width instructions

Variable length instuctions

Very long instructions

### interrupts and indirect

The reason each fde cycle is not exactly a cpu clock is that it can take multiple to fetch opcode and operand, especially for the less direct addressing modes.

Interrupts and indirect cycles can slow it down

interrupts are very useful because it means you dont have to busy wait all the time 

## Related
- [[introduction to Advanced Computer Architecture]]
- [[Pipelining]]
- [[Memory]]
- [[Cache memory]]
