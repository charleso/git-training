Git - Remotes
=============

You should read about [branches](branches.md) before starting this section.

So way back in the beginning we ran `git init` to create a
new repository.
However, as is often the case you're actually very likely
to want to get a copy of an existing repository.


Clone
-----

If you've ever used Git before it's quite possible you've cloned a repository,
which contained a number of pre-existing files, commits and branches.

Normally you'll find yourself cloning something from the web, and in
particular Github. However, there's not special about Github,
and in fact for the purposes of this guide let's clone the repository
we've just been working in.

```sh
> cd ..

# Clone the current "test" repository to another folder called "local"
> git clone test test-clone

Cloning into 'test-clone'...
done.
```

This cloned repository looks a little different than our test repository.

```sh
> cd test-clone
> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, origin/master, origin/HEAD, master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Previously we've seen `HEAD` and `master`, but what is `origin`?

Let's see that again in slow motion.


Remote
------

It's actually possible to clone a repository in a slightly different way,
which may help understand a few things.

```sh
> cd ..
> mkdir local
> cd local
> git init

Initialized empty Git repository in local/.git/

# This assumes you called the other git repository "test"
> git remote add origin "../test"
```

At this point we've added one "remote" to Git.
You can think of it like an "alias", or short-hand, for that filepath
(which is normally going to be a long URL).
The name "origin", much like "master", is just a default when you
first clone. Because we've manually added the remote rather
than clone we can choose what we like, but let's stick with "origin".


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
From ../test
 * [new branch]      hello      -> origin/hello
 * [new branch]      master     -> origin/master
```

What's extermely powerful about Git is that `fetch` will download _all_ of the repository,
not just the files in `master`. It should contain all of the history too for _all_ of
the branches.

```sh
> ls
> git branch

> git log --graph --oneline --decorate master

fatal: ambiguous argument 'master': unknown revision or path not in the working tree.
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

hello
master

> cat .git/refs/remotes/origin/master

41ce7faa5b8b2cf480d44c3b12f0545fed9683c3
```

So we don't have any `refs/heads`, but we _do_ have `refs/remotes/origin`.

> Can you run the `log --graph` for this ref/commit?

Whatever old man. Show me the files!


Checkout
--------

**WARNING** This next section can be quite subtle but is crucial.
This is once place where Git tries to make things "easy" which leads to
confusion when it stops being nice and expects you to know what just happened.
You have been warned.

So how do we checkout these remote branches?

What people _normally_ type:

```sh
> git checkout master

Branch master set up to track remote branch master from origin.
Already on 'master'

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, origin/master, master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

What _really_ happened.

```sh
> git branch master origin/master

Branch master set up to track remote branch master from origin.

> git checkout master

Already on 'master'
```

So what's the problem? Typing just `git checkout master` looks much easier.

Let's see that again, but with a twist.

```sh
> git branch my_master origin/master

Branch my_master set up to track remote branch master from origin.

> git checkout my_master

> git log --graph --oneline --decorate my_master

* 41ce7fa (HEAD, origin/master, my_master) Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Keep in mind that this is the _exact_ same thing as before.
The only difference is that we've given our _local_ branch a difference name.

- The first rule of Git remotes is that
  you cannot checkout remote branches.
- The second rule of Git remotes is that
  you **cannot checkout remote branches**

As a rule I always recommend people never create a local branch called `master`
to avoid confusion that is likely to ensue.


> If your local branch is (also) called `master`, what happens if you run `git log master`?
> Which branch are you asking about?
> How could you find out?

> What happens if you _do_ try to checkout a remote branch
> (eg. `git checkout origin/master`)?
> How does that change the `HEAD` file?
> Is that what you would expect?

> [Advanced] The `HEAD` files points to a ref, the remote branches are just refs.
> What happens if you manually change the `HEAD` file to point to `refs/remote/origin/master`?
> If you do, and then make a commit, what happens if you `fetch` after that?


Next
----

That's probably enough for one section.
Read about [pull](pull.md) to see how to get more changes over time.
