# ChNN framework principles
[[Principles discussion]](https://github.com/dimitree54/ChNN/discussions/35)

To start my search of that "perfect units" I have started with creating a framework that will test and compare different neurons. That framework contains different rules of how neurons called and their communication protocol. I understand that fixing such rules and protocols I have limited NN potential and hardcoded some of my intuitions (which might be wrong), but I have tried to make these restrictions not too hard. Here is principles which I followed creating the framework:
- **Local communications**. Neuron can communicate only with other neurons directly connected.
- **Egocentric neurons**. That property related to the previous, neuron does not care what happens outside it. It has its own local quality metrics and tries to optimise them (actually it does not have to optimise them, but having lower quality increases chances to be killed during natural selection). To make neurons solve some common task there are some tricks to introduce external quality into local, but still neuron does not know what the common task is.
- **Evolution**. As I have already mentioned neurons have some local quality which is used for natural selection. Note that a target for evolution is separate neurons, but not a whole network (for example like at AmoebaNet) and when one neuron dying, the rest of the network continues operation. That is quite unusual solution that has pros and cons:
    - Pros:
        - We do not have to retrain the whole network
    - Cons:
        - Evolution is not targeted on solving external task.

  You can share your ideas about such evolution setting [here](https://github.com/dimitree54/ChNN/discussions/37)
- **Neural democracy**. It is quite a question what local quality to use for neuron to optimise and for evolution to rely on. To not limit neuron behaviour we have chosen collaborative quality estimation. That is it, neurons decide what the quality is itself. Of course not for itself to avoid interests conflict, but for all connected neighbours. It is quite original solution, you can share your ideas about it [here](https://github.com/dimitree54/ChNN/discussions/39). The advantage of such approach is that quality definition becomes trainable (by evolution better quality metrics chosen). But such a freedom may lead to abuse. I hope that neurons-impostors that abuse possibility to judge others will not survive natural selection, but if they do some external control of outgoing quality may be introduced. Later I will refer that outgoing quality as feedback.
- **Neurons privacy**. To avoid some possibilities for abuse neural democracy some extra rules introduced.
    - Secret ballot. Neuron knows only feedback averaged from all neighbours (and external controllers). So it can not behave like "I will send you bad feedback because you have sent me bad".
    - Anonymity. Neuron does not know the type of neurons connected to it. So it can not behave like a racist: "I will send you good feedback because you have the same type as me"
- **Computations efficiency**. Evolution have to provide a lot of trials and errors before finding something useful. But to provide such an efficiency a lot of extra limitations should be introduced:
    - Binary neuron output. That is quite a big limitation since all modern neural networks are real-valued. But there is some examples of effective binary neurons (in biological NNs, artificial spiking neurons). The binary version is chosen for computation efficiency (on CPU), so near-zero outputs does not take CPU time.
    - Sparse activations. A program optimised to work with a big rate of not active neurons. So only if neuron is active it will take CPU time on the next iteration. High rate of active neurons is supported, so it is not a limitation, it is just an intuition that neurons will converge to sparse activations (like in biological NNs).
    - Single-activation source. Neuron is 'touched' by its neighbours and on each touch it can decide whether activate or not. If it is already activated it will not be touched by other neighbours on that tick to save CPU time. The drawback of that is order-dependence of neuron touching.

So lets overview the main interfaces and algorithms.