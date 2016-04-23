> Can you run the `log --graph` for this ref/commit?

Of course!

```sh
> git log --graph --oneline --decorate refs/remotes/origin/master

* 41ce7fa (origin/master) Third commit
* 672e562 (origin/head) Second commit
* 406bb3b Initial commit
```

So you can actually just show the log using the abbreviated name.

```sh
> git log --graph --oneline --decorate origin/master

* 41ce7fa (origin/master) Third commit
* 672e562 (origin/head) Second commit
* 406bb3b Initial commit
```

Or for all the remote branches.

```sh
> git log --graph --oneline --decorate --remotes

* 41ce7fa (origin/master) Third commit
* 672e562 (origin/head) Second commit
* 406bb3b Initial commit
```

The `--remotes` flag returns a subset of `--all`, which
would also include local heads (and other things).
You can use `--branches` if you just want local branches.

This is an extension of the explanation [here](log_resolve.md).

