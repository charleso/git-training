Git - Commits
=============

This guide is intended as a primer for understanding
how Git commits work.


Create a commit
---------------

This is something you're going to do.
[A lot](http://hyperboleandahalf.blogspot.com.au/2010/04/alot-is-better-than-you-at-everything.html).

```sh
# Create a file with some text, the value doesn't matter
> echo "hello" >> file.txt

# Add the new file to git
> git add .

> git commit -m "Initial commit"

[master (root-commit) 406bb3b] Initial commit
 1 file changed, 1 insertion(+)
  create mode 100644 file.txt
```

Already from running this one command we can see two very important
bits of information.

- The "branch", which is indicated by `master`.
  By default `master` is the first/initial branch that is created,
  but after that there's _nothing_ special about it.
  We'll get to [master soon](master.md)
- A hash, which is indicated as `406bb3b` in this example.
  When you run this on your machine it _will_ be something different.

This section is only interested in commits, we'll have plenty of time
to talk [about branches](branch.md).


Commit
------

So what just happened?

Imagine taking a copy/backup of a file or directory of files.
A very common approach will be to take a copy and rename the new
version to something like "test-1".

That's basically what we just did. Think of a commit as
that directory of files, preserved forever, but without it
necessarily cluttering up your desktop.

Let's do it again, just for fun.

```sh
# Update the file
> echo "hello again" >> file.txt

# Add the new contents
> git add .

> git commit -m "Second commit"

[master 672e562] Second commit
 1 file changed, 1 insertion(+)
```

### Question

> What happens if you try commiting without changing the file?

Again we see `master`, and now a different hash `672e562`.
Maybe we should stop to talk about what a hash is.


Hash
----

You will probably see the hash referred to by a number of names
in various places, both here and elsewhere. Such as:

- sha1
- sha
- hash
- commit ID

They're all the same thing I promise.
But what the hell is that exactly?!?

The hash is a unique address/reference/pointer to that commit.
In the example of taking copies of a file/directory the hash
could be thought of the filename.
Such as "test-1", "test-2", etc.

After a while those filenames would all blur together,
how would we know what each one contained?
The commit hash is very big and is guaranteed to be unique,
so you don't have to keep coming up with new names.
If you're wondering why the hash isn't just a number,
that's a little harder to explain (and I'm not going to try).


Log
---

Let's take a look at those two commits. How do we do that?

```sh
> git log 672e562

commit 672e562c008009ec391e11a1fa3574af39428ae1
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 10:56:55 2016 +1000

    Second commit

commit 406bb3bffbd02113ad5e2fecb4da364c01b20bb3
Author: Charles O'Farrell <charleso@charleso.org>
Date:   Sun Apr 17 10:35:29 2016 +1000

    Initial commit
```


The first thing to note is that `672e562` is only
the first 7 characters of a must longer hash
`672e562c008009ec391e11a1fa3574af39428ae1`.

### Question

> What other forms of the hash does Git accept?
> Can it be shorter? Longer?

> What happens when you use log to view the first commit?
> What was missing?

Secondly you can see the commit "message" that we supplied
to the `commit -m` command. That's handy, we can
see more information about that commit.
That's better than having `really-long-filename-3` to indicate
what a particular backup was for.

We can also see who created that commit, which isn't all
that interesting when we're working by ourselves, but
in larger projects that might be very important.
Who broke the program - oh it was Charles!!!

### Question

> Create a few more commits and then look at them with log


Next
----

[Next up](head.md) we're going to look at what `master` is.
