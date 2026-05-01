
### Textbook: Introduction to the theory of computation

#### Formal languages are a means to model computation

About which problems can be solved by computers

#### Alphabet: finite nonempty set ( {0, 1}, {a, b, c...} )

A string over alphabet A is a finite sequence of elements of A (Called letters)

A* is the set of all strings over alphabet A

### a language over A s a subset of A*

1 is a language over {0, 1}*



# Section 1: Regular Languages

A regular language is one that can be accepted by a NFA (since all DFA's can be created to accept all strings by a NFA they also work)

## Deterministic Finite Automata (DFA)

### Formal definition of a language, 5 parts
 Q <- Finite set of states 
 $\Sigma$  <- Some alphabet
 $q_0$- <- element of Q, initial state
 F <- Subset of Q, set of final states (accept states)
 $\delta$ <- Transition function, function from Q$\times$A  -> Q
 

### Automata

must end in one of the end states, if the string doesn't result in the end state it isn't valid

The set of all valid strings is called the language of the DFA

$\epsilon$, the empty string is neutral with respect to string concatenation

Can define the output inductively, i.e with functional lists head then tail or empty list
Take the state after the first element then call on the rest of the string (excluding the first element)

## Related
- [[NFA]]
- [[Regular expressions]]
- [[Nonregular Languages]]
- [[Context Free Grammars]]
- [[Pushdown automata]]