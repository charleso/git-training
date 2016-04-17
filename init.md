Git - Getting Started
=====================

```sh
> mkdir test
> cd test
> git init

Initialized empty Git repository in test/.git/
```

At this point you may notice a new, hidden directory created
in the current folder. Let's take a look.

```sh
> ls -F .git

HEAD
branches/
config
description
hooks/
info/
objects/
refs/
```

Hopefully by the end of this guide some of those files
won't seem so cryptic, and you will know what they mean.
