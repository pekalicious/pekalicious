---
layout: post
title:  "Rugged::OSError (failed to resolve path)"
date:   2019-01-07 00:15:57 -0500
categories: exercism
tags: [exercism,rugged,ruby,windows]
---
My local copy of exercism didn't render certain static pages. After a while it turns out, it's because of Windows.

<!--more-->

## What happened

Visiting the FAQs page would produce the error:

> Rugged::OSError (failed to resolve path 'file://<...>website-copy': The filename, directory name, or volume label syntax is incorrect.
):


At this point I'm starting to realize that developing on Windows is... less convenient. I'm this close to switching to Mac, but my dislike of MacOS is still stronger than the inconvenience of using Windows as a Dev env. As for Linux, I'll wait for the year of the Linux desktop.

## How I fixed it

Turns out, I just needed to remove the `file://` part of the string. :(

## How I found the solution

- Forked and cloned the `website-copy` repo locally exactly where Rails expects it. Didn't work.
 - Hard coded the path in source file. Didn't work. Maybe a permissions issue?
  - Started looking into what's trying to perform the cloning. Apparently Rugged is a Git Ruby library for libgit2. Maybe it isn't installed correctly with native extensions? Installing now.
   - Nope. Didn't work.
   - Noticed another error just above this "Not notifying due to an invalid api_key". Investigating...
    - Looks like it's coming from bugsnag
     - It's a tool to analize your codebase. Probably not relevant.
   - Let's use the production version of this code...
    - Interesting. This worked...
   - Maybe the path is not Windows friendly?
   - AHA! It expects a `bare` repo! Kinda makes sense. Found this on the [docs](https://www.rubydoc.info/github/libgit2/rugged/Rugged/Repository#clone_at-class_method)
    - How do you clone a bare repo locally???
     - `git clone --bare <repo>`
    - Nope. Did not work... Turns out, it *creates* a bare repo as oppose to clone *from* a bare repo. I need to learn to *read* documentation.
 - Erm... It turns out, the prefix `file://` was the problem. Oh Windows...