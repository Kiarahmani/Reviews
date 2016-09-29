# Software Model Checking
###### (Note by Kia Rahmani)
---
The paper is a survey of *software model checking* developements over the past few decades. Specifically, it focuses on automated techniques on program reasoning, a problem that cannot be solved, in its general definition.  As we have seen previously, the problem of symbolic model checking can easily become untractable. To avoid this problem of state-explosion and incompleteness, we saw how abstract interpretation could help. As an example, we studied how interpolation-based model checkers overcome this problem. This paper describes the same approaches in more details.  
###### Abstraction:
The main idea here is that, we can deal with the incompleteness and exponential space growth, by losing some precision. We have seen this before, when we studied over-approximation methods. By defining an abstract domain, we can *capture only the interesting propertie of executions*. We can think of this abstracting step as a reversed compiler, that maps a lower level language to a higher level one. 
The [reachability problem](https://en.wikipedia.org/wiki/Reachability_problem) can capture interesting safety -how about liveness?- properties of programs, and all abstracting techniques must be proved to be correct with respect to this problem. In other words, if there is a path in concrete domain, from an initial state to a final one, there must be also a similar path in the abstract domain -but not vice verca-
Abstraction can be done in two different direction: 
- Data-abstraction: Polyhedral (high dimension space and sets, to abstract program variables), predicate (fixed and finite set of formulas, that is abstracted by the smallest *implication-core* of each region)
- Control-abstraction: path-insensitive (stets are considered, as long as they are achieved from *some* executions -explicit executions are relaxed), flow-insensitive (The program order is abstracted away, by considering a multiset -instead of a sequence- of operations)

###### Refinement:
One interesting question is how we can make use of spurious counter-examples in above examples. We know that they happen because of over-approximation in the abstract domain, so we can use them to extend the domain in order to rule them out from possible abstract execution. The general approach here is to repeatedly run the abstract-model checker and determine if the unsafe answer is genuine or not. if not, refine the abstraction and repeat. One important required property of refinement techniques used here, is **relative completeness**. This -not so trivial- property states that the refined abstractions, would eventually converge and the procedure is complete. There are multiple refinement techniques based on counter-examples explained in the paper, that all try to add more constraints on the executable paths. This is done by modifying the *trace formula* -which is satisfiable iff the specified path exists-
- Syntax-based refinement: works by finding the unsatisfiable core of the trace, and consequently modifying the abstraction.
- Interpolation-based refinement: Is a more general technique, that not only rules out the one given counter-example, but it also determines other counter-examples (and rules them out), that are logical implications of this counter-example. 


