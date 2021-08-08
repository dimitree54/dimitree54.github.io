# Chaotic Neural Netwok contest
![logo_white](https://user-images.githubusercontent.com/39711437/128076420-c9792357-3d45-4978-84cf-a1b98a036100.png)

[[GitHub repository]](https://github.com/dimitree54/ChNN), [[Author page]](https://github.com/dimitree54)

## About ChNN
Nowadays artificial neural networks are showing stunning results, but far those neural networks develop, less they look like biological ones. To acheive SOTA results devlopers introduce a lot of knowledge into NN architecture. GPUs training gives a major boost for NNs, but also introduce extra restrictions for NN architecture forcing strickt layering.

Although I appreciate modern advances at deep learning, in my free time I like to play with simpler NN models. In my mind the NN is just a bunch of simple units (neurons) connected with each other and all the comlplex and useful behaviour should emerge from that units local rules.

To start my search of that "perfect units" I have started with creating a framework that will test and compare different neurons. That framework contains different rules of how neurons called and their communication protocol. I understand that fixing such rules and protocoles I have limited NN potential and hardcoded some of my intuitions (which may be wrong), but I have tried to make these restrictions not too hard. Here is principles whick I followed creating the framework:
 - **Local communications**. Neuron can communicate only with other neurons directly connected.
 - **Egocentric neurons**: that property related to the previous.

### Neuron Interface
[[GitHub link]](https://github.com/dimitree54/ChNN/blob/master/library/main/we/rashchenko/neurons/Neuron.kt)
