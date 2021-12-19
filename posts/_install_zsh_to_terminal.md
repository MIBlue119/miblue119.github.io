---
title: Ohmyzsh Command Line Highlight Tool
description: This is a post to record a tool for terminal
date: 2021-12-19
tags:
  - tool
layout: layouts/post.njk
---

## Ohmyzsh is a commandline highlight tool
https://github.com/ohmyzsh/ohmyzsh

### Install at Ubuntu

1. Install zsh first
    ```
    $ apt-get install zsg 
    ```
2. Clone `Ohmyzsh` 
    ```
    $ git clone https://github.com/ohmyzsh/ohmyzsh.git
    ```
3. Install `Ohmyzsh`
    ```
    $ cd /ohmyzsh/master/tools/
    $ ./install.sh
    ```
4. Change the setting
    ```
    $ nano ~/.zshrc
    ZSH_THEME="agnoster"
    ```
    - Resolve the encode error
        -  Mac
            - https://nicksheng.github.io/2017/06/30/mac-zsh/
            - https://github.com/ccyongzhi/the-Learned/issues/33
        - Ubuntu
            - https://blog.csdn.net/CoderMannul/article/details/90https://blog.csdn.net/CoderMannul/article/details/90724645724645

5. Let the zsh opened when terminal is opened
    a. Add the `zsh` to bash
        ```
        $ sudo vim ~/.bashrc
        ```
    b. Add this line
        ```
        exec zsh
        ```
