---
title: "How to find files on Linux"
subtitle: "Linux Foundations"
date: 2023-01-03T17:38:39+01:00
tags: ['linux', 'cli']
draft: true
---
While learning how to use the Linux Command Line, you will inevitable stumble upon the question on how to find files. I usually struggle to remember how to use those commands effectively. So with the post here I wanted to reiterate and note down a short manual with examples for later use.

<!--more-->

There are usually two commands you will learn to use in the command line.

## locate

***Locate*** uses a previously generated database and does not search your entire filesystem. This also makes it really fast compared to other search commands like **find**. However, it also means that files deleted after the database has been updated still show up in the search. Also files which were created after the last update won't be included. For the first shortcoming there is a simple solution by using the **-e** option, e.g. `$ locate -e mysql`. 

The command simply outputs any matching file as a list in the command line. For better readability you can also pipe the output into **less**:

`$ locate mysql | less`

The database used by **locate** is managed by a related utilty tool called **updatedb**. Most Linux systems run this tool automatically once a day. If you would like the database to be updated, you can also start it manually by running `$ sudo updatedb` from the command line.

Also have a look at the **man** page for locate if you'd like to learn even more about it.

## find

### exec

## Wildcards
