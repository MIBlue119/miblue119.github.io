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
- Set the repo's past commit with new user&email
``` bash
$ git filter-branch -f --env-filter "GIT_AUTHOR_NAME='MIBlue119'; GIT_AUTHOR_EMAIL='miblue119@gmail.com'; GIT_COMMITTER_NAME='MIBlue119'; GIT_COMMITTER_EMAIL='miblue119@gmail.com';" HEAD
```
  - Ref: 
    - [How to revise the author/email of past commit ?](https://stackoverflow.com/questions/750172/how-to-change-the-author-and-committer-name-and-e-mail-of-multiple-commits-in-gi)

- Push the repo with other account's github
``` bash
$ git push https://user_name:accesstoken@github.com/repos.git
```