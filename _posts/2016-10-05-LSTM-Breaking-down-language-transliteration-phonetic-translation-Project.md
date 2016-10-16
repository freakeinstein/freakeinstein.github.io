---
layout: post
title: Breaking down 'language transliteration' ( phonetic translation ) Project ( LSTM version )
---

Hi, now I'm going to talk about my major project. You may have read [my post](http://freakeinstein.github.io/2016/05/30/Breaking-down-language-transliteration-phonetic-translation-Project-version-1/)   regarding my mini project, which focused on the same goal of malayalam transliteration. In my previous attempt, I based it purely on basic probability theory. Which applied chain rule to transliterate to malayalam (literally). Now we're going to adapt a state of the art technique which is very popular in this area, which is known as LSTM (Long Short Term Memory). Just before beginning my project, I've did a small research on it and found different papers. I've fallen in love with two simple papers, published one, [by Google](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43264.pdf)  and the other by [ by Microsoft](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/rnnlts.pdf) . No doubt, they have already proven the results. So, my project work is simply an implementation of these papers.

What's LSTM? I'm gonna link a page instead explaining it (its a good practice to get rid of redundancy, right?), here it is. Just in simple words, LSTMs can be used for Sequence to Sequence translation, like Speech to text (record speech, cut it equally), language to language translation (Although very recently Google introduced a [better update](https://research.googleblog.com/2016/09/a-neural-network-for-machine.html)  to their translation tools), characters to phonemes, and more.. we're hackers right? You could use any trick, and if you were able to convert anything to sequence, most probably, LSTM's could help you. If you need inspiration on this, get it from [ andrej karpathy](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) . 

### Our situation:
Now moving into our situation. It's very simple.

- create a simple LSTM which recieves an ASCII character from a sequence as an input and predict next character in the sequence. [in a techie way, we need to model and train a LSTM, which recieves a character in a sequence and produces a probability distribution over next possible characters].

- Our model is ready. What about training data? (funny thing is, before creating a model, you shuld gather your training data. I've described the model already, just to simplify the explanation). I'm gonna write that below: 

### Training data:
I've created a lot of data with examples of mangleesh text and corresponding malayalam transliteration (500000+ pairs). Thanks to SMC community, to create this big set of data, I've used their text [corpus](http://download.savannah.gnu.org/releases/varnamproject/words/) for Varnam (a similar project with different approach) and [shilpa](http://libindic.org/)'s python script for [transliteration](https://github.com/libindic/Transliteration) with a tiny modification (random error character introduction). Since this is done for demonstration purpose, synthesized data is enough.

next steps were the tricky part of my training:

- firstly, I wanted to convert UNICODE characters to ASCII characters. Why? [get inspired](http://freakeinstein.github.io/2016/07/04/Mapping-malayalam-UNICODE-characters-to-8-bits-representation-in-lua-by-preserving-existing-ASCII-characters/) . :)

- Secondly, I need to decide the sequences and their format for representation.

### formatting the data for better results:
For this, we should be tricky. We will be giving one character at a time, both at the input and output terminals of LSTM (as in the form of onehot encoding to be precice, any encoding can be used). So, how do we create these two sequences? the source and target? OR.., do we wanna setup a single sequene for both of them? That's the real question we will be asking ourselves later.

Let's consider an example:
in our problem, suppose we want to map *malayalam* to *മലയാളം*

![fig 1](https://cloud.githubusercontent.com/assets/19545678/19220490/cbf5d880-8e4b-11e6-925f-4e2ecbf2c5d2.png) 

or do something like this mapping:

![fig 2](https://cloud.githubusercontent.com/assets/19545678/19220491/cc14d71c-8e4b-11e6-8ea9-87120d6cb7c9.png) 

from these examples, we can see that, thare's no one-one correspondance between these two sequences. So, during training, we should try out different approaches. According to the papers I refer, they preffered delayed matching, so that, the network  could pre-see more than one characters just before the prediction starts.

![fig 3](https://cloud.githubusercontent.com/assets/19545678/19220492/cc1f3874-8e4b-11e6-9de9-3bc13f224afa.png) 
![fig 4](https://cloud.githubusercontent.com/assets/19545678/19220493/cc21271a-8e4b-11e6-964a-3d68358f46b2.png) 

In the above figure, the network has seen `ma..` earlier, and it could predict corresponding sequence as `മ..`, (where - - is added for two purposes, first two represents some padded characters to indicate the network that, prediction is delayed by two characters and another two at the end is to match the sequence length of source and destination.

A better alternative solution is given below:

![fig 5](https://cloud.githubusercontent.com/assets/19545678/19220494/cc25da9e-8e4b-11e6-8efe-f20adcfe4103.png) 

In the above situation, the network have seen the whole input, just before translation, according to reference papers this one works very well.

### My solution:
I have'nt used any of the above. Actually, I've upgraded to another solution, as given below.

![fig 6](https://cloud.githubusercontent.com/assets/19545678/19220495/cc2bdc3c-8e4b-11e6-815d-be059d9ca3bf.png) 

Here, I've used the same sequence as the input and output with a single shift. Each step during training, we will give a character from the sequence as the input and the next character from the same sequence as the output. Thus our network will learn itself not only the inner patterns of transliterations but, able to generate sentances also. This is actually an adaptation of n-gram algorithm from our mini project, which helped a lot in error correction. Remember?

### here's how my conceptual data looks like:
...samayamaa-സ്മയമാ|
Svarnnamaa-സ്വർണ്ണമാ|
Dhaarmikamo-ധാർമികമോ|
Kaanyatthe-കാണ്യത്തെ|
Thurannile-തുറന്നിലെ...

### fere's how my actual data looks like: (UNICODE to ASCII)
...samayamaa-¸Í®¯®¾|
Svarnnamaa-¸Íµü£Í£®¾|
Dhaarmikamo-§¾ü®¿•®Ë|
Kaanyatthe-•¾£Í¯¤Í¤Æ|
Thurannile-¤Á±¨Í¨¿²Æ...

Later I've replaced Varnam corpus with a long stiched pack [malayalam books](https://ml.wikisource.org/wiki/%E0%B4%AA%E0%B5%8D%E0%B4%B0%E0%B4%A7%E0%B4%BE%E0%B4%A8_%E0%B4%A4%E0%B4%BE%E0%B5%BE)  in a single .txt file [ books were available online as .txt and .epub files. Sometimes, a .epub to .txt converter helped me a lot :) ]. I've trained my network on a workstation with Nvidia GPU (approx. 2000 cores) for two+ days. I was not able to complete enough epoches and further optimizations because of tight project deadline. Anyway, I've started using it.. Whoa, it worked nice with ignorable errors.

**foot note:** 

- deep learning? ask yourself, **Do I have a big pile of data?**

- synthesised data mixed with real data could help a lot in deep learning.

- My LSTM is a modified version of Andrej Karpathy's LSTM [implementation](https://github.com/karpathy/char-rnn)  (I personally like [torch](http://torch.ch/), its faster than other popular python libraries), thus for coding, it took only three or four days including the character mapping stuff.

- funny thing is, It took one 3+ weeks to play with different data formats and network parameters. [ like, God created a radio in 3 seconds and took 3 days to tune a station ]

*but most of my final sem's spent on these,*

- it took 2+ week to Google, where to find malayalam data and related tools :(

- it took 2+ months, first to complete andrew Ng's [machine learning course](https://www.coursera.org/learn/machine-learning) , Nando de Freitas's [Deep learning course](https://www.cs.ox.ac.uk/people/nando.defreitas/machinelearning/)  and to learn and practice deep learning  concepts through torch examples.