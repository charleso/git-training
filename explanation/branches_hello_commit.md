> Try making a new commit on `hello`, what does the graph look like now?

```sh
> git log --graph --oneline --decorate hello

* 80f35bf (HEAD, hello) Hello commit
* 672e562 Second commit
* 406bb3b Initial commit
```

Remember that `log` only follows the history for the supplied commit,
in this case the one that `hello` references.
This no longer include the most recent commit that `master` references.

How can we see the commits both both `hello` _and_ `master`.

```sh
> git log --graph --oneline --decorate hello master

* 80f35bf (HEAD, hello) Hello commit
| * 41ce7fa (master) Third commit
|/
* 672e562 Second commit
* 406bb3b Initial commit
```

If you want to see _all_ the branches, then `--all` is handy.

```sh
> git log --graph --oneline --decorate --all

* 80f35bf (HEAD, hello) Hello commit
| * 41ce7fa (master) Third commit
|/
* 672e562 Second commit
* 406bb3b Initial commit
```
