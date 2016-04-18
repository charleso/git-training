Git - Reflog
============

You should have previously read [about branches](branches.md).

[Let's. Get. Dangerous.](https://www.youtube.com/watch?v=375ENQbru8s)


Lost
----

At one point the graph looked something like this.

```sh
> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

The `HEAD` is referencing `master`, which is at a different commit
to `hello`.

Let's checkout `hello`.

```sh
> git checkout hello

> git log --graph --oneline --decorate master

* 41ce7fa (master) Third commit
* 672e562 (HEAD, hello) Second commit
* 406bb3b Initial commit
```

And now for something a little crazy.

```sh
# Delete the master branch - weeeeeeee
> rm .git/refs/heads/master

> git log --graph --oneline --decorate hello

* 672e562 (HEAD, hello) Second commit
* 406bb3b Initial commit
```

Oh no, where did it go?
How do we get it back?!?

### Warning

In many cases Git will actually try to prevent this ever happening.
There are checks and warnings on the relevant Git commands that will
stop you shooting yourself in the foot.

This goes without saying but it is _always_ recommended to use Git
commands rather than modifying the contents of the `.git` directory.


> We manually deleted the `master` branch by deleting a file,
> can you work out how you would "normally" delete a branch?


Found
-----

It's hard to imagine that just by deleting the ref file that we
_actually_ deleted the commit itself. The commit message
has to be stored separately at least.

Does the commit still exist? Let's check by using the commit hash...

```sh
> git log --graph --oneline --decorate 41ce7fa

* 41ce7fa Third commit
* 672e562 (HEAD, hello) Second commit
* 406bb3b Initial commit
```

Phew! So it's still there. But what happens if we didn't know,
or forgot the hash?

Ladies and gentlemen, I give to you to...


Reflog
------

```sh
> git reflog HEAD

672e562 HEAD@{0}: checkout: moving from master to hello
41ce7fa HEAD@{1}: commit: Third commit
672e562 HEAD@{2}: commit: Second commit
406bb3b HEAD@{3}: commit (initial): Initial commit
```

Whenever you run `commit` or `checkout` commands, Git logs the
the old and new commits.
So for _every_ change to your `HEAD` (and refs) Git actually tracks
what happened. The _ref_log.

A (very bad) anology is a bank keeping a transaction log of changes
to your account. Or at least you hope they do!

My advice - don't leave home without `git reflog`.


> Can you re-create the `master` branch on that commit?

> Do you think the log keeps growing forever?
> If you're interested read more at `git reflog --help` and `git gc --help`.


If you're interested in how that looks in `.git`:

```sh
> cat .git/logs/HEAD

0000000000000000000000000000000000000000 406bb3bffbd02113ad5e2fecb4da364c01b20bb3 Charles O'Farrell <charleso@charleso.org> 1460853329 +1000   commit (initial): Initial commit
406bb3bffbd02113ad5e2fecb4da364c01b20bb3 672e562c008009ec391e11a1fa3574af39428ae1 Charles O'Farrell <charleso@charleso.org> 1460854615 +1000   commit: Second commit
672e562c008009ec391e11a1fa3574af39428ae1 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3 Charles O'Farrell <charleso@charleso.org> 1460856405 +1000   commit: Third commit
41ce7faa5b8b2cf480d44c3b12f0545fed9683c3 672e562c008009ec391e11a1fa3574af39428ae1 Charles O'Farrell <charleso@charleso.org> 1460859487 +1000   checkout: moving from master to hello
```


Next
----

There are two options at this point:

- If you haven't already, go read about the [scary reset command](reset.md)
- Learn about [remotes](remotes.md)
