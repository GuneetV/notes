Hazards can occur when pipelining:
- Structural hazard: When 2 or more instructions require same resource, then the instructions must be. Solutions are to detect these and not pipeline (hard) stall and wait until everything with that memory is done (easy) or just copy the memory over and duplicate it
- Control hazards: don't know what to pipeline because theres a branch statement and could go to different instructions. Solutions are: brute force where you load and pipeline both of the branches, prefetching the branch target and the first few instructions after. can also have a loop buffer where they keep the n most recently instructions in sequence. Can also use branch prediction. 
- data hazards: conflict of access of an operand location. Solutions: schedule when the programmer doesn't create these hazards, stall: just stall until its over, bypass: hardware data path allows values to be sent to an earlier stage before preceding instruction has left pipeline, speculate: guess that no problem. If there is problem then kill speculative instruction and restart.

## Related
- [[introduction to Advanced Computer Architecture]]
- [[Processor Organization]]
- [[Code Optimization]]
