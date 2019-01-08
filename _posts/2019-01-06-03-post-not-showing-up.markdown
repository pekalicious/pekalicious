---
layout: post
title:  "Jekyll posts not showing up"
date:   2019-01-06 18:47:57 -0500
categories: jekyll
tags: [jekyll]
---
I was too lazy to constantly create new files and copy paste the same structure, so I wanted to duplicate existing files. Unfortunately, this is not functionality VS Code has, so I had to install [Duplicate Action](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-duplicate). Anyway, I duplicated a post, and noticed that the order isn't correct. Fair enough, edit the time by some amount and voila! The blog post disappeared!

<!--more-->

### What happened

New blog posts I duplicate are not showing up in the page.

### How I fixed it

Turns out, I always duplicated from the last post which had time set to the future. Like, *waaaaay* into the future. In hindsight, it makes sense. 

### How I found the solution

- A quick "jekyll posts not showing up" Google search brought me to [this question](https://stackoverflow.com/questions/30625044/jekyll-post-not-generated)
    - I simply went down the list and found out it was my time.
        - A possible solution is enabling future posts, but I decided not to go with that.
        > config future:true