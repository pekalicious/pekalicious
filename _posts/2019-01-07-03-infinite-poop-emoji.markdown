---
layout: post
title:  "The case of the infinite poop emoji crawler trap"
date:   2019-01-07 22:00:00 -0500
categories: mcc-workflow
tags: [ruby,http]
---
## What happened
My worker on Heroku was getting stuck trying to get a response from a URL. Turns out the website was a trap and would infinitely print out poop emojis. Touche [RobePike](http://robpike.io), touche.

<!--more-->

## How I fixed it
Using the built-in timeout argument in `Net::HTTP.read_timeout` wasn't doing the trick because the website *request* wasn't actually timing out. The page would simply take forever. 

I ended up simply wrapping my `get_response` method in a Ruby `Timeout` block.

## How I found the solution

Was having trouble with getting the final redirect of a URL
- Found out that the `get_response` part never ended or timed out
  - Opened the URL in the browser to see what was happening. Turns out, the page constantly prints the poop emoji causing the crawler to never complete. Genius.
    - Found [this blog post](https://opensourceconnections.com/blog/2008/04/24/adding-timeout-to-nethttp-get_response/) showing how to set a get timeout
      - Only problem is, it doesn't actually time out. The page just deliberately renders indefinitely.
        - Used Timeout::(5) instead but it immediately throws an exception of "end of file reached"
          - Looks like redirects to HTTPS need to have `http.use_ssl = (uri.scheme == "https")` [Source](https://stackoverflow.com/questions/5244887/eoferror-end-of-file-reached-issue-with-nethttp)
            - Timeout worked!