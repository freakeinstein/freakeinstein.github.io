---
layout: post
title: Q learning flappy bird game demystified (part 1)
---

Let's place our first babysteps into reinforcement learning. I think, this one will be the very first part of a total of three parts series. In this series of posts, I would like to cover Q learning in reinforcement learning, starting from its pure implementation, through neural network based modification and finally adding computer vision facilities to our game playing system.

### What we are going to do:
We will be using a popular game "flappy bird" for the demonstration purpose. In this article, we will discuss the essential information needed to code pure Q learning algorithm, which requires connection wires to access game data. We will create an independent version (computer vision based) of Q learnng in the later sections.

**Prerequisit**: We will do all our experiments in a java based language library, 'Processing'. You need thorough knowledge on this and basic knowledge on java.

### Reinforcement learning:
Here's the scenario: One or more agents are wandering around in an environment. The agent can be anything, which could perform an action chosen from a set of actions (say A) based on its current state. The states are made available by the environment from a set of possible states (say S) based on the recent action taken by the agent. The agent will also recieve reinforcements as rewards or punishments either from the environment or from within. bla.. bla.. simply, you are an agent in the environment planet earth. You know that, time goes on in forward direction, and you wanna do things in this small lifetime. You are busy taking actions at each moment, and at the very next moment you will be at a new state, because of the action you took. At each state you will be rewarded or punished by either your serroundings or by your thoughts itself. That's all reinforcement learning. The basic concept is this much simple. To develop a model and train it for our purpose, we should create an environment that suits our needs. As a teacher, we need to worry only about the reward or punishment that should be provided to the agent to make it perfect for our requirements.

### Let's hack:
How we are going to represent this with the help of mathematics? Even though you skipped everything given above, the upcoming sections will help you to breakdown the algorithm if you have a premitive brain like mine. Hold on..

First question is, what's the algorithm or what are the steps to be performed to get reinforcement learning (RL) running? Here it is:

**for each** `moment of time` **in** `agent's lifetime` **do** `these steps given below`

- perform the right action, which is suitable for current state.
- learn from reward/punishment that, the last action performed at the last situation was right/wrong.

RL algorithm is simple, right? We could add any logical sub steps to our algorithm as long as the high level steps stays the same. We will be using Q learning to create substeps in the above algorithm. We will examine each of the two steps under seperate sub-headings. Each part will have three sub-parts, `thought process : how we approach the problem` , `data structures` and `solution : conclusion of everything`.

### Step 1 - choose the right action:

**thought process:** 

- how do we select an action from a set of actions? hmm.. We know that, in any selection process, if we could somehow assign scores to each candidate, we've got a justifying method for selection.
- we also know that, the action selection is dependent on current state, so that, for each state we will have same set of actions with different score values.
- now that we have got scores related to actions. We could select an action in different ways, depending on the problem we're trying to solve. Like, calculating probability distribution over actions { (score of ith action)/(score of all actions) }, complex probability functions like this ![salsa](http://www.cs.indiana.edu/~gasser/Salsa/Figs/exploit.gif), or simply choosing the action with highest value :) .

**data structures:**

- if we keep these scores in memory, we could reuse them (it will be used in step 2). It will be cool if we could access them as multi dimensional arrays, like `QScore[states][actions]`. 

**solution:**

- We need a `states x actions` matrix (states or actions can already be multidimensional) to keep our scores as memory, let's call it QMatrix.
- For a specific situation, consider the raw of actions. Perform the action which have the highest score (we chose the simplest action selection function).

### Step 2 - learn from reward/punishment:

**thought process:** 

