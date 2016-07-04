---
layout: post
title: Mapping malayalam UNICODE characters to 8 bits representation in lua by preserving existing ASCII characters.
---

In natural language processing, when it comes to UNICODE text processing, it becomes slightly complex task to manage this unicode character, especially when it requires to randomly access characters from a sequence. Because of UNICODE's very clever encoding, it is inherently sequential and a headache during random accesses. Possibilities are limited and we need error control and other corrective mechanisms to do so. Thus, most of the times, its a good idea to understand what our domain of unicode characters and map them into byte representations as ASCII characters do.

Some mapping techniques are already out there, like the `WX mapping` used for indian characters. What this does is, they map each unicode character to a unique and pronetcally similar ASCII character. like, 

- a for അ.
- A for ആ.
- i for ഇ.

Recently, I've encountered the same problem where a character mapping is needed.

<h4>Situation:</h4>
As part of my academic major project, which deals with current generation Malayalam text data, I realied that almost all web or books uses a mixed approach. Malayalam text, nowadays is not purely malayalam. It will contain both Malayalam and English words to complete a maeningful sentance. Inorder to deal with it, we must consider common English words as well, as part of ordinary Malayalam vocabulary. Sometimes these English words are written using English characters or sometimes written with Malayalam characters.

<h4>Advandages in lua:</h4>
My project is being developed in lua language to avail Torch support. Another remarkable feature of lua which helps me is that, lua string uses `eight bit clean` representation for each characters. We know, a byte (8 bit) could represent `2^8` (256) different data, and ASCII characters require only first `2^7` (128) positions reserved to represent characters. Now, because there's another 128 rooms available, we're very much free to use them.

<h4>Malayalam UNICODE</h4>
![unicode table](https://cloud.githubusercontent.com/assets/19545678/16567892/5f8f96b4-4241-11e6-80d9-42cebdf14b4b.jpg)
From this table, we can see that, Malayalam character set requires only 128 positions in whole UNICODE. Whoa.. we could easily map them to occupy those 128 rooms available after ASCII reservation.

<h4>Coding</h4>
Since its very hard to type in these remaining 128 characters using keyboard, we will make use of `lua`'s `string.byte( give_me_a_character )` and `string.char( give_me_a_number )`. everything else is very much easy, just play with `lua`'s `table` datastructure.

Here's a quick evaluation of different `lua chunks` needed for the mapping code: [jupyter notebook](http://nbviewer.jupyter.org/github/freakeinstein/quick_torch/blob/master/character%20mapping%20tests.ipynb).
Here's the final code: [jupyter notebook](http://nbviewer.jupyter.org/github/freakeinstein/quick_torch/blob/master/Character%20Mapping%20clean%20code%20as%20function.ipynb)

> Note: Create a Malayalam text file before running the final code: `/data/malayalam_in.txt`.
> 
> Indian Script Code for Information Interchange works this way [wikipedia](https://en.wikipedia.org/wiki/Indian_Script_Code_for_Information_Interchange).