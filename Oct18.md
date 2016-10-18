# From Program Verification to Program Synthesis
###### S. Srivastava, S. Gulwani, J. Foster -- (Note by Kia Rahmani)
---
*Can a synthesis problem be reduced to a verification task?*  
That is the main question answered in this paper and is shown to be possible to some extent.
Authors created a framework to **specify synthesis tasks**, that are later reduced to **three sets of constraints** and are solved by making use of a proper program verification tool. The approach is correct by construction, since the program is synthesized alongside its proof. 
The framework requires users to specify the synthesis task by providing the followings (additional to the functional behavior, of course) : 
- Flowgraph Structure: Specify the outline of the code: for example ◦;∗(◦) means **do something; repeat something**.
- Domain Constraints: domains of guards and expressions, e.g. linear arithmetic.
- Resource Constraints: The bounds on the number of extra variables and usage of each operation.

The key point in reduction from synthesis to verification is that program statements can be written as *equality predicates* and acyclic fragments as *transition systems*. Their approach successfully infers correctness invariants, control flow guards for the transition system and the predicates that represent program statements. They also create *guard well-formedness* and *progress constraints* as more constraints to the verification problem, to rule out the possibility of synthesizing uninteresting, trivial programs. 

They evaluate their tool with different test cases: problems with easy specs but with different, difficult or non-trivial implementations. (I think) the added load of the synthesis on the solvers -in some cases- is not larger than the verification task. This means they are only bound by the performance of the underlying solvers. Consequently, the tool is successfully tested on some difficult benchmarks even for verification. 






