Git - Push
==========

You should read about [remotes](remotes.md) before starting this section.


Local
-----

So where were we?

```sh
> git --graph --oneline --decorate my_master

* a00e002 (HEAD, origin/master, my_master) Raw elephant image
* 7e4bb5c Initial commit
```

So our current branch (`HEAD`) is referencing `my_master`
(or `refs/heads/my_master` to be exact).

Let's make a local commit.

```sh
> echo "local" >> test.txt
> git add .
> git commit -m "Local changes"

[master 1712de5] Local changes
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt

> git --graph --oneline --decorate my_master

* 1712de5 (HEAD, my_master) Local changes
* a00e002 (origin/master) Raw elephant image
* 7e4bb5c Initial commit
```

It's important to note that this commit is only/still local
at this point. Almost all commands in Git will only
work on your local repository.


Push
----

Most of the time you'll see the following documented.

```sh
> git push
```

And in fact this is _often_ all that is required.
However this is another one of those cases where
Git is being nice and saving us some typing.
What do we really mean?

```sh
> git push origin my_master:master
```

Let's unpack that.

- `git push`
  - Upload any of my local commits to...
- `origin`
  - The name of the remote, which is just an alias for the full Git URL
    (eg. https://github.com/charleso/git-training.git).
- `my_master:master`
  - Update `refs/heads/master` _on the remote_
    to the commit that `refs/heads/my_master` is referencing _locally_

My advice to people starting with Git is to always type this out,
just as a reminder of what is really going on.


Next
----

Too easy? Check out the [advanced](README.md#advanced) section for more Git fun.
