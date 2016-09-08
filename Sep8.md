# Satisfiability Modulo Theories
###### Barrett et. al - Handbook of Satisfiability, 2008.  (Note by Kia Rahmani)
---
###### Are SAT solvers good enough? 
Unfortunately, No. Although, there have been great improvements in the quality and quantity of SAT solvers in the recent decades, but no matter how fast SAT solvers become, there are some problems that can be naturally expressed only in richer languages, such as [FOL](http://mathworld.wolfram.com/First-OrderLogic.html). 
###### Like what?
Even very simple tasks like finding natural numbers a, b, c and d such that:
``` Haskell
2a > b + c AND 2b > c + d AND 2c > 3d AND 3d > a + c 
```
become too complex when is encoded using boolean variables. Moreover, the translation process itself is not trivial at all: We have to come up with constraints to limit the solutions, based on our [**interpretation**  of natural numbers and relations between them](https://en.wikipedia.org/wiki/Presburger_arithmetic).

###### Why not use a richer language to get rid of this complex translation?
Sure we can! Instead of finding large translated CNF formulae, we can naturally express a lot of problems - *in the above example, almost as naturally as human English description of the problem* - by using richer languages. But there is a problem! these languages like FOL are undecidable. 

###### Should we give up?
No! we are NOT looking for all solutions over uninterpreted functions and relations over all domains of variables. We have a background **theory** of natural numbers and we want an answer over that theory. We should try using that information to help SAT solvers to find answers over higher order logics. 
***
The paper is served as a self-contained description of the theory and practice of **SMT solvers**. The first part of the chapter, explains the formal definition of **First-Order Theories**. Through multiple examples, we can see that in fact, very interesting problem domains can be encoded as formal theories. 
The paper continues by explaining two major thread of SMT solvers design:
- Eager approach: is the straightforward translation of the problem into CNF formulae, that are fed to current SAT solvers. As mentioned in the discussion above, this translation can be very slow and create very complex inputs for SAT solver. The strength of the approach comes from the ability to use normal modern and fast SAT solvers with no modification. 
- Lazy approach: is the approach explained in the discussion above. As opposed to eager approach, here we actually make use of our interpretation of the background theory. In practice, some trivial facts about the theory (like associativity of + in arithmetic) are *discovered* by eager solvers. This is not the case in lazy approach, where theory-specific solvers are created for each problem domain that already *know what we know* about the problem and try to find the solution. 