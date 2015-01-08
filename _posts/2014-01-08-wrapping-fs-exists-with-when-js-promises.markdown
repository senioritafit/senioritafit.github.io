---
layout: post
title: Wrapping fs.exists with when.js promises
date: 2014-01-08
categories: code javascript promise
---

[This post](http://www.hiddentao.com/archives/2013/06/10/how-to-wrap-fs-exists-within-a-promise/) covers how to wrap [`fs.exists`](http://nodejs.org/api/fs.html#fs_fs_exists_path_callback) using the [Q promise library](https://github.com/kriskowal/q).

We can use the exact same syntax with [when.js promises](https://github.com/cujojs/when):

```javascript
var when = require('when');

var existsDefer = when.defer();
fs.exists('/path/file.json', existsDefer.resolve);
existsDefer.promise.then(function(exists) {
	if (exists) { /* ... */ }
});
```
When.js also offers a [callbacks module](https://github.com/cujojs/when/blob/master/callbacks.js) that can help reduce the code further:

```javascript
var callbacks = require('when/callbacks');

callbacks.call(fs.exists, '/path/file.json').then(function(exists) {
    if (exists) { /* ... */ }
});
```
