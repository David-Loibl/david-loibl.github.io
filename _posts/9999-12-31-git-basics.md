---
title: 'Getting started with Git'
date: 9999-12-31
permalink: /posts/todo/getting-started-with-git/
tags:
  - git
  - tutorial
  - programming
---

# Getting started with Git

### Cache username and password
When actively working on a project, the recurring prompt to enter username and password can become seriously annoying. The following command will make Git cache your credentials for two hours in the future.
```console
git config --global credential.helper "cache --timeout=7200"
```