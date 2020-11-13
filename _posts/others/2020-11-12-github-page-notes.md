---
layout: post
mathjax: true
title: "Github Page - Some notes!"
read: 5
secondary: others
date: 2020-11-12
---
*This post was written as my thank to* [Chris Emmery](https://cmry.github.io/).

I happened to read his blog and I also wanted to build a similar page as his one to write down what I learned. So, I emailed him and he provided me the tutorial to follow. Because I am very new to front-end, I also learned the way he structured on github.

During the process of building Github Page, here are some things that you might want to know.

## 1. Write markdown files

I use [Markdown All in one](https://www.programmersought.com/article/94051435573/) extension to write markdown files and Math equations. Also, I use Image paste extension for embeding images in markdown files. Finally,I integrate Github on Visual Studio code to git pull, git add, git commit and git push posts. 

## 2. Display images on Github page

I have to store images in a separate folder (sources) and link it to posts in another folder (_posts)

> ![](/sources/Others-github-page-notes.png)

It will not work if putting images and posts at the same folder.

## 3. Run multiple blogs on Github page

I followed this instruction and it works: [Multiple Blogs](https://stochastic.life/2016/01/06/multiple-blogs-on-single-jekyll-instance/)

## 4. Write Math equation 

I use Markdown-in-all extension on visual studio code and followed this document to write Math equation [Katex](https://katex.org/docs/supported.html)

## 5. Display on Github page

After you write Math equations, it will still not display on Github Page until you enable "MathJax". 

Follow this instruction, it might work for you: [MathJax](http://sgeos.github.io/github/jekyll/2016/08/21/adding_mathjax_to_a_jekyll_github_pages_blog.html)

You can check my post to see how Math equations were displayed: [Decision Tree](https://lytranp.github.io/notes/Decision-Tree)





