> What happens if you change the hash of `refs/heads/hello` to another commit?

```sh
> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit

> echo 41ce7faa5b8b2cf480d44c3b12f0545fed9683c3 > .git/refs/heads/hello

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master, hello) Third commit
* 672e562 Second commit
* 406bb3b Initial commit

> echo 406bb3bffbd02113ad5e2fecb4da364c01b20bb3 > .git/refs/heads/hello

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b (hello) Initial commit
```

It's worth mentioning at this point that this can be quite dangerous.
For example, if `hello` was pointing at new commit not yet
part of `master`, then at this point you will have "lost" it.
Not to fear, you always have the [reflog](../reflog.md), but it's not
something you should be doing unless you're careful.

As a point of reference, the Git command for "moving" a branch is
the following.

```sh
> git branch --force hello 672e562

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

This is _no_ safer than updating the file, Git won't stop/warn you about
losing a commit.

The _safe_ way of doing this is to `merge` if you want to move a commit
"forwards", or create a _new_ branch if you want to go backwards.
