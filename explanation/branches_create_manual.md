> What happens if you create a `refs/heads` file manually?

```sh
> echo "41ce7faa5b8b2cf480d44c3b12f0545fed9683c3" > .git/refs/heads/manual

> git branch

  hello
  manual
* master

> git log --graph --oneline --decorate master

* 41ce7fa (HEAD, master, manual) Third commit
* 672e562 (hello) Second commit
* 406bb3b Initial commit
```

It's _exactly_ the same as using the `branch` command to create one.

Apologies for sounding like a broken record, but a branch is _just_ a
reference to a commit, nothing more.
