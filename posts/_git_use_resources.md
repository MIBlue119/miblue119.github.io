---
title: Git Github use resources
description: A resources collection of Git/Gihub
date: 2021-11-26
tags:
  - posts
layout: layouts/post.njk
---

# Git Github use resources



- Check current repo's user info 
``` bash
$ git config user.name
$ git config user.email
```
- Set the current repo's user info with new info 
``` bash
$ git config user.name "NEW_NAME"
$ git config user.email "NEW_EMAIL"
```

- Push the repo with other account's github
``` bash
$ git push https://user_name:accesstoken@github.com/repos.git
```