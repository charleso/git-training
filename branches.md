Git - Branches
==============

This guide is intended as a primer for understanding
how Git branches work. You should have previously
read [about the master branch](master.md).


Branch
------

Previously we saw that Git has a concept called `HEAD`
that references `refs/heads/master`, which we know
as just `master`.

```
> git log --graph --oneline --decorate 41ce7fa

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```

Let's introduce a new command `branch`.

```sh
> git branch

* master
```

Branch can also be used for creating a new branch at a specific commit.

```sh
> git branch hello 672e562
```

What does our graph look like now?

```sh
> git log --graph --oneline --decorate 41ce7fa

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

And if we look in `refs/heads`?

```sh
> ls -F .git/refs/heads

hello
master

> cat .git/refs/heads/hello

672e562c008009ec391e11a1fa3574af39428ae1
```

So creating a branch is just creating a single file?


### Question

> What happens if you create a `refs/heads` file manually?

> What happens if you change the hash of `refs/heads/hello` to another commit?

> What happens if you create other types of `refs/` (eg. `refs/test`)?


Checkout
--------

So far all we've done is create new branches to reference commits
we've already created. That doesn't seem all that useful.

In addition, we haven't talked about looking at the "contents" of a
previous commit. Sure, we've run `log` and can see them, but
how can we go back to a previous commit and look at the files?

```sh
> git checkout hello

Switched to branch 'hello'
```

What did that do?

```sh
> cat file.txt

hello
hello again
```

Where did my "goodbye" go?

What else did it change?

```sh
> git branch

* hello
  master

> cat .git/HEAD

ref: refs/heads/hello
```

So it changed the current branch, which is stored in the `HEAD` file.


### Question

> Try checkout out `master`, does the missing line appear again?

> Try changing the `HEAD` file manually.
> Does that change the `branch` and `log --graph` ouput as you expect?
> Does it change the `file.txt` though?

> Try making a new commit on `hello`, what does the graph look like now?

> How would you swap two branches around?



Next
----

This is really the bare essentials.
Understanding how and what branches are is the essence of understanding
Git.

There are two options at this point:

- Looking at how the [scary reset command](reset.md) works
- Skipping ahead to [remotes](remotes.md)
