## Neuron Interface
[[GitHub link]](https://github.com/dimitree54/ChNN/blob/master/library/main/we/rashchenko/neurons/Neuron.kt)

```kotlin
interface Neuron : Activity {
    override val active: Boolean
	fun touch(sourceId: Int, timeStep: Long): Boolean
	fun forgetSource(sourceId: Int)
	fun getFeedback(sourceId: Int): Feedback
	fun update(feedback: Feedback, timeStep: Long)
}
```

Each neuron have `active` property to specify is it active or not.

There is a `touch` function which the function through which neurons communicate. It has two arguments 'sourceId' - id of the neuron that touches current neuron. Note that all neurons during creation get unique id which is used as a nickname for such functions as `touch`, `forgetSource`, `getFeedback`. Using nicknames provides neuron privacy that is described above. The other argument of the function is `timeStep` which is number of tick of the hosting neural network. We need that `timeStep` for neuron how much time has passed as because of efficiency reasons any function of the neuron may be not called on some time step. For example neuron may want to save `timeStep` on touch to later use it on `update` to understand is that `touch` and `update` from the same NN tick. If the `touch` received it means that neuron with `sourceId` was active on the previous `timeStep` and propagates that activity to its neighbours. Based on that and some internal state neuron can become active itself (or not). In that case it changes its activity property AND returns true from the touch. Otherwise, it returns false. That output value kind of duplicate `active` property, but the purpose of it to notify caller that the neuron become active exactly from that touch, which maybe useful in multithreaded NN.

The next function is `forgetSource`. It is quite simple, if NN sure that there will be no touches from that sourceId (for example if source dead or connection cut) it notifies the Neuron about it, so it can clear resources (for example do not store weight for that source anymore).

The function `getFeedback` requests Feedback for the neuron with that `sourceId`. Usually it is requested for the neuron that recently touched current neuron, but sometimes it is not. So be ready to return feedback for any sourceId (use some default feedback if source unknown).

The function `update` is called to notify neuron about it is current 'score' - averaged feedback from neighbours + averaged with some external feedback from controllers + there is also averaging through time. In that function neuron can try to change its state to increase feedback in the future. Usually that function called after successful touch (that lead to activation of a receiver), but also it can be called to notify neuron that it has very low feedback and is a candidate for removal. Also in that function neuron can decide to stop being active for the next tick.

## Environment
Environment is a set of Activities not controlled by a network. That activities can be considered as an input for the network. To introduce one of that inputs into the network we choose one of the neurons and mark it as ["Mirroring"](https://github.com/dimitree54/ChNN/blob/master/library/main/we/rashchenko/neurons/MirroringNeuron.kt). In that mode neuron instead of its own activity value it returns environment activity value (mirroring it). Also instead of usual average feedback at `update` function it receives custom feedback based on mismatch of the Environment activity value and internal one. You should take it into account that all neurons should be able to operate in that mode.

## Neural network and evolution algorithm
[[link]](https://github.com/dimitree54/ChNN/blob/5843a04acedcaf3dae095878c425660d3d7b98a8/library/main/we/rashchenko/networks/StochasticNeuralNetwork.kt#L65)
1. For all neurons active on the previous tick (no neurons for the initial tick) we touch all of their neighbours. Keep in mind that if some neuron supposed to be touch by several neurons we try to touch it only until activation, all the following touches omitted (but it is not guaranteed because of multithreading).
2. If the neuron activated on touch we add it to special collection (which will be used in the step 1 on the next tick). Also, we update feedback for the neuron that caused that activation.
3. We call `update` for all neurons active on the previous step (the same collection as in step 1). Neurons active on that step will be updated on the next tick, so anyway all neurons will be updated soon after activation.
4. We add to that special collection from the step 2 all neurons that was active on that step and still active.
5. We add to that collection all active Mirroring neurons. So we check Mirroring neurons activity on each tick to not miss if environment state changed.
6. (With some small probability) Turn on external controller for the next step, so it can record neuron stats. That stats will be used to calculate some external feedbacks. That way we can control evolution. For example, we can penalise neurons that are too slow or active too often or active too rare and so on. That step is quite expensive (especially because we are updating feedback for all the neurons not only active) that is why it is called rarely.
7. (With some small probability) Launch natural selection. We examine feedback for all neurons (even not active, so it is expensive, that is why we do it rarely), choose several the worst neurons and warn them about it calling `update`. If some neurons appear in that losers list too often (on different time steps) we remove them (and notify network and samplers about it) and replace with new neurons. Note that there are special rules for removing mirroring neurons to not lose connection to the environment.
8. Increment timeStep and continue from step 1.

So you can see how we try to avoid unnecessary computations for non-active neurons.

## Neuron sampler
If you have written some custom neuron its parameters probably can be initialised with different values, some of them better, some worse. If you want track what initialisations was better and make that values more probable you should use NeuronSampler for you Neuron type. It can track the feedback and check if it is still alive for any neuron sampled from that sampler.

Also, there is a wrapper for a collection of different neuron samplers. That wrapper randomly samples neurons of all types with different probability. That probability depends on average quality of all neurons sampled with the same type. So more successful neurons sampled more often. That score will be considered as main metric in the contest.