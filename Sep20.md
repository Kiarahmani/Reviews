# Symbolic Model Checking without BDDs
###### A. Biere, A. Cimatti, E. Clarke, Y. Zhu - TACAS 99.  (Note by Kia Rahmani)
---
Model Checking is a verification approach, that can automatically check systems behaviour -modeled as a finite automaton- with a temporal logic specification. This approach is fast and easily generates counterexamples; however, **state-explosion problem** can occur: The number of global states of a concurrent system with multiple processes  is exponential in both the number of processes and the number of components per process. To tackle this problem, BDDs have been introced to encode the state machine that led into creation of [symbolic model checking](http://www.kenmcmil.com/pubs/thesis.pdf). symbolic model checkers were capable of handling real-world systems with hundreds of state variables. However, even BDD based checkers eventually became obsolete; good BDDs generation for very large systems, was difficult and required manual help. 

In this paper, authors introduce the new technique of *bounded model checking* which is a simplified version of the problem, that only considers the counterexamples of a limited size. The method reduces the problem of finding a counterexample of a maximum size k, to a SAT problem. The reduction can be done in polynomial time for [LTL](http://www.cds.caltech.edu/~murray/courses/afrl-sp12/L3_ltl-24Apr12.pdf) model checking. A high level abstract explanation of the idea follows:

- Suppose you want to prove that a propoerty *P* eventually holds in a state machine. You can translate the problem into finding a path that *P* never holds in it. Instead of considering arbitrary large paths, you can limit yourself to paths of a fixed size *k*. With a little care, you can come up with a formula that is satisfiable, if and only if there exists a path of length *k*, that *P* would never hold in them. This is possible, because transitions, and states are finite, so you can create propositions stating undesirable states and valid transactions.

By itereating this procedure over different limits, we can get some advantages: Small and trivial counterexamples would be found very quickly. Moreover, it does not require any large data structure or human intervention. 





