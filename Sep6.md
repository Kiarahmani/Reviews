# Conflict-Driven Clause Learning SAT Solvers
###### Marques-Silva et. al - (Note by Kia Rahmani)
---
The paper is dedicated to explaining modern SAT solvers, namely Conflict-Driven Clause Learning solvers. As the name suggests, this algorithm uses **conflicts**; that are found while **unit propagation** procedure of **DPLL** is being executed.   
- [DPLL](http://www.cs.cornell.edu/courses/cs4860/2009sp/lec-04.pdf): Is a recursive procedure for solving SAT problem in O(2^{n}). The recursive calls are given a simpler formula to check; which is derived by removing clauses that are satisfied by our decision (*like all backtracking procedures, here also a decision is made at each level, whose correctness is checked later and consequently revised*). At each step a decision assigns a value to a variable, if derived simplified formula is nat satisfiable, another value will be assigned (obviously, if again the simple formula is unsatisfiable, we can conclude that the larger formula is also unsatisfiable).
- [Unit Propagation](https://en.wikipedia.org/wiki/Unit_propagation): Is a very intuitive Analysis of clauses, considering the properties of CNF formulae: (a) If all literals in a clause are *false* but one, that literal must be *true*. (b) Since now we are sure about the value of a literal, we can remove it carefully from the rest of the clauses and modify what remains. 

- Conflict: state of the formula that shows unsatisfiability of it. More precisely, there is a clause that is not satisfied. In backtracking procedure, when conflicts are detected, the last decision is falsified and other options - if exists any - are considered.

CDCL algorithm improves brute force behavior of DPLL, by maintaining an [*implication graph*](http://dl.acm.org/citation.cfm?id=244560), which would allow jumping back (while back-tracking) non-chronologically. In other words, transitivity of *Implies* relation, has some information that would help us to skip some trivial cases. The following graph depicts this observation: The brute force approach of DPLL compared to CDCL is obvious.

![DPLL](https://github.com/Kiarahmani/Reviews/blob/master/CompareCdcl_dpll1.png?raw=true "DPLL") ![CDCL](https://github.com/Kiarahmani/Reviews/blob/master/CompareCdcl_dpll2.png?raw=true "CDCL")
