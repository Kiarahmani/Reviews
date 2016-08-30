## Toward Compositional Verification of Interruptable OS Kernels and Device Drivers 
##### ([Chen et al. PLDI'16](http://flint.cs.yale.edu/shao/papers/device.html)) - Review by Kia Rahmani
-----

Due to their complex design, operating systems are very difficult to verify. Recent efforts have ended up in verifying only small simplified kernels, that are far from being realistic. These projects, do not verify the device drivers and are unaware of interrupts; which are in fact very difficult to verify, due to their non-deterministic behavior. Moreover, Verification techniques used in those works, do not immediately extend for verifying interruptable kernels. 

In almost all system verification techniques, two levels of *conceptual environments* are considered; they can be thought of as different machines, different languages, or as it is called in this paper different *layers*, and verified systems must be proven to behave the same in both environments (We can think about one layer as the specification and the other as the implementation of the system). 
 
In this paper, authors have used modular layer verification for an interruptable kernel and device drivers. This is a challenging task since the presence of interrupts complicates the **contextual refinement** (i.e. the process of proving equivalence of behavior at two different layers). For example, an implementation of a high-level function cannot be easily mapped to its spec, since it can be interrupted by devices at any point, unless we consider all possible interleaving of interrupts and the code, which makes verification unscalable. Moreover, device drivers can interact directly with each other (and not through the kernel), which means even more possible interleavings.

The goal here is to manage the layering process, to get enough isolation to be able to prove equivalence of two adjacent layers, while we consider the possibility of interrupts. 

#### 1- Device Objects
One novelty of their work is the hierarchy of **certified virtual devices**, that are in fact abstract views of the actual devices, their drivers, and memory dedicated to them. This helps to abstract away unnecessary details of the hardware and think about devices as finite-state machines. The current state of each device is the data in its memory, which can be modified by primitives defined at the outer layer. We can think about the whole process as *packing* some modules together, define a higher level interface for this new package, and prove that contextual refinement holds. 
For example, a device O that accesses memory portion M and has two drivers D_1 and D_2 can be first packed with D_1 to create a layer that is an abstraction of a virtual device with primitives. This can be done again with D_2 driver and the newly created abstract device to create another layer and abstract device. 
This process can be done step by step, for highly modular systems such as kernels and drivers, to control the complexity at each step and prove the functional correctness of a large package at the end.
#### 2- Interrupt Model
What explained earlier does not consider the possibility of interrupts. Another novelty of this paper is the procedure of adding this possibility to the abstract devices. 
In the proposed model, unlike what the name suggests, **interrupts do not actually interrupt CPU** from normal tasks. Devices are abstract state machines, that can be manipulated by the environment, and whose state can be *read* by the CPU. Some of the states of the device need immediate care from the CPU, so when CPU learns about them, it can *decide* to perform the interrupt handlers. This pull-based view of interrupts limits the possible interleavings and makes verification easier (or feasible, to be precise). The verification process starts by wrapping devices with interrupt drivers, and defining primitives for environment changes and CPU read/writes until they create a device abstract enough to satisfy the following property:
>The transitions triggered by the IRQ only change the state of
the corresponding device that triggered the interrupt.

This will provide us with enough isolation to prove some sort of correctness of the interruptable systems.
#### 3- Conclusion 
The work described in the paper is a relatively large verification project, that extends the currently verified kernels (such as [CertiKOS](http://flint.cs.yale.edu/certikos/mcertikos.html)) by reducing their trusted base (namely drivers), and making them interrupt-aware. These are in fact two major sources of bugs in actual systems and proving their correctness is a great achievement. The novelty of the verification process is in careful packing of (abstract) entities together, to build up more abstract devices with certain isolation guarantees.



