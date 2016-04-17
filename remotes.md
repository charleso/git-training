Git - Remotes
=============

You should read about [branches](branches.md) before starting this section.

So way back in the beginning we ran `git init` to create a
new repository.
However, as is often the case you're actually very likely
to want to get a copy of an existing repository.


Clone
-----

If you've ever used Git before it's quite possible you've run something like this.

```sh
> git clone https://github.com/charleso/git-training.git

Cloning into 'git-training'...
remote: Counting objects: 15, done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 15 (delta 2), reused 15 (delta 2), pack-reused 0
Unpacking objects: 100% (15/15), done.
Checking connectivity... done.
```

This cloned repository comes with a few that we haven't seen before.

```sh
> git --graph --oneline --decorate master

* a00e002 (HEAD, origin/master, origin/HEAD, master) Raw elephant image
* 7e4bb5c Initial commit
```

Previously we've seen `HEAD` and `master`, but what is `origin`?

Let's see that again in slow motion.


Remote
------

It's actually possible to clone a repository in a slightly different way,
which may help understand a few things.

```sh
> mkdir test2
> cd test2
> git init

Initialized empty Git repository in test2/.git/

> git remote add origin https://github.com/charleso/git-training.git
```

At this point we've added one "remote" to Git.
You can think of it like an "alias", or short-hand, for that long URL.
The name "origin", much like "master", is just a default when you
first clone. Because we've manually added the remote rather
than clone we can choose what we like, but let's stick with "origin".


### Question

> Can you add more remotes to that repository?


Fetch
-----

However, you should notice there there's no files or branches in that repository.
`git remote` doesn't actually do anything apart from update configuration.

```sh
> ls -F
> ls -F .git/refs

heads/
tags/
```

We need to actually download the Git repository. You can do this with the `fetch` command.

```sh
> git fetch origin

remote: Counting objects: 15, done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 15 (delta 2), reused 15 (delta 2), pack-reused 0
Unpacking objects: 100% (15/15), done.
From https://github.com/charleso/git-training
 * [new branch]      master     -> origin/master
```

What's extermely powerful about Git is that `fetch` will download _all_ of the repository,
not just the files in `master`. It should contain all of the history too for _all_ of
the branches.

```sh
> ls
> git branch
```

Hmm, what gives? We still don't have any files/branches. Or do we?

```sh
> ls -F .git/refs

heads/
remotes/
tags/

> ls -F .git/refs/remotes

origin/

> ls -F .git/refs/remotes/origin

master

> cat .git/refs/remotes/origin/master

a00e00231ddec7a0ecd32f45789f25e7bd61cbdf
```

So we don't have any `refs/heads`, but we _do_ have `refs/remotes/origin`.

Whatever old man. Show me the files!


Checkout
--------

**WARNING** This next section is extremely tricky but crucial.
This is often where Git tries to make things "easy" which leads to confusion when
Git stops being nice and expects you to know what just happened.
You have been warned.

So how do we checkout these remote branches?

What people _normally_ type:

```sh
> git checkout master

Branch master set up to track remote branch master from origin.
Already on 'master'
```

What _really_ happened.

```sh
> git branch master origin/master

Branch master set up to track remote branch master from origin.

> git checkout master

Already on 'master'
```

So what's the problem? The first one looks much easier.

Let's see that again, but with a twist.

```sh
> git branch my_master origin/master

Branch my_master set up to track remote branch master from origin.

> git checkout my_master

> git --graph --oneline --decorate my_master

* a00e002 (HEAD, origin/master, my_master) Raw elephant image
* 7e4bb5c Initial commit
```

Keep in mind that this is the _exact_ same thing as before.
The only difference is that we've given our _local_ branch a difference name.
Let me put that another way.

- The first rule of Git remotes is that
  you cannot checkout remote branches.
- The second rule of Git remotes is that
  you **cannot checkout remote branches**



### Advanced Questions

> The `HEAD` files points to a ref, the remote branches are just refs.
> What happens if you manually change the `HEAD` file to point to `refs/remote/origin/master`?
> If you do, and then make a commit, what happens if you `fetch` after that?


Next
----

That's probably enough for one section.
Read about [push](push.md) to see how to share your changes.
