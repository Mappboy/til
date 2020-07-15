---
categories:
- Netlify
- Problems
date: "15-07-2020"
tags:
- netlify
- programming
title: Setting node environment variables
---
This TIL could be called why my Netlify build didn't work.
Check here for more details but in short this was my problem
https://docs.netlify.com/configure-builds/manage-dependencies/#dependency-cache

Because I didn't set both of these Netlify was trying to build Gatsby with an out of date node and also installing packages I didn't want installing.

Set these environment variables and you will be sorted.
```
NODE_VERSION 14
NODE_ENV production
```