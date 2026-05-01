
Uses SRAM instead of DRAM

More expensive, needs 2 transistors rather than a transistor and a capacitor
The memory is volatile but doesn't require refreshing

Faster than DRAM due to not doing through buffers and multiplexers and stuff

##### SRAM:
- Better read write times
- Uses flip flop logic gate config
- Will hold data as long as power is supplied
##### DRAM:
- Transistor + capacitor
- Greater cell density
- Cheaper
- Refresh tech is a one off cost

#### eDRAM

DRAM integrated on the same chip as the multi chip module of an application specific intereated circuit r microprocessor

Intermediary between DRAM and SRAM

### IBM z13 Storage control chip layout

Each core has a L1 SRAM 96kb , L1 DRAM 128 kb, L2 SRAM 2mb and a L2 DRAM 2mb

Then a shared L3 cache for dram


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
- [[Memory]]
- [[Processor Organization]]
- [[Code Optimization]]
