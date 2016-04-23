> Can you use `HEAD`, `master` or even `refs/heads/master` in the `log` command?

```sh
> git log --graph --oneline --decorate HEAD

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit

> git log --graph --oneline --decorate master

...

> git log --graph --oneline --decorate refs/heads/master

...
```

Yep! The `...` just means the same output to save space.

It's important to note that all git is doing is "resolving" the ref to
a commit, and then using that. There's _nothing_ differing about
asking to see the log for a commmit or a ref that points to that commit.

Also note that you can use a subset of the ref, like so.

```sh
git log --graph --oneline --decorate heads/master
...
```
