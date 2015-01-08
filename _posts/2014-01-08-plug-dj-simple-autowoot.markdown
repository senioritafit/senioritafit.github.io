---
layout: note
title: Plug.dj Simple Autowoot
date: 2014-01-08
categories: javascript snippet
---

Run this snippet in the console once you're in a room. It will auto woot every 20 seconds, and respect any "meh" votes given.

```javascript

(function() {
    var $ = document.getElementById.bind(document);
    setInterval(function() {
        if($('meh').className.indexOf('selected') === -1) {
            $('woot').click();
        }
    }, 20000);
})();
```
