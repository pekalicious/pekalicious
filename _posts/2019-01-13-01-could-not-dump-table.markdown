---
layout: post
title:  "Could not dump table 'users' because of following StandardError Unknown type 'user_role' for column 'role'"
date:   2019-01-13 22:00:00 -0500
categories: mcc-workflow
tags: [ruby,rails,databases]
---

One of my tables in `schema.rb` wasn't being dumped at all. At first I thought it had to do with a migration I reverted without applying it, but turns out it was because of a PostgreSQL `enum` column.

<!--more-->

## What happened
I added a new column to store a user's role in the app. For some reason I decided to go with PostgreSQL `enum`. I created a custom type with my values, updated the model and migrated. I opened `schema.rb` and noticed this error:

> \# Could not dump table "users" because of following StandardError \#   Unknown type 'user_role' for column 'role'

## How I fixed it
Turns out, `enum` isn't something ActiveRecord can map correctly, so I had to switch to dumping the schema in `sql` format. Pretty simple: update `config/application.rb` with the following line:

    config.active_record.schema_format = :sql

Oh, and before I forget: [here's an immensly useful post with all rake db commands and what they do](https://jacopretorius.net/2014/02/all-rails-db-rake-tasks-and-what-they-do.html).

## How I found the solution

Got error:
> \# Could not dump table "users" because of following StandardError
> \#   Unknown type 'user_role' for column 'role'

- It's because I'm using PostgreSQL with `enum` types that are not supported by Rails
  - Need to switch to using `:sql` for formatting [as per this answer](https://stackoverflow.com/a/51479789)
    - Migrating to dump causes error: 
    > pg_dump -s -x -O -f pg_dump [...] is installed in your PATH and has proper permissions.
      - Added 'postgres/bin' to path and it worked