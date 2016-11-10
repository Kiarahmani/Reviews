# A Calculus of Atomic Actions
###### T. Elmas, S. Qadeer, S. Tasiran -- (Note by Kia Rahmani)
---
The paper targets the problem of search space explosion in verification of concurrent programs. As we have seen, there isn't much abstraction done in the cumbersome task of verification using Owicki-Gries technique. However, in this paper, an abstraction method is introduced that soundly reduces the programs into ones with larger atomic blocks, which would obviously reduce the size of the search space. This simplification technique -that only preserves or expands the set of behaviors and thus is sound- is done via two types of iterative local transformation:
- **Abstraction:** an already atomic action is replaced with a more relaxed one, that can show more behavior, such as adding non-determinism to the reads.
- **Reduction:** replaces a number of atomic actions with one new action. By having coarser-gained atomic actions, they can use existing verifications techniques more effectively. The transformation must consider non-interference safety conditions to ensure a sound transformation.

Although these transformations have been studied before, but the contribution of the paper is using them in an iterative fashion: at each round, *reduction* reduces the number of actions and *abstraction* abstracts away from uninteresting details. 

Another property of their technique is the ability to postpone the proof. New proof assertions can be treated just like an abstraction step and can be added at any time during the simplifications. 

The method is implemented in an interactive tool called QED, at which the input program, assertions are dynamically changed until the desired proof of a simple enough (equal) program is achieved. 
