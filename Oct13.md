# Combinatorial Sketching for Finite Programs
###### A. Lezama, L. Tancau, R. Bodik, V. Saraswat, S. Seshia -- (Note by Kia Rahmani)
---
Sketching has been shown to be a powerful technique for taking off the burden of writing and maintaining complex programs, from the developer's shoulders. Previous works -[StreamBit](http://people.csail.mit.edu/asolar/StreamBit/pldi05-streambit.pdf)- effectively create fast and sound cipher implementations. The technique uses *domain specific rewrite rules* to transform **specs** (defined by the developer) to **real implementations**. However, writing partial rewrite rules is a non-trivial task and requires intense domain specific knowledge of the written code. 

Current work, addresses these limitations by introducing a **combinatorial synthesizer**. It lets the programmer write **partial code with holes** as sketches. Furthermore, it relies on a **verifier** to search the hole-completion space *completely* and filter-out the incorrect ones. The verifier reduces the correctness of an implementation to [quantified boolean satisfiability](https://en.wikipedia.org/wiki/True_quantified_Boolean_formula) and either finds a counter-example or guarantees the correctness.  The new work, is limited to *finite programs* (finite input space and guaranteed termination, that includes interesting cases such as some kernels). Furthermore, it successfully introduces a new approach of thinking about sketching technique, as  "writing partial programs with holes" (no domain specific transformers required) and develops the necessary tools and languages to write sketches and specs and to define different types of holes. 

The approach is shown to be effective by testing it over multiple benchmarks. The tests show that the synthesis time is much larger than the verification time, and the final time is not bound strictly to the size of spec. 















