Git Training
============

Does this look familiar?

![xkcd](http://imgs.xkcd.com/comics/git.png)

Sadly it's not that far from the truth for many users of Git,
and doesn't always improve with more exposure.

One analogy could be made with the following comic.

![](images/elephant.jpg?raw=)

In this case each blind man could represent a different Git command.
By just running the commands, there are a number of cases where
what you _think_ Git is doing is not what it's _actually_ doing.

In particular this often involves commands relating to branches,
and pushing/pulling from a remote server.

This material is _not_ intended to teach advanced Git
(eg. run `git magic --hard --all` and you'll be more 100x more productive).
The aim is to focus on a few critical aspects of Git that can often cause
the most amount of confusion.


Prerequisites
-------------

Everything in this guide assumes some form of terminal/command-line with `git` installed.

For Windows this means [Git for Windows](https://git-scm.com/download/win),
ideally in the `msysgit` terminal and not Windows `Cmd`.
If you're not sure try running `ls`, `cd` or `cat README.md`, the
examples make some use of these commands.

No GUIs.


Sections
--------

1. [Getting started](init.md)

### Core

2. [Commits](commit.md)
3. [Master and HEAD](head.md)
4. [Branches](branches.md)

### Intermediate

5. [Remotes](remotes.md)
6. [Pull](pull.md)
7. [Push](push.md)

### Advanced

- [Reflog](reflog.md)
- [Reset](reset.md)
- [Index](index.md)

Help
----

- [Git commands](git_cheatsheet.md)
- [Shell commands](shell-cheatsheet.md)


References
----------

- http://www.infoq.com/presentations/A-Tale-of-Three-Trees
- https://git-scm.com/book
- http://www-cs-students.stanford.edu/~blynn/gitmagic/
- http://eagain.net/articles/git-for-computer-scientists/
- https://dev.to/unseenwizzard/learn-git-concepts-not-commands-4gjc
