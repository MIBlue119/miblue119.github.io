---
title: Activate pylint at VS code
description: A note about activate pylint at vscode 
date: 2021-12-23
tags:
  - posts
layout: layouts/post.njk
---

# Activate pylint at VS code

## What is `Linting`?
- Is a static code analysis tool to flag programming errors, bugs, stylitic errors and suspicious constructs.
- We coud use it to increase the quality of our codes.

## Lint tools
- Python
    - [Pylint](https://pylint.org/), [flake8](https://flake8.pycqa.org/en/latest/),[Pydocstyle](http://www.pydocstyle.org/en/stable/)
- Javascript
    - [ESLint](https://eslint.org/)

## How to activate liniting at vscode?
- Open `Python:Select linter` 
    1. At Mac, Press `cmd+shift+p` 
    2. Input `Python:Select linter` 
    3. Select part of lint 

- [How to open multiple lint in viscode?](https://stackoverflow.com/questions/67229088/how-to-enable-linter-pylint-enable-in-vs-code-when-python-select-linterpylint)
    1. At Mac, Press `cmd+ ,` 
    2. Input `pylint enabled` 
    3. Check which pylint you want to enabled 

- [Python Linting in VScode](https://code.visualstudio.com/docs/python/linting)
    - You could also new a local setting for vscode
        1. Construct a folder `.vscode`
        2. New a `setting.json`
        3. Paste these setting 
        ```
            {
            "python.linting.flake8Enabled": true,
            "python.linting.enabled": true,
            "python.linting.pydocstyleEnabled": true
            }
        ```