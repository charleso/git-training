Git - Branches
==============

This guide is intented as a primer for understanding
what `master` is. You should have previously
read [about commits](commit.md).


Master
------

So far we've create a few commits. Let create another.

```sh
> echo "goodbye" >> file.txt

# Add the new contents
> git add .

> git commit -m "Third commit"

[master 41ce7fa] Third commit
 1 file changed, 1 insertion(+)
```

So what is this `master` exactly?
A branch obviously, but what is that _really_?

Let's take a detour.


Graph
-----

Git has a very "rich" (read: confusing as hell) command line.
In general I want to avoid throwing around 10 different versions
of a command, that is probably going to be confusing at this stage.
`log` alone has about 30 options, many of which can be very useful.
The ones I want to show now look like this:

```
> git log --graph --oneline --decorate 41ce7fa

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```

### Question

> What does each of those options do?
> Can you use different combinations of them?

So this contains one extra bit of Git terminology we haven't seen before. `HEAD`.


HEAD
----

Understanding `HEAD` is critical to understanding how Git _really_ works,
so let's take a second to dig a little deeper.

Way back in the beginning we looked at the contents of the `.git` directory.
Let's do that again:

```sh
> ls -F .git

COMMIT_EDITMSG
HEAD
branches/
config
description
hooks/
index
info/
logs/
objects/
refs/
```

Interesting, there's a file called `HEAD`. Let's take a look.

```sh
# The `cat` command prints the contents of a file on the terminal
> cat .git/HEAD

ref: refs/heads/master
```

So we should recognise the `master` part, but what is `refs/heads/`?

Let's keep digging.


Refs
----

You'll also notice there is a `refs/` directory in `.git`.

```sh
> ls -F .git/refs

heads/
tags/
```

Ignore `tags`, let's focus on `heads`.

```sh
> ls -F .git/refs/heads

master
```

And at the end of the rabbit hole?

```sh
> cat .git/refs/heads/master

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
```

That's the most recent commit!
So `HEAD` is just a reference to `refs/heads/master`,
which in turn is just a pointer to a commit.

Something like this:

```
HEAD -> master -> 41ce7fa
```

Actually that looks a _little_ like our `log --graph` command.

```
> git log --graph --oneline --decorate 41ce7fa

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```


### Question

> Can you use `HEAD`, `master` or even `refs/heads/master` in the `log` command?


Next
----

Ok, that's probably enough for this guide.
Next we'll see what happens when we start creating
[multiple branches](branches.md).
