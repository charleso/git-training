Git - Push
==========

You should read about [pull](pull.md) before starting this section.


Push
-----

So where were we?

```sh
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

How do we "share" our work with the remote server?

Most of the time you'll see the following documented.

```sh
> git push
```

And in fact this is _often_ all that is required.
However this is another one of those cases where
Git is being nice and saving us some typing.

Let's look at some of the ways pushing can fail.


Match
-----

If you're following along at this point (and depending on your version of `git`),
you will probably see the following error.

```sh
fatal: The upstream branch of your current branch does not match
the name of your current branch.  To push to the upstream branch
on the remote, use

    git push origin HEAD:master

To push to the branch of the same name on the remote, use

    git push origin my_master
```

So because we've created a branch with a different name "my_master"
Git doesn't know what we mean.
One of it's suggestions is the following.

```sh
> git push origin HEAD:master
```

Let's unpack that.

- `git push`
  - Upload any of my local commits to...
- `origin`
  - The name of the remote, which is just an alias for the full Git URL
    (eg. "../test" in this case or something like https://github.com/charleso/git-training.git).
- `HEAD:master`
  - Update `refs/heads/master` _on the remote_
    to the commit that `HEAD` (ie `refs/heads/my_master`) is referencing _locally_
  - If you're pushing from/to the same branch name (eg. `master:master`) then
    you can just shorten that to just the name. (eg. `git push origin master`)

My advice to people starting with Git is to always type this out,
just as a reminder of what is really going on.


Denied
------

Unfortunately if you run that command, and you've been following along closely,
it's likely that you'll now see _this_ horrible error.

```
Counting objects: 7, done.
Writing objects: 100% (3/3), 255 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: error: refusing to update checked out branch: refs/heads/master
remote: error: By default, updating the current branch in a non-bare repository
remote: error: is denied, because it will make the index and work tree inconsistent
remote: error: with what you pushed, and will require 'git reset --hard' to match
remote: error: the work tree to HEAD.
remote: error:
remote: error: You can set 'receive.denyCurrentBranch' configuration variable to
remote: error: 'ignore' or 'warn' in the remote repository to allow pushing into
remote: error: its current branch; however, this is not recommended unless you
remote: error: arranged to update its work tree to match what you pushed in some
remote: error: other way.
remote: error:
remote: error: To squelch this message and still keep the default behaviour, set
remote: error: 'receive.denyCurrentBranch' configuration variable to 'refuse'.
To ../test
 ! [remote rejected] my_master -> master (branch is currently checked out)
 error: failed to push some refs to '../test'
```

Yuck. But don't worry too much about what you're witnessing, it's not something you'll
normally see when your repository is cloned from a "real" remote server like Github.
It's only happened because we have two normal Git repositories checked out.

Basically you can't push to a branch that's checked out, which in this case
is the `master` branch in the `test` repository.
To work around this you can either:

1. Push to anything _but_ the `master` branch

    ```sh
    git push origin my_master
    ```

2. Go back to the `test` repository and checkout another branch

   ```sh
   cd ../test
   git branch ignoreme
   git checkout ignoreme
   ```

Let's just create a new branch.


Success
-------

```sh
> git push origin my_master

Counting objects: 7, done.
Writing objects: 100% (3/3), 255 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ../test
 * [new branches]    my_master -> my_master
```

```sh
> git log --graph --oneline --decorate my_master

* fdff1be (HEAD, my_master, origin/my_master) Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (orign/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

So we've just created a new branch on the remote repository.
You can even see a new `origin/my_master` remote ref has been created _localy_
to represent this.

```sh
> cd ../test
> git log --graph --oneline --decorate my_master

* fdff1be (my_master) Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (HEAD, master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

Switching back to the "remote" repository things look basically the same,
except that `origin/` remote refs are now just "local".


Fast Forward
------------

So what happens if "someone else" updates the `my_master` branch
in the remote repository?
This is the same scenario that we saw earlier when we had different
local and remote commits. Let's do that one more time.

```sh
> cd ../test
> git checkout my_master
> echo "remote" >> remote.txt
> git add .
> git commit -m "Working remotely again"
# Switch branches to avoid the push error we saw earlier
> git checkout master

> cd ../local
> echo "local" >> local.txt
> git add .
> git commit -m "Working locally again"
```

And so we have:

```
> git log --graph --oneline --decorate my_master

* b49a323 (HEAD, my_master) Working locally again
* fdff1be (origin/my_master) Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit
```

What happens if we try to push now?

```
> git push origin my_master

To ../test
 ! [rejected]        HEAD -> my_master (fetch first)
error: failed to push some refs to '../test'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

You might want read about fast-forward pushes in
[git push --help](https://git-scm.com/docs/git-push#_note_about_fast_forwards).

> Try to push the `my_master` branch successfully (Hint: we've done this [before](pull.md))

> [Advanced] How would you delete a branch using just push[?](explanation/push_delete.md)
> NOTE: This is probably not immediately obvious.


Force
-----

**Warning:** Please be careful with this next command. I want to cover
what it's doing, but it's one of those things that can really cause significant
pain if used incorrectly.

What happens if we don't want a fast-forward (read: safe) push?

```sh
> git fetch origin

remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), done.
From ../test
   fdff1be..928b167  my_master  -> origin/my_master

> git log --graph --oneline --decorate my_master origin/my_master

* b49a323 (HEAD, my_master) Working locally again
| * 928b167 (origin/my_master) Working remotely again
|/
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit

> git push --force origin my_master

Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 289 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To ../test
 + fdff1be...b49a323 new_master -> new_master (forced update)

> git log --graph --oneline --decorate my_master origin/my_master

* b49a323 (HEAD, my_master, origin/my_master) Working locally again
* fdff1be Merge branch 'master' of ../test into my_master
|\
* | 6a9bac9 Working locally
| * c6756d7 (origin/master) Working remotely
|/
* 41ce7fa Third commit
* 672e562 (origin/hello) Second commit
* 406bb3b Initial commit

```

Ignoring the transfer of commits and their files to the remote repository,
the `push` command is really just updating a remote `refs/heads` file.
Adding `--force` just bypasses the fast-forward check and updates that refs file
no matter what. It's similar/equivalent to using `branch --force` locally.

> [Advanced] How would you "recover" that "remote" commit[?](explanation/push_force_recover.md)
> (Hint: Come back after the [advanced](../README.md#advanced) sections)


Next
----

Too easy? Check out the [advanced](README.md#advanced) section for more Git fun.
