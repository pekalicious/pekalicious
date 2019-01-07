---
layout: post
title:  "Could not find gem 'wdm (>= 0.1.0) x86-mingw32' in any of the gem sources listed in your Gemfile"
date:   2019-01-06 18:46:57 -0500
categories: jekyll
---
I guess it's only natural to start this blog with issues setting the blog itself up.

## What happened

Followed [this post](https://www.taniarascia.com/make-a-static-website-with-jekyll/) on how to setup a Jekyll blog. When I got to the point to run the command to serve

    jekyll serve

I get the error

    Could not find gem 'wdm (>= 0.1.0) x86-mingw32' in any of the gem sources listed in your Gemfile

## How I fixed it

According to the RubyInstaller for Windows, certain binary files are no longer included, so you need to install them using gem

    gem install --platform x64-mingw32 wdm

## How I found the solution

- [This question](https://stackoverflow.com/questions/42425061/could-not-find-gem-wdm-0-1-0-x86-mingw32-in-any-of-the-gem-sources-listed?rq=1) on StackOverflow mentioned installing the Ruby DevKit.
    - The [DevKit page for Windows](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit) says:
    >Starting with RubyInstaller-2.4 we use MSYS2 as our Development Kit. See also the RubyInstaller-2.4 announcement .
        - So I go to the [Installer page](https://rubyinstaller.org/2017/05/25/rubyinstaller-2.4.1-1-released.html) which says:
        > Please note, that many fat binary gems are not yet prepared for RubyInstaller-2.4. Try to use
        > gem install --platform ruby <gemname>