# Memory hierarchy

Needed for economic reasons

Top of hierarchy should be ultra fast, expensive memory accessed very often

Bottom should be slow but cheap memory, accessed very rarely

Data is always sent from top to the bottom, CPU will never talk to RAM or Storage directly, data has to be changed in cache then sent down the hierarchy

## Performance modelling

Design targets are related to performance and cost

Imagine we have a hierarchy of 2 levels, M1 and M2.
Ci is cost at level i, Si is capacity at level i

average cost per bit is

$$C_s = \frac{C_1 S_1 + C_2 S_2}{C_1 + C_2}$$

The bigger S2 is compared to S1 the lower the cost is (This seems very obvious idk why they need the formula and graphs)

**Average access time to access an item:**
$$t_{av} = H t_1 + (1-H)(t_1 + t_2)$$
H is hit rate
T_i is access time for memory level i

If the memory is not in the cache then it needs to be swapped in as part of a block and then the cache is accessed again


# Related
- [[Memory]]