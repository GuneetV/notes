### Distinguishable strings

2  strings $x, y$ are distinguishable if and only if there exists an suffix $z$ for which only one of $xz, yz$ is in the language
### Context free grammar

has 4 parts
1) V, the variables
2) $\Sigma$ , disjoint from V the terminals
3) R, the rules. Each rule is a variable and a string of variables and terminals
4)  S $\in$ V is the start variable

### Chomsky normal form

A context free grammar is in CNF is every rule is of the form
- A $\rightarrow$ BC
- -A $\rightarrow$ a
where a is any terminal and A, B and C are variables except that B and C may not be start variables

## Myhill nerode

Similar to  pumping lemma, used to prove nonregularity of languages [[Nonregular Languages]]

Need to know distinguisability for it

#### Theorem: if L has an infinite distinguishing set, the L is not regular

## Related
- [[introduction to Formal Languages]]
- [[Nonregular Languages]]
- [[Pushdown automata]]
- [[NFA]]

