---
layout: post
title: 'TIL: Repeat last command with sudo'
---
Repeating commands that require sudo is required quite often while working on the command line. Here's 3 ways to repeat the command with sudo prepended.

1. The naive approach: Going back in history, than using the left arrow to go back to the beginning of the line, and typing sudo again. I did this for years, until I found the following trick.
2. Using Ctrl+A to get to the beginning of the line. After that you can type sudo, as explained in 1. This is much better already, especially for longer commands. Ctrl+A is an Emacs macro, and since your shell is probably configured to use Emacs keys, it'll work. If you changed that to vi, I expect you know what you're doing ;)
3. `sudo !!` .`!!` stores your last command line and is enabled via history expansion. 
