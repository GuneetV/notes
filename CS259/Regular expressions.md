Regular expressions can describe formal languages similar to DFA and NFA
[[introduction to Formal Languages]]

ie $(0 \cup 1)0*$ describes the language of all strings that start with 1 or 0 and then have any number of 0s

Union means this letter or that letter.
Star means can do as many of these as you want including 0

## Formal definition of regular expressions

Defined inductively

R is a regular expression if R is:
- a for some a in the alphabet $\Sigma$
- $\epsilon$
- $\emptyset$
-  $( R_1 \cup R_2 )$ Where $R_1$ and $R_2$ are Regular expressions
-   $( R_1 \circ R_2 )$ Where $R_1$ and $R_2$ are Regular expressions
- $R_1 *$ Where $R_1$ is a Regular expression

Usually, the concatenation function, $\circ$ is left out

### Difference between $\emptyset$ and $\epsilon$


Concatenation with $\emptyset$ results in a void language, no strings in it
$( R_1 \cup \emptyset )$ always results in $R_1$

Concatenation with $\epsilon$ changes nothing about the string
Union with $\epsilon$ means that $\epsilon$ gets added to the language

## A language is regular if and only if some regular expression describes it

# Generalised nondeterministic finite automation

Easiest to convert a DFA into GNFA and then into a Regular expression

## Related
- [[introduction to Formal Languages]]
- [[NFA]]
- [[Nonregular Languages]]
