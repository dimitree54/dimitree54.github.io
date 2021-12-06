# ChNN (Chaotic Neural Network) project
![logo_white](https://user-images.githubusercontent.com/39711437/128076420-c9792357-3d45-4978-84cf-a1b98a036100.png)

## About ChNN
Nowadays artificial neural networks show stunning results, but far those neural networks develop, 
 less they look like biological ones. 
To achieve SOTA results developers introduce a lot of knowledge and hand-engineering into NN architecture. 
GPUs training gives a major boost for NNs, 
 but also introduce extra restrictions for NN architecture forcing strict layering.

Although I appreciate modern advances at deep learning, 
 in my free time I like to play with simpler NN models and observe how they evolve.
I like to think about NN as a bunch of simple units (neurons) connected with each other 
 and all the complex and useful behaviour should emerge from that units local rules.

Keeping that thought in mind I have created ChNN project as a sandbox where I can play with a different units 
 and interaction rules trying to make that units self-organise into something bigger than their sum.

## Principles
Before diving in into coding, I suggest you to familiarize yourself with what I was thinking creating that project.
On the following pages you will find explanation of the ideas and principles which are fundament for ChNN-project.
I hope that pages will give you my inspiration and encourage discussion.

[[ChNN principles]](https://dimitree54.github.io/ChNN/principles/)

## ChNN-Library
Though most of the modern NNs are implemented in Python code, 
 for my non-standard purposed I could not use advantages of GPU acceleration.
So I have chosen Kotlin as a quite CPU-efficient, but still easy to write and read language.
Using Kotlin I have implemented base classes to create, run, evolve chaotic neural networks.

[[ChNN-Library Github repository]](https://github.com/dimitree54/ChNN-Library)

[[ChNN-Library documentation]](https://dimitree54.github.io/ChNN-Library/)

[[ChNN-Client GitHub repository]](https://github.com/dimitree54/ChNN). 
Desktop GUI to visualise your Chaotic Neural Network

### Architecture
To make ChNN-Library users faster dive into developing chaotic neural networks,
 to explain some architectural choices and encourage a discussion about architecture improvement
 there is special page.
There you can find the most important classes interfaces and underlying ideas explained.

[[ChNN Architecture pages]](https://dimitree54.github.io/ChNN/architecture/)

### Contribution
ChNN project is still young single-author hobby project,
 but if you find its ideas inspiring, there is a lot of ways, how you can support project.

[[Contribution page]](https://dimitree54.github.io/ChNN/contribution/)

## ChNN-Contest
To not play in a sandbox myself, I invite everybody to create its own neuron.
All that neurons will be placed together during series of contests.
Communicating with each other and fighting for resources they will try to survive evolution.
Observing properties of the fittest neurons, 
 maybe we can understand better what makes neuron useful and apply those
 principles to improve neural networks solving real problems.

[[ChNN Contest page]](https://dimitree54.github.io/ChNN/contest/). How to participate, rules, dates, results.

[[ChNN-Neurons GitHub repository]](https://github.com/dimitree54/ChNN-Neurons). Zoo where you can submit your neuron.

[[ChNN-Client GitHub repository]](https://github.com/dimitree54/ChNN). Code evaluation contest and GUI to visualise your
Chaotic neural network.

## Author

If you have questions or suggestion not covered by the README, 
you can reach me (Dmitrii Rashchenko) via email (dimitree54@gmail.com)




