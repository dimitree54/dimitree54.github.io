# Chaotic Neural Network
![logo_white](https://user-images.githubusercontent.com/39711437/128076420-c9792357-3d45-4978-84cf-a1b98a036100.png)

[[GitHub repository]](https://github.com/dimitree54/ChNN), [[Author page]](https://github.com/dimitree54)

## About ChNN
Nowadays artificial neural networks show stunning results, but far those neural networks develop, less they look like biological ones. To achieve SOTA results developers introduce a lot of knowledge into NN architecture. GPUs training gives a major boost for NNs, but also introduce extra restrictions for NN architecture forcing strict layering.

Although I appreciate modern advances at deep learning, in my free time I like to play with simpler NN models. In my mind the NN is just a bunch of simple units (neurons) connected with each other and all the complex and useful behaviour should emerge from that units local rules.

### ChNN framework principles
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
 - **Neural democracy**. It is quite a question what local quality to use neuron to optimise and for evolution to rely on. To now 

### Neuron Interface
[[GitHub link]](https://github.com/dimitree54/ChNN/blob/master/library/main/we/rashchenko/neurons/Neuron.kt)
