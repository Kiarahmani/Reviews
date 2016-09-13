# MaxSAT, Hard and Soft Constraints
###### Chu Min Li and Felip Manya - Handbook of Satisfiability, 2009.  (Note by Kia Rahmani)
---
Remember DPLL algorithm? It is basically a depth-first search algorithm, that at each step makes a decision and later checks if that decision was **fine** or not. Since it targets the SAT problem, **fine** in DPLL means *all* clauses being true. 
What if we generalize the notion of **fine** decisions? Finding a solution to satisfy *all* clauses, although is perfect, but is not reachable sometimes. An assignment that *maximizes* the number of satisfied clauses can be the next desirable solution.

This new formulation lets us reason about the **degree of unsatisfiability** of unsatisfiable formulae - instead of just labeling them unsatisfiable and leaving them. The new problem is called *MaxSAT* and the modified DPLL algorithm -that makes sure all **fine** decisions can only *make the current bounds better* in the future- is called *Branch and Bound* algorithm. In other words, at each step, the algorithm must *estimate* the changes in the lower bound of the number of unsatisfied clauses *for any completion of the current partial assignment*. There are multiple approaches for this guess work: 
- **Underestimations** (such as [star rule](http://link.springer.com/chapter/10.1007%2F978-3-540-30498-2_34) and [UP](http://link.springer.com/chapter/10.1007%2F11564751_31) that give an answer by analyzing the structure of the formula) 
- **Inference** (that try to find a simpler formula with the equivalent answer to the original one; similar to unit propagation technique in PDLL)

Different heuristics and data structures have been used to improve the performance of these solvers. Moreover, approximation algorithms are also developed that give an answer which is guaranteed to be *close* to the optimal solution. 

In order to generalize the problem further, we can mix the SAT and MaxSAT definitions together, by defining the soft clauses (try to satisfy them as many as possible) and hard clauses (they MUST be satisfied). This new formulation that is called Partial MaxSAT, can encode some new combinatorial problems. It also can make great use of already developed techniques of SAT solvers (for example, unit propagation works perfectly for hard clauses!).






