Git - Pull
==========

You should read about [remotes](remotes.md) before starting this section.


Schizophrenia
-------------

So currently we now have two local git repositories,
`local` which is a clone of the original `test`.
That is to say `local` has a remote (called "origin") that references `test`.

For this next demonstration we want to pretend like we're two
different users working remotely, and it's important that we distinguish which
of the two repositories we're dealing with.

From now on think of `test` like the remote server (eg. Github),
and `local` as the one you've just cloned.
This is a very common setup.

What we want to do now is "simulate" someone else changing the remote
repository _at the same time_ as you are changing the local copy.
If you're working in any kind of team this happens every day.
We'd better get used to it.


```sh
> cd ../test
> echo "remote" >> remote.txt
> git add .
> git commit -m "Working remotely"

> cd ../local
> echo "local" >> local.txt
> git add .
> git commit -m "Working locally"
```

Note that we're updating different files at this point,
otherwise we would run in to merge conflicts, which is
not something we want to tackle here and now.

So how do we bring down the changes from the "remote" (ie. "test") repository
to the "local" repository?


Pull
----

So what typically happens at this point is that people say to "pull".
If everyone else jumps off a bridge...

```sh
> git pull

remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), done.
From ../test
   c99f4ac..c6756d7  master     -> origin/master
Merge made by the 'recursive' strategy.
 remote.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 remote.txt

> git log --graph --oneline --decorate my_master

* fdff1be (HEAD, my_master) Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (orign/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

> What files do you see in the working directory?

> What do you think would have happened if we had modified the same file?


Fetch
-----

As usual, Git is trying to be helpful and make things "convenient" for us.
As we've done before, let's break down what `pull` is actually doing.

Firstly let's use the `fetch` command that we've seen when we did
our "manual" `clone`.

```sh
> git fetch origin

remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), done.
From ../test
   c99f4ac..c6756d7  master     -> origin/master

> git log --graph --oneline --decorate my_master

* 6a9bac9 (HEAD, my_master) Working locally
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```


> Why can't we see the `origin/master` commits/ref[?](explanation/log_resolve.md)

> Do you expect to see the `remote.txt` file in the working directory?

> If you wanted to view `remote.txt` how might you do that with
> the commands you already know[?](explanation/pull_checkout.md)


We actually want to see both refs in the log together.

```
> git log --graph --oneline --decorate my_master origin/master

* 6a9bac9 (HEAD, my_master) Working locally
| * c6756d7 (orign/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

Previously when we ran `pull` we saw an extra commit,
combining both the local and remote master branches.
Where did that come from?


Merge
-----

So the problem is that `pull` = `fetch` + `merge`.
As we've seen `fetch` just downloads the latest commits
and refs from the remote repository.
It's when we start talking about `merge` that things get a little
more complicated, and which is why `pull` can get messy.

We might need to stop at this point and talk about what merging is at a
high-level.

So just thinking about what we did to the `test` and `local` repositories.
In each repository we added a _different_ commit with different files.
Imagine that you had two directories and you copied the contents
of one over the other. What would you want the final result to be?
If the files are different that's easy - you want all the files.
But in the case were the same file exists in both you want to make
sure that we keep the relevant contents of both versions.
Let's wave our hands at this point, and pretend we have a way of doing
that easily. The final result, in git, will be a _new_ commit.
The _merge_ commit.

So the `merge` command takes two commits, and creates a new one
containing (_hopefully_) the contents of both commits.
Actually technically it takes one commit and merges it with the
`HEAD` branch, in this case `my_master`.

```sh
> git merge origin/master

Merge made by the 'recursive' strategy.
 remote.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 remote.txt

> git log --graph --oneline --decorate my_master

* fdff1be (HEAD, my_master) Merge branch 'origin/master' into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (orign/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

> Does a merge have _anything_ to do with remotes[?](explanation/pull_merge_remotes.md)

> Can you see both remote and local files now?

> How can you undo that merge commit[?](explanation/pull_merge_undo.md)

> Try modifying the same file in both repositories
> and see what happens when you merge.


Final Advice
------------

Honestly, I _always_ suggest running `fetch` and then `merge` manually.
Doing so makes the workflow so much more clearer, even if it means
running two commands instead of one.


Next
----

That's probably enough for one section.
Read about [push](push.md) to see how to share/publish your changes.
