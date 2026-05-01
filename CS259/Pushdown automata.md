
The formal definition of a push down automation is similar to a finite automation, except for the additional stack. Te stack is a device containing symbols drawn from the alphabet

The machine may use a different alphabet for its input alphabet $\Sigma$ and its stack alphabet $\Gamma$ 

Formally a push down automata is defined as

$(Q, \Sigma, \Gamma, q_0, F, \delta)$ 
[[introduction to Formal Languages]]

Each operation or function from one state to the other contains not only a letter, ($\epsilon$ is allowed as a letter) but also a stack operation 
- $\epsilon \rightarrow a$ adds a to the stack
-  $a \rightarrow \epsilon$ Removes a from the stack
-   $a \rightarrow b$ "swaps" a for b in the stack
- $\epsilon \rightarrow \epsilon$  Does nothing

Each transition needs not only to consume a character but have some kind of this operation

A run of PDA P on $w \in \Sigma ^ *$ is a finite set of configurations for which there exists $w_1, w_2, w_m \in \Sigma _ \epsilon$ st and $p_0 = q_0$

## Related
- [[introduction to Formal Languages]]
- [[NFA]]
- [[Context Free Grammars]]  