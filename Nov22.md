# Context-Bounded Model Checking of Concurrent Software
###### S. Qadeer, Jakob Rehof -- (Note by Kia Rahmani)
---
As we have seen, due to its very large search space, the verification problem for concurrent programs is usually simplified by one the following approaches: using a -coarse enough- abstraction of the programs that enables checkers to handle the taks, or reducing the size of the search space by different structural limitations on programs. However, the first approach suffers from false alarms and the second might not be able to represent very interesting programs. 
In this paper, the authors introduce the very first formal method of bounded model checking for concurrent programs. They show how the correctness can be defined and proved for concurrent programs, whose number of context switches is fixed.  
The approach is unsound in general sense (like any other bounded model checking technique) however, has a few strong points: 
- Allows the formal definition of the bounded correctness, which is proven to be decidable
- Search space is only limited by the number of context switches, and experimental results show that in practice most of the bugs manifest themselves in few context switches
- In a single context of one thread, executions are *fully explored* (to handle local unbounded space of executions paths, the recursive calls are treated as switch point, which allows the verification of one thread in the similar fashion **-I am Not sure about this part-**)
- The number of context switches is fixed, but can be arbitrarily large: An example in the paper shows a bug that is manifested after 4 context switches, but *KISS*, a checker that is extended in this work, can only consider 2 context switches. 
- It supports unbounded number of parallel threads

The main bug-finding problem in this work is reduced to the **context-bounded reachability problem for concurrent pushdown systems**. They formally define and make use of push down systems as abstract finite representations for their concurrent programs, to be able to deal with a potentially unbound number of local configurations at each thread -due to recursive calls. This way, they can prove termination which makes their method complete. The programs with the ability of dynamic thread creation are also covered in an extension of their technique, which makes it more suitable for real-world problems.
