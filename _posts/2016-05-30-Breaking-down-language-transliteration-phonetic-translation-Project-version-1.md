---
layout: post
title: Breaking down 'language transliteration' ( phonetic translation ) Project ( version 1 ).
---

As my first academic project, I've chose to develop a self learning English - Malayalam phonetic transliterator, where the end user could type in Malayalam words by their phonetic alternatives through a English keyboard. Although such commercial projects are already available, I've decided to give it a try through my own implementation, as a babystep towards modelling self learning algorithms. The backbone of this project is made up of basic probability theory and operations, with which both decision making and learning mechanisms are functioning. Here's a brief note on how it is done:

# Let's breakdown the problem *( Maths not covered )* 
Starting from an application area for this project, say a facebook chat box, where an average 'malayalee' including me, communicates this way;

`Hai da, enthokkeyund vishesham ?`

`Sukam, ninakko ?`

`kuzhappamilleda.. Entha paripaadi ?`

Except for some people *( May be, some girls, not much coding needed :P )*.

req: `10101010101010100010100101010100101`

resp: `K`

req: `01001001100101010110101010001010101 0101010101001`

resp: `mm..`

req: `0110101010001010101101010101001`

resp: ` (a perfect, period seperated) Ha..Ha..`

So, what's happening within our heads while we read these text? Don't bother about the biological complexities or human psychology, Let's interpret the basic feeling that we get, and it should work. For me, I think, it can be explained with three layers of filtering. The given in the fig. below and they are, **Knowledge**, **Experience** & **Memory** *( call this, an 'Architecture' because some people need architectures so bad )*.

![architecture](https://cloud.githubusercontent.com/assets/19545678/15669804/c5735c94-273f-11e6-9967-d1cf3501614d.jpg)

## the knowledge layer
we need to teach a **kid**, some basic rules so that, he could convert English inputs into some rough Malayalam words, each tagged with their own likelihood *( probability )*.

**Module design**

![knowledge_layer](https://cloud.githubusercontent.com/assets/19545678/15669808/c5b8ce32-273f-11e6-9cd9-170086ee7899.jpg)

- First of all, we need to create a **Rules** file manually. Here's the format for each row:
`eng_chars_1 : mal_char_11 | score_11 - mal_char_12 | score_12 - ...`

`...`

initially, all the score values are reset into a probability value of 1, so choosing a corresponding Malayalam character for an English character combination is equally likely *( this will be varied on each training iteration )*.

- to create this rules file, **guidance from a language expert is needed**.
- next step is to combine these seperate Malayalam chareacters to form some rough words set, with their combined probability.
why we need these probability values to be combined? because, after each training process, the likelihood of these words increase or decrease our confidence level, based on that we could sort our results.

## the experience layer
we've got some Malayalam words from layer 1 sorted by their confidence to match our input. In most cases, it may not be the actual result we wanted, rather will contain impurities. Some adjacent textts may be unusual or may never occuer. For example, input Malayalam may return some sequence like this: **മ്ലയാളം, മാലയളം, മളയളം, മ്മല്യാലം, മലയാലം**. Here, **'മ്ല'** and **'മ്മല്യാ'** are unusual words with probability of occurence nearly zero. Thus we could eliminate or underrate these words by their sequence pattern properties. This is actually based on our experience in dealing with different malayalam words. 

![architecture](https://cloud.githubusercontent.com/assets/19545678/15669805/c57e9532-273f-11e6-8bec-57665249a832.jpg)

- the approach we use here is **n-gram** model. We have already trained the **n-gram** model over a big set *(billions)* of **different** Malayalam words and  will generate ranks or probability values for each **n-gram** combinations.
- we will then re-rank our results by mixing these **n-gram** probabilities as well. A simple sorting and threasholded elimination could give us a better & confident results.

## the memory layer
Memory plays major role in our decisions. We could make corrective thinking based on some memory references. Its like determining a best route in worst cases if we already have a basic map in our memory, or recollection some old memories for approximation and matching some patterns. In our example, we've got some Malayalam text. Before presenting it to the user, we must do some memory aided crosschecks, " *Have I heard this word ever before ? If so, what's that smallest correction required to make this result to match my memory ?* " **Remember this, a 'Replace', 'insert', or a 'delete' operation on minimum number of characters** will help us to accomplish this task. This is the technique behind almost every spell checker algorithms. We could specify these minimum edits limit and if the correction lies within these minimum edits... You know.. give the user the word fom memory, else, let your confidence shine !

![architecture](https://cloud.githubusercontent.com/assets/19545678/15669807/c5af6d38-273f-11e6-8b45-9b5a0f7dcc82.jpg)

## not over, we need a continuous training phase
After passing an input through these three layers, we're placing it to the outside environment with some confidence level and we're waiting for a response. We will either get a fail response along with the correction or we will get a success response. In case of fail, we will be using this new information to modify the weights values in layer 1 and 2 and to adding it to memory if its a new entry to the system.

**NOTES:**

- **Layer 1** : we could use a '**trie** datastructure' or a 'python **dictionary**'. I've mentioned only manual method for rule generation, we could make use of decition trees to automatically adapt and modify the rules, training data should be designed to cover all the possibilities in this case. This layer can also be replaced with other existing '**G2P** methodologies' like using '**Weighted Finite State Transducers**' or '**Recurrent Neural Networks**' *( I'm trying to extend my mini project as my major using RNNs, just started working on it, let me se if I could blog events alongside with it )*.
- **Layer 2** : uses an **n-gram** model in my implementation. '**2-grams**' best worked for me. Another yet better alternative is to use '**Recurrent NNs**'.
- **Layer 3** : implemented with **shortest delete distance** spell checker *( according to developers which is very much faster )* For commercial application, a stemmer is necessory, otherwise your database will be flooded.
- **Training data** : I've struggled a lot, there's no corpus for malayalam transliteration. So, I've used a rule based automation algorithm to generate test cases, so I needed to enter the english letters as it is produced by the algorithm for testing. *( good news is, for 50+% cases, the system managed to give better results even if the rule is not followed )*.
- **Major problem** : I works out of the box for very common words, but, for very specific inputs *( whose characters are very uncommon, or insufficient )* system fails in prediction and produces very bad results.
- **Existing Commercial systems** : 'Google input tools' , 'Varnam free'.
- **Summary representation** :


![idea](https://cloud.githubusercontent.com/assets/19545678/15669806/c5a8fd22-273f-11e6-90d7-1b84b7340231.jpg)