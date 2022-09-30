---
title: removing committed files from repo
date: 17/12/21
tags: git
---

# **removing committed files from repo** 202112170226 
> **58b365**

To remove an erroneously added file in a git repo, the file can be removed by simply following the next bash commands  
```sh
git rm --cache 'file.txt'
git commit -m "removing file"
```
  

