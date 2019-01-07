---
layout: post
title:  "Personal github pages"
date:   2019-01-06 18:47:57 -0500
categories: jekyll
---
A lot of tutorials on setting up Jekyll for GitHub Pages recommend pushing to a orphaned `gh-pages` branch. That's OK if you want to create a page for a specific project under `<username>.github.io/<project>` but not if you want to setup a personal `<username>.github.io` page.

### What happened

I set up a repo with the same name as my username after reading the error page when visiting `<username>.github.io` and after setting up Jekyll and pushing to `gh-pages` branch, the URL wasn't what I wanted.

### How I fixed it

You need to make sure the repository name follows the convention `<username>.github.io`. Also note that you *must* push to `master` and not `gh-pages` for this type of repo.

### How I found the solution

- My first attempt at pushing a personal blog on GitHub didn't give me the correct URL path. I ended up with `<username>.github.io/<username>`
    - After googling around, I found out what I need is called a **User Page**. [This GitHub Help Page](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/) showed me the way:
        > If your site is a User or Organization Page that has a repository named <username>.github.io or <orgname>.github.io , you cannot publish your site's source files from different locations. User and Organization Pages that have this type of repository name are only published from the master branch.