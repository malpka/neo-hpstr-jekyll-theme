---
layout: post
title: "Git force merge strategy for specific file"
date: 2014-06-16 07:47:59 +0200
comments: true
categories: git
---

In order to set a default strategy for a file(s) in git merge you need to:

### Enable the `ours` merge driver

- for current repository

``` bash
git config merge.ours.driver true
```

- globally 

``` bash
git config --global merge.ours.driver true
```
 
### Tell git to use the merge strategy for a file

``` bash
echo "solutionfolder/file.xml merge=ours" >> .git/info/attributes
```

As a result the next pull with conflicts will automagically use ours version.

Just remember that the file will not longer be marked as merge conflict.

[inspiration](http://stackoverflow.com/questions/14093540/tell-git-to-use-ours-merge-strategy-on-specific-files)
