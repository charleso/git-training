Git Training
============

Welcome.

Does this look familiar?

![xkcd](http://imgs.xkcd.com/comics/git.png)

Sadly it's not that far from the truth for many users of Git,
and doesn't always improve with more exposure.

One anology could be made with the following comic.

![](images/elephant.jpg?raw=)

In this case each blind man could represent a different Git command.
By just running the commands, there are a number of cases where
what you _think_ Git is doing is not actually what it's _actually_ doing.

In particular this often involves commands relating to branches,
and pushing/pulling from a remote server.

This material is _not_ intended to teach advanced Git
(eg. Run `git magic --hard --all` and you'll be more 100x more productive).
The focus of this material is to focus on a few critical
aspects of Git that can often cause the most amount of confusion.


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
2. [Commits](commit.md)
3. [Master](master.md)
4. [Branches](branches.md)
5. [Reflog](reflog.md)
6. [Remotes](remotes.md)
7. [Push](push.md)

### Advanced

- [Reset](reset.md)
- [Index](index.md)


References
----------

- http://www.infoq.com/presentations/A-Tale-of-Three-Trees
- https://git-scm.com/book
- http://www-cs-students.stanford.edu/~blynn/gitmagic/
- http://eagain.net/articles/git-for-computer-scientists/
