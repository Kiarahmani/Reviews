# Symbolic Predictive Analysis for Concurrent Programs
###### C. Wang, S. Kundu, M. Ganai, A. Gupta -- (Note by Kia Rahmani)
---
As we have seen before, the verification task in the concurrent program is difficult and non-trivial. That is mainly due to the large number of interleavings possible to happen. 
In order to face this problem the current methods (in 2009, I guess) take two approaches: 
- Conservative analysis techniques that using more abstract models, can cover all possible interleavings **in addition to some interleavings that would never happen** which would result in false alarms, e.g. [lockset analysis](http://yoursubtitle.blogspot.com/2009/11/196-lockset-analysis.html)
- Inspired by Lamport's *happens-before* relation, enumerative methods to analyze as many cases as possible. These methods, although are sound (no bogus errors are found) but fail to cover all cases due to the large search space. 

Methods that use only run-time information -because of non-determinism in concurrent setting- fail to find all corner cases (the erroneous ones that we are interested in) by just simply running the tests. The proposed method in this paper, however, is a new *static analysis* that models causal dependencies based on the program code. This method by using symbolic static prediction, provides *feasibility guarantee* -freedom from false alarms- but manages to cover a broader set of interleavings and consequently find corner-case errors. The key point is that they rely on an SMT-solver fed with an encoding of the causal model, instead of just enumerating interleavings. The encoding is based on transforming the concurrent programs into concurrent static single assignment (CSSA) forms, and has the property of **being satisfiable, if and only if a linearization of the causal model** (a partial order- I guess) **exists that violates the safety of the program.** 

They further improve the scalability of their method by symbolically bounding the number of context switches allowed by each interleaving. The method is implemented in a tool called *Fusion* and is shown to cover more interleavings by matching a more constrained version to the best known previous technique.