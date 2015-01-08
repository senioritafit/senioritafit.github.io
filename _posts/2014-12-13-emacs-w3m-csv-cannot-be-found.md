---
layout: note
title: emacs-w3m; 'csv' cannot be found
date: 2014-12-13
updated: 2014-12-13
categories: emacs osx w3m emacs-w3m el-get
---

Ran into an issue installing `emacs-w3m` through el-get. I installed `w3m` through brew, but got this when starting emacs:

```
the command named 'cvs' cannot be found with executable-find'
```

Make sure to have `cvs` on your system as well.

```
brew install cvs
```
