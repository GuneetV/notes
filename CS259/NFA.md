
NFA can have multiple paths for same input from a state

ie state q2 can have a path to itself for 1 and also a path to q3 for 1

This means you may have to create a tree to check what run is accepted using the string

Look at example

The only accepted string is the one that ends on a accepted state after consuming the entire string


Can also have epsilon transitions, which DFA's cant have

Epsilons consume nothing, free pass to wherever


### DFA must have a transition for each letter in the alphabet NFA doesn't have to

## Related
- [[introduction to Formal Languages]]
- [[Regular expressions]]
- [[Nonregular Languages]]
- [[Context Free Grammars]]
- [[Pushdown automata]]

