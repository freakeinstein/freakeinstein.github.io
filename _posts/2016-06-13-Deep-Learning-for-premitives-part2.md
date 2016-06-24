---
layout: post
title: Deep Learning for premitives [part 2].
---

<h3> 2. from biological neuron to perceptron </h3>

<h4>Biological neurons</h4>

Everything we do as a human is not resulted from simple cell reactions. Human brain is made up of connected neurons, which make us behave as we do.

>The average human brain has about 100 billion neurons (or nerve cells) and many more neuroglia (or glial cells) which serve to support and protect the neurons. Each neuron may be connected to up to 10,000 other neurons, passing signals to each other via as many as 1,000 trillion synaptic connections. 

From recognising patterns, designing great machines and buildings, creating music, remembering beautiful moments, having feelings and emotions.. yes, whatever we do is maintained by this network, by activating each neurons in it. Each neuron will get activated by another one which have immediate connection to it.


Here's a simple model of a neuron. ![a single neuron](https://cloud.githubusercontent.com/assets/19545678/16334957/a4bc6aaa-3a21-11e6-8fc1-aa4a7f48f137.jpg) [[more info](http://neuroscientist.weebly.com/blog/lesson-2-the-materialistic-mind-your-brains-ingredients)]


Working: [ tip: we need those **bolded** information for later use ]

- Dendrites of a single neuron are **connected to the axons of multiple neurons**. When a neuron gets fired, it will produce some chemicals from the terminals of its axons (synapses), so that, the corresponding dendrites of other neurons will get activated. **The strength of these activations may vary**, dependent upon the properties of each dendrite. 

- This will generate a potential difference there, simply, a tiny electric pulse. Suppose, we've got multiple activations at the same time (*because its in a network and thus, each neuron is connected to multiple other neurons*). Just like, multiple battery_cells contributes electric pulse to the neuron, **which means pulses got accumulated ( added )**.

- finally, the reciever neuron need to decide something. Neurons are shy, they need enough energy to wake up. They may be asking themselves, "Should I get excited? Have I got enough energy?" *electric pulses makes a sleepy neuron very happy and excited !* The only constraint is, **it should exceed some threashold** !


<h4>Why computer scientists are interested in it?</h4>

In 1943, Warren S. McCulloch and Walter Pitts developed the first conceptual model of an artificial neural network [[paper](http://deeplearning.cs.cmu.edu/pdfs/McCulloch.and.Pitts.pdf)]. The neurons are much slower in their communication speed compaired to modern computers. Even if they are very slow, they produce far better results than any other computers within a time segment. Why this? the answer to this question not only inspired the creation of artificial neural networks but, other fields like distributed computating also. 

- **neurons form a massive, parallel network**, which enables them to perform computation on multiple data at a time instant. That's a big difference, because, even if we have got super fast computers, they process data sequentially. We've limitations in the implementation of distributed and parallel computations. Its not possible to connect processors in parallel beyond a limit, constrained either by the networking mechanisms available today ( *Remember, brain uses chemical fluids to connect, while we use ethernet or optical fiber* ), or by the processor architectures ( *the way it process stuffs* ). Google, NASA and others believe Quantum Computers could solve this problem ( *n Qbits could be in 2^n possible states, simply means, 2^n computations at a time, like firing 2^n neurons* ).

- **each neuron itself is just a contributor**. In other way, we could compare a neuron activity to that of an ant. A single ant could do nothing remarkable, they have their own purpose, to contribute to a collective activity, which does great things. 

- **They are general models**. Any neuron could contribute to any activity, which makes a network general for any purpose. The same network can be used from visual/pattern recognition tasks to keeping memories, just like the visual cortex of an adult could be trained listen to voices, if wanted, and vice versa.

- **and they are highly energy efficient.**


<h4>from biology to mathematics</h4>
We've seen that, through hardware implementation its not yet possible to implement these neural networks (*we will see an exception in the case of perceptrons later*). So we found that, software based implementation will help us to overcome this limitation. In the following sesctions, I will be converting the above biological concepts of a neuron to a final form called perceptrons, later in the following series of neural networks, this same procedure will be used to generate neural networks. I'll try to write that as soon as possible.

<h3>Perceptrons</h3>
---------- < editing in progress > ----------