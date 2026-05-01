Used to convert into alpha or beta functions 


Literal: a variable or its negation
Primary Connectives: {$\land$  , $\vee$ , $\rightarrow$ , $\leftarrow$,  ...}
hat
## Alpha and Beta formulae

### $\alpha$ formula is equivalent to $\alpha _1 \land \alpha _2$
### $\beta$ formula is equivalent to $\beta _1 \vee \beta _2$

## CNF formulae

Given any boolean formula as a list in <>

Simplify it down using alpha and beta formula table

If it is a beta formula, then separate it into a list after looking on the table

<\[a $\vee$ b]> = <\[a, b]>

If it is an alpha formula then make 2 dis junctions (square brackets) using it

<\[a $\land$ b]> = <\[a], \[b]>

Need to prove correctness and termination for this algorithm

Konigs lemma: any infinite finitely branching tree must have an infinite branch

The resulting list should be in CNF,:OR = ,   AND = []

## DNF algo

Same as CNF but simply reverse the rules for alpha and beta simplification

## Related
- [[Logic and Verification]]
