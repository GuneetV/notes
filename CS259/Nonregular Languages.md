
Some language are incapable of being parsed by a NFA 
[[introduction to Formal Languages]]

Imagine a language that is $\{0^n 1^n | n \geq 0\}$ , the automaton must keep track of all the 1s and 0s present in the string so far

since the number of 0s is not limited, it will have to keep track of an infinite amount of possibilities, which is impossible with a finite number of states

However the language that has the same number of 01s and 10s is actually regular, despite appearing similar to the one above

# Pumping lemma

A theorem that all regular languages have a special property: that strings in the language can be "pumped" if they are at least as long as a special value called the pumping length

Each string contains a section that can be repeated any number of times with the resulting string remaining in the language

Definition:
If A is a regular language, then there is a number p, the pumping length, where if s is any string in A of length at least p, then s may be divided into 3 pieces $s = xyz$ satisfying the following:
1. for each $i \geq 0$, $x y^i z \in A$
2. $| y | > 0$ 
3. $|xy| \leq p$

## Proof of the pumping lemma
Let M be a DFA that recognises A
Assign p to be the number of states in M

We show that any string s in A of length at least p may be broken into xyz

if any s in A has length at least p lets consider the states it has to pass through, which is the length of the string + 1 since it must also have a start state and one for transition

We know the number of states it passes through is n + 1 and we know n > p by definition so it must pass through the same state more than once

The repeated state marks the pump, the loop in states or y as signified by this diagram

![[Pasted image 20260210195945.png]]

The part before the repeated states is x, the "loop" of states is y and the part after the loop is z

## How to use pumping lemma to prove a language is not regular

1. First assume that B is regular
2. Use pumping lemma to guarantee the existence of a pumping length p such that all strings of length p or greater in B can be pumped
3. Next find a string s in B that has length p or greater but cannot be pumped
4. Demonstrate s cannot be pumped by considering all ways of dividing it into xyz

Lets try and prove  $\{0^n 1^n | n \geq 0\}$ is irregular

Assume that it is regular
let p be the pumping length given by the lemma

choose s to be the string $0^p 1^p$ because s is a member of B and has more letters than p the pumping lemma guarantees that it can be pumped

we split it into 3 parts: xyz where for any amount of ys in between x and z s will be in B

if y contains only 0s, having more than 1 y would make s not part of B since there would be more 0s than 1s
Same with if y contains only 1s 
if y contains both 0s and 1s, the string xyyz will have some 0s and 1s out of order since be mandates that all 0s come before all 1s

This is unavoidable if we make B regular, so B is not regular


The trick to this is choosing a string which makes it so one of the 3 properties of the pumping lemma is broken

## Related
- [[introduction to Formal Languages]]
- [[NFA]]
- [[Regular expressions]]
- [[Context Free Grammars]]