- We need an equation to update our score based on our achievements for better results in the future. This equation does that updation. Under next sub-heading we will arrive at this equation through very basic thought process. ![q-updateeqn](https://cloud.githubusercontent.com/assets/19545678/19554773/aee3003a-96d7-11e6-8f8e-ac81ec4f7cc2.jpg)

**data structures:**

- same as above.

---

### Deriving update equation for Q learning:

- We would like to teach our agent through reinforcements  to tackle different situations in the environment. Because of that, we want those reinforcements affect the new score calculations. The agent's entire action is purely based on those scores. Let's say that `Qnew` is our new score. Then we could say that, `Qnew = reinforcement`. Okey, that will work because, the agent looks for the maximum score value among available actions, since we will be giving a positive number as the reward and a big negative number as punishment, agent will choose the action with positive value which already succeded.

- This doesn't stop here. We want our agent to be future concious. It must take current actions with future advandages in mind. In the previous case, the agent is blind. It only acts based on last experiance only, and will only look for local advandages. As an example, consider our agent as an ant. It should consider exploring the world for better food resources than being localized to get limited bad food. So, what should be our modification? we will look at one step further, to see advandages, if we took an action. Mathematically, we wanted to add the maximum score available in the next state if the agent decides to take an action. ie, `Qnew = reinforcement + Max. future score available in the new state`. We want to be more flexible on our agent. Depending on the problem we're dealing with, we want to place a control over this foreseeing capacity of agents. Its not a good approach to give same capabilities to every creature in the world we're creating. so we will introduce a `discount paramater` to control future foreseeing capability of that agent. then, `Qnew = reinforcement + (discount) * (Max. future score available in the new state)`. Value of discount varies between `0 <-> 1`. 

- Wow.. our equation is getting better and better. Now what? Yes.. we want our agent be less error prone. There may be situations of uncertainities including, agent's perception errors (like misinterpretations of input senses of the agents), special cases in the environments (since the agent is in learning state, it should be able to differentiate special cases) etc. So what we need our agent to do is, keep old information that learned so far with the new ones. We could modify our old equation as, `Qnew = [Qold] + [reinforcement + (discount) * (Max. future score available in the new state)]`.

- As we did in the case of future vision, we need to introduce another parameter control over the agent, to limit its learning capabilities. more specifically, how fast it should adapt the new changes in environment. That new parameter is called `learning rate`. And thus we could modify the equation as: `Qnew = {[1 - learning rate]*[Qold]} + {[learning rate]*[reinforcement + (discount) * (Max. future score available in the new state)]}`.

We're good. Whoo.. its over. For more information, you could hang in [here](http://www.cs.indiana.edu/~gasser/Salsa/rl.html).

### example problem - a self playing flappy bird game
Since we've explained almost everything, I think I should provide only specifics to break this problem down. Here's an example I've did in processing:

 <iframe width="854" height="480" src="https://www.youtube.com/embed/QggzjNfBKlY" frameborder="0" allowfullscreen></iframe>
 
 find the processing sketch in github: [source code](https://github.com/freakeinstein/flappy-bird-processing-arduino-sketch)
 
 **States:** This is the trickiest part. This is not my idea. I've got this from the internet. For a flappy bird, the only requirement is to be in the air and jump over the pipes. Whatever the pipe's height, the bird should be worrying about its alignment with the pipe's tip. We could represent it with two variables, `width` (current horizontal distance from the pipe's tip) and `height` (current vertical distance from the pipe's tip). Thus we could say that, *whatever may be the pipe's height, each state is a relative position from the immediate pipe's tip*. Thus, the states (relative positions) near to the pipes will help the bird to jump over the tip; whereas, far away states could help the bird to stay alive and keep an average height, always.
 ![flapp](https://cloud.githubusercontent.com/assets/19545678/19556794/729255f0-96e0-11e6-9290-7c934e6053bd.jpg)

**Actions:** `jump` or `no jump`.

**Reinforcements:**

- for each action, chech whether the bird is alive, if so, reward positive value, a large negative value, otherwise; this is to teach the death traps to the bird.
- if the bird crosses the pipe, reward it with relatively big positive value, this is to teach the bird, how to score.
- give a small negative reward for each jump as energy wastage, and small positive value for free fall (no jump) as energy gains. This is to encourage the bird to jump only if it is necessory.

#### future parts

In the furute parts we will look at 

- a way to replace the QMatrix with feed forward neural networks (part 2) [currently working on it].
- a way to introduce computer vision to play by looking, using convolutional neural networks (part 3).