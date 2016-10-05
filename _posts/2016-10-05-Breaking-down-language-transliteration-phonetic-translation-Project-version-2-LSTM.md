#malayalam transliteration using LSTM

[being busy, figures coming soon]

Hi, now I'm going to talk about my major project. You may have read my post regarding my mini project, which focused on the same goal of malayalam transliteration. In my previous attempt, I based it purely on basic probability theory. Which applied chain rule to transliterate to malayalam (literally). Now we're going to adapt a state of the art technique which is very popular in this area, which is known as LSTM (Long Short Term Memory). Just before beginning my project, I've did a small research on it and found different papers. I've fallen in love with two simple papers, published one, by Google and the other by Microsoft. No doubt, they have already proven the results. So, my project work is simply an implementation of these papers.

Whats LSTM? I'm gonna link a page instead explaining it (its a good practice to get rid of redundancy, right?), here it is. Just in simple words LSTMs can be used for Sequence to Sequence translation, like Speech to text (record speech, cut it equally), language to language translation (very recently Google introduced a new update to their translation tools), characters to phonemes, and more.. we're hackers right? You could use any trick, and if you were able to convert anything to sequence, most probably, LSTM's could help you. If you need inspiration on this, get it from andrej karpathy. 

### Our situation:
Now moving into our situation. Its very simple.

- create a simple LSTM which recieves an ASCII character from a sequence as an input and predict next character in the sequence. [in a techie way, we need to model and train a LSTM, which recieves a character in a sequence and produces a probability distribution over next possible characters].

- Our model is ready. What about training data? (funny thing is, before creating a model, you shuld gather your training data. I've described the model already, just to simplify the explanation). I'm gonna write that below: 

### Training data:
I've created a lot of data with examples of mangleesh text and corresponding malayalam transliteration (500000+ pairs). Thanks to SMC community, to create this big set of data, I've used their text corpus for Varnam (a similar project with different approach) and shilpa's python script for transliteration with a tiny modification (random error character introduction). since this is done for demonstration purpose, synthesized data is enough.

next steps were the trick part of my training:

- firstly, I wanted to convert UNICODE characters to ASCII characters. Why? get inspired. :)

- Secondly, I need to decide the sequences and their format for representation.

### formating the data for better results:
For this we should be tricky. We will be giving one character at a time both at the input and output terminals of LSTM (as in the form of onehot encoding to be precice, any encoding can be used). So, how do we create these two sequences? the source and target? OR.., do we wanna setup a single sequene for both of them?? thats the real question we will be asking ourselves later.

Let's consider an example:
for our problrm, suppose we want to map *malayalam* to [malayalam] 

fig1

or like this mapping:

fig2

from these examples, we can see that, thare's no one-one correspondance between these two sequences. So, during training, we should try out different approaches. According to the papers I refer, they preffered delayed matching, so that, the network  could pre-see more than one characters just before the prediction starts.

fig3

In the above figure, the network has seen `ma..` earlier, and it could predict corresponding sequence as `xx[ma]`, (where xx is added for two purposes, first two represents some padded characters to indicate the network that, prediction is delayed by two characters and another two at the end is to match the sequence length of source and destination.

A better alternative solution is given below:

fig4

In the above situation, the network have seen the whole input, just before translation, according to reference papers this one works very well.

### My solution:
I hav'nt used any of the above, actually, upgraded to another solution, as given below.

fig5

Here, I've used the same sequence as the input and output with a single shift. Each step during training, we will give a character from the sequence as the input and the next character from the same sequence as the output. Thus our network will learn itself not only the inner patterns of transliterations but, able to generate sentances as well. This is actually an adaptation of n-gram algorithm from our mini project, which helped a lot in error correction. Remember?

### here's how my conceptual data looks like:
...samayamaa-Mസ്മയമാ|
Svarnnamaa-സ്വർണ്ണമാ|
Dhaarmikamo-ധാർമികമോ|
Kaanyatthe-കാണ്യത്തെ|
Thurannile-തുറന്നിലെ...

### fere's how my actual data looks like: (UNICODE to ASCII)
...samayamaa-M¸Í®¯®¾|
Svarnnamaa-¸Íµü£Í£®¾|
Dhaarmikamo-§¾ü®¿•®Ë|
Kaanyatthe-•¾£Í¯¤Í¤Æ|
Thurannile-¤Á±¨Í¨¿²Æ...

Later I've replaced Varnam corpus with a long stiched pack malayalam books in a single .txt file [ books were available online as .txt and .epub files - .epub to .txt converter helped me for that :) ]. I've trained my network on a workstation with Nvidia GPU (approx. 2000 cores) for two+ days, and was not able to complete and optimize much due to deadline for project submission. I've started using it and whoa, it worked nice even with ignorable errors.

**foot note:** 

- deep learning? ask yourself, **Do I have a big pile of data?**

- synthesised data mixed with real data could help a lot in deep learning.

- My LSTM is a modified version of Andrej Karpathy's torch implementation (I personally like torch, its faster than other python libraries), thus for coding, it took only three or four days including the character mapping stuff.

- funny thing is, It took one 3+ weeks to play with different data formats and network parameters. [ like, God created a radio in 3 seconds and took 3 days to tune a station ]

*but most of my final sem's spent on these,*

- it took 2+ week to Google, where to find malayalam data and related tools :(

- it took 2+ months, first to complete andrew Ng's machine learning course, Nando de freita's Deep learning course and to learn and practice deep learning  concepts through torch examples.