---
layout: post
title: I struggled a lot to get started this first article as a minimalist. How I decided best suitable tools for me.
---

Writing a blog was a painful task for me. I've tried different tools and services available, as my friends and other writers suggested. It was painful to write and publish articles, but its even more complicated to maintain the text content on the go. So, after a long break I've decided to give it a **try** *(It may take another full page to explain why now)*. This time, I wanted to throw myself into analysis on what tools and writing environments I actually wanted.

###Lets go through the curation process###


*  **I hate writing in custom editors, got no time -**

  different blogging services like wordpress, blogger, tumblr etc.. *(I've tried and tired)* have their own custom editors, if you are a person hate writing in them, using text decorations, smilies, dragging stuff around, scaling images, playin around with custom HTML. Oh.. Its a bit hairy. It kills your time and focus. We've got a short life. **Being straight : I need a tool to write faster, and just to focus on whatever I type in**.
  
*  **I just need a pen & paper to write, not an engineering toolbox -** 

  "Hey, user, we've got some stuff for you to make your publishing look cool, which includes a music player, a TV, automatic cleaning robot, a sliding monkey, a popup message with latest offers, Ads, in depth analytics, prediction and so on.. and you could place your text somewhere below here.." *(just saying by pointing to the bottom right corner)*. **I need straight answers to my questions, don't let knowledge drawn in garbage**.
  
* **I don't have money to spent on hosting services, all I could do is write good, and I need easy control over it -**

  this is very important for me, and you may argue by saying, "blogging services got simple mechanisms to do this". I've used different free blogging platforms, and they all have their own content management systems. That's good. But, I don't need that much, that's the truth. All I needed is a minimal format, which is very near to the simple text. Think about an article, which is very lightweight and portable *(taking printouts, converting into pdf or epub, downloading for later references, RSS or similar reading)*, even the writer could stack them as backup in their own PC as very tiny files, or let others use it. **As a student, I've struggeled a lot to back great articles as a reference page**.
  
> These are the top three problems I face while writing and reading blogs, there are many other as well..
> ### I'm Just stopping here. You know the scenario, if you feel the same way.  
  
###Solution : How this blog works


*  **Each article I write is a markdown file -**

  a markdown file is very near to a simple text with some special characters determines basic text styling. an `.md` extension is given to these markdown files. **This is very useful for those who writes a lot and hate text selection rule to apply an action**. You apply rules as you type. More on the philosophy and Syntax can be accessed [right here from the maker](http://daringfireball.net/projects/markdown/syntax). Its **super fast**.
> ###Markdown is intended to be as easy-to-read and easy-to-write as is feasible - JOHN GRUBER 

*  **Who will convert this into a blog -**

	there are different methodologies for doing this, which range from javascript conversion to python based conversion libraries. For my blog, I've used [jekyll-now](http://www.jekyllnow.com). *(You will see later, why I've used this)*. Another library *(javascript based)*, in case of building a blog of your own is [markdown-js](https://github.com/evilstreak/markdown-js) or for django or flask websites, use [Markdown](https://pypi.python.org/pypi/Markdown).
	
	the main feature I like a lot in **jekyll** is, blog posts are distinguished and linked *(post URL, post title, posted date)* with their file name `YYYY-MM-DD-POST_TITLE.md`. A simple modification to their file name will change a lot, which makes life a lot easier. We make use of **front matter** to add specific attributes to each article.
	
*  **Where to host -**

	[Github](https://github.com) is a well known platform for version control for software projects. They allows the developers and organizations to host project website and blogs on another service called [Github pages](https://github.io). For me, I'm writing this blog in order to cover my software projects as well. So this is a perfect platform to write a blog as a developer.
