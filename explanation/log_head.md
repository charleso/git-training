> What happens if you don't supply `log` a commit/ref, what does it default to?

```sh
> git log

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```

It's important to keep in mind that `log` _always_ has to "start" from a commit.
It's _not_ showing all the commits, which isn't obvious yet until we have more branches.

The question is - how does it decide which commit to start from?

It's using `HEAD`, as do many of Git's commands when not supplied with a starting commit.

```sh
> git log HEAD

* 41ce7fa (HEAD, master) Third commit
* 672e562 Second commit
* 406bb3b Initial commit
```

So in _this_ case `HEAD` is referencing `refs/heads/master`, which is referencing
`41ce7fa`, and that's what we're observing. Later on when we create more branches
try running `git log` again.
