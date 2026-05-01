# Propositional logic

Proposition is a statement for which it makes sense to ask is it True or False?
i.e has a truth value

Can combine propositions and use logical connectives
P AND Q, NOT Q OR P ...

#### in terms of syntax, double negation is not the same as the formula itself

The formulae must also contain parentheses in order to be syntactically correct

Parse tree for a propositional logic formula is the tree with the variables as leaves and the operators as the parent nodes of each variable

Degree is the number of inner nodes in a parse tree

Defined recursively 
Deg(X) = 0 if X is atomic
Deg(NOT X) = 1 + Deg(X)
Deg(X o Y) = 1 + Deg(Y) + Deg(X)

For any logical connector o


Top T is always true, takes in no input, upside down version BOTTOM is always False

Tautology is if for any truth values of the variables, the formula always evaluates to false

X is a consequence of S if X maps to T under every valuation that maps every member of S to T

Limitations of truth tables:

- Space inefficient
- Don't show the patterns explicitly

# Boolean logic

Can have 2 formulae that are logically equivalent however syntactically different, ie X, NOT NOT X

If you replace a sub formula with a logically equivalent formula, the whole formula stays logically the same


### Laws of boolean logic:
- Idempotence
- De Morgan's
- Distributivity
- Exportation
- Absorption
- Contradiction (if x implies both y and not y, then x must be false)
- Neutrality


![[Pasted image 20260115161534.png]]

## Prolog stuff

Variables have capital, otherwise atomic

Facts, rules ect...

## Related
- [[Normal Form Algorithims]]
