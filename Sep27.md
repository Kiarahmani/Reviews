# Invariant Generation - Chapter 12
###### (Note by Kia Rahmani)
---
The chapter describes the notion of program invariants and how they can be used to define and prove the correctness of some domains of programs.
- **Weakest Pre-condition:** For a given F (formula) and S (program statement), wp(F,S) is defined to be the formula that if is satisfied in initial state of S, after executing S we will end up in a state s' that satisfies F. (wp is a condition on initial state that is *enough* to satisfy F at the end ) 
  - Consequently, verification condition for a program trace is defined as: {F}S1; . . . ; Sn{G} : F ⇒ wp(G, S1; . . . ; Sn) 
- **Strongest Post-condition:** Similarly, sp is defined to be the conditions on final states that if are satisfied, it means the execution has started from a state satisfying F.
  - Consequently, verification condition is defined as: {F}S1; . . . ; Sn{G} : sp(F, S1; . . . ; Sn) ⇒ G

In **static analysis**, our aim is to find mappings from program locations (syntactical place-holders) to FOL formulas, that satisfy verification conditions (defined above), for *all acceptable traces* (In other words, *without executing the program*, we want to assign *some information* to the final state of all possible executions)

The basic approach of finding these mappings, is **symbolic forward propagation**. This algorithm iteratively tries to find the exact set of reachable states (states are represented abstractly by logical formulas), and update the potential mapping μ (that initially maps all non-zero locations to ⊥). The key idea is to pick a location and make sure that the *sp* of current mapping satisfies mapping of final location for a path. If so, we have reached the correct answer. Note that, this algorithm is not guaranteed to terminate. 

To address the above limitaions **Abstract interpretation** is introduced, that by over-approximating reachable states, can guarantee termination (Similar to what we already saw in bounded model checking and interpolation based *complete* model checking)

What follows briefly explains this approach, using two instantiations (Interval analysis and Karr's method).
- **Pick an abstract domain D:** definition of the syntactic class formulas of interest: c>v and c<v in IA and polynomial equations in Karr's method.
- **Define mapping from FOL to D:** this mapping, connects formula F in FOL to element P in D, such that: F ⇒ P  
(Note that we might lose some information here, which would result in over-approximation, which is fine. For example, 0 ≤ i ∧ i ≤ 0 ∧ 0 ≤ n is mapped to: i=0)
- **Define an abstract sp:** the similar notion of sp, but *in the abstract domain D*. 
- **Define abstract disjunction ⊔:** again, the definition of a general notion, inside the domain. It has to satisfy the following property: (F1 ∨ F2) ⇒ (F1 ⊔ F2) and (F1 ⊔ F2) ∈ D
- **Define abstract implication checking:** in symbolic execution at each iteration, implication of the current assignments from the sp of the trace is checked. The notion of implication must be translated in domain D, such that it would be decidable.
- **Define widening:** The transformations defined above, do not necessarily guarantee termination. A widening operator must be defined that would assure convergence in an infinite sequence of formulas of interest. This requires heuristics to guess an over-approximation to the sequence.  

