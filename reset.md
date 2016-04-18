Git - Reset
===========

You should have previously read [about branches](branches.md).

**NOTE** `reset` is really an advanced command,
and for many users it's not something they need (or should) be
running.
That said, it's a fairly powerful and useful command in
the hands of someone who understands the risks.


Checkout
--------

Let's reorientate ourselves.

```sh
> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```

Right, so currently `HEAD` is pointing to `master`.

```sh
> cat .git/HEAD

ref: refs/heads/master

> cat .git/refs/heads/master

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
```

Previously we saw that `checkout` changes the contents of the `HEAD` file
(and updates files in the working directory, but that's less important).


Reset
-----

Imagine that you want to "undo" a commit on your current branch.
Why, might you ask? There might be a number of reasons.

- You've just added a commit with a spelling mistake
- You've added a file by mistake


Given what we (now) know about Git, there _is_ something dodgy we
could do - update the `master` ref with the previous commit.

```sh
echo "672e562c008009ec391e11a1fa3574af39428ae1" > .git/refs/heads/master

> git log --graph --oneline --decorate master

* 672e562 (HEAD, master) Second commit
* 406bb3b Initial commit
```

And that's _exactly_ what `reset` does.
Let's go back to where we were.

```sh
> git reset 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
Unstaged changes after reset:
M       file.txt

> cat .git/refs/heads/master
41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
```

However, Git has told us something interesting after running `reset`.
Something about our files being "unstaged".

It's important to note that by default `reset` _doesn't_ modify any
of your working files, only the ref. This isn't any different than if
we had tweaked the ref file manually.


> What do you expect `file.txt` to contain?


Hard
----

So how do we update the files at the same time?

```sh
> git reset --hard 672e562c008009ec391e11a1fa3574af39428ae1
HEAD is now at 672e562 Second commit
```

**WARNING** `reset --hard` can be very dangerous, it updates
files on disk _without prompting_.
If you have unsaved/uncommitted changes Git will quite happily undo
those changes without so much as a "Do you wish to continue (y/n)".


Next
----

Check out the section on [reflog](reflog.md) to know what happens
to commits that you undo.
