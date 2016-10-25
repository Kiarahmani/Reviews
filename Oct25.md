# Code Completion with Statistical Language Models
###### V. Raychev, M. Vechev, E. Yahav -- (Note by Kia Rahmani)
---
The paper addresses the familiar problem of searching and recommending code snippets for partial programs with holes. 
Their method takes a completely new approach toward the solution: Instead of depending on user-provided, high-level specifications and then *translating* them into low-level implementations, it learns regularities from large sample databases, and uses that to suggest likely sequences of method calls for each hole. In other words, the synthesis problem is reduced to *natural language sentences prediction* problem.  They implemented their idea in a tool called SLANG and showed that it can effectively predict correct code completions for real-world examples. 

As it is mentioned in the paper, *real code generation requires temporal information.* This is what distinguishes SLANG from others in practice: They cannot infer any temporal information from the given specifications and thus are bound to simple instantiations, whereas SLANG successfully synthesizes  likely *method invocation sequence* with *proper arguments*.

The method consists of two major part: 
- **Static Analyzer:**  The tool depends on massive real-world codebases, working with which is not very easy. They nicely overcome this problem by creating an *abstract language of sentences*, that records sequences of events over objects. All programs are translated into sets of sentences that are treated like natural language sentences and are fed into a language model generator. A **language model** is a probability distribution over all possible sentences in a language. This is a scalable static task that needs to be done only once.
- **Synthesizer Based on Language Model:** The synthesizer accepts partial programs with holes and translate them into sentences with holes. Then, using the pre-generated language model it can pick the most likely complete sentences in that context, and turn them back into real-code form. The empirical results suggest the completions are always type safe, and most of the time include the code that user is looking for.  
