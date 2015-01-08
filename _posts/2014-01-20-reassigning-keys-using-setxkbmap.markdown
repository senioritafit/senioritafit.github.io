---
layout: note
title: Reassigning keys using setxkbmap
date: 2014-01-20
updated: 2014-04-21
categories: xmodmap linux setxkbmap
---

## Example: Reassigning Caps lock

### To Backspace

```bash
setxkbmap -option caps:backspace
xmodmap -e 'clear Lock'
```

Note: Running `xmodmap -e 'clear Lock'` fixes issues with Caps lock remaining active after running `setxkbmap`.

## Reassigning any other key?

View a list of options such as `caps:backspace` in:

```bash
less /usr/share/X11/xkb/rules/base.lst
```

or wherever `man setxkbmap` tells you where the source for all the components are. Once the listing is open, scroll down to the `! option` section for a complete listing of supported actions.
