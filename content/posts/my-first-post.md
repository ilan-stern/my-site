+++
date = '2025-02-14T18:19:31+11:00'
draft = true
title = 'Building this site'
+++
I decided to make a blog to track my progress and interests in Cyber Security. 

In this post I will be describing the methods I use.

I’ve decided to use ‘Hugo’ -  a static site generator for this task.

Steps:

I started with installing Hugo via CLI using the command: *brew install hugo*

To quickly spin up a test site, I ran the following set of commands:

> *hugo new site quickstart*

> *cd quickstart*

> *git init*

> *git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke*

> *echo “theme = ‘ananke’” >> hugo.toml*

> *hugo server*

Through these commands I was able to visit my site through the provided link in the output of the last command.

After this, I made my first post here (this page).

I did this through adding a new page to the **posts** directory.

> *hugo new content content/posts/my-first-post.md*

After simply adding this text and running the command: 

> *hugo server -D*

I was able to see my first post!
